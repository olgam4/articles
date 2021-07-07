# A Neat Trick to Easily Upgrade the Readibility of Your Unit Tests

<img src="https://github.com/olgam4/articles/blob/main/testing/better-testing/thought-catalog-mmWqrsjZ4Lw-unsplash.jpg " width="100%" alt="It seems way more relaxing to read this than to read some tests I wrote two years ago whilst learning TDD in uni.">

https://github.com/olgam4/articles/blob/main/testing/better-testing/910Uj-uTAcL._SX600_.jpg

Have you ever heard that tests are supposed to "pilot your development"; you should think about your desired outcome, make sure your new functionality will work as intended and *only* then are you going to implement it. That's what *TDD* is supposed to be.

Depending upon context, you’ll have your code interacting with something. Since your test should only be asserting one functionality is working, you don’t want your test to fail because of some context which has changed. If you’ve heard about the “Given When Then” strategy to testing, then you’ll know that our Given is the current state of our application. Sometimes, this boiler is incredibly tedious and different with every test you’re encountering.

Don't forget that this article is highly opinionated and don't be shy to comment to enhance everyone's knowledge!

## Toyato Car Tests

``` java
class CarTest {

    @Test
    givenARunningCar_whenStopping_thenEngineStops() {
        Year buildYear = new Year(1990)
        Engine engine = new WorkingEngine();
        List<Passenger> passagers = new ArrayList();
        Car car = new Car(buildYear, engine, passengers);
        car.start();

        car.stop();

        expect(car.isRunning).toBeFalse();
    }

    @Test
    givenAFaultyEngineAndARunningCar_whenStopping_thenTheCarExplodes()
        Year buildYear = new Year(1990)
        Engine faultyEngine = new FaultyEngine();
        List<Passenger> passagers = new ArrayList();
        Car car = new Car(buildYear, faultyEngine, passengers);
        car.start();

        assertThrows(CarExplosion.class, () -> {
            car.stop();
        });
    }
}
```

It’s all fun and games until your “given” takes fifty lines to read… Aren’t tests supposed to be easily readable and intuitive? Well, fifty declarations do the line, I’m definitely not understanding fully what you were trying to achieve in the first place, especially not four months after we've merged this.
Some would say that taking this setup into a private function in your test class would be enough, but imagine: now, you have four more functions to handle whatever case you had and you need to implement the same functions in some other test class because you need your real Domain Object there too...

I hear you crying: yes but it is perfectly okay to have different given states depending on what you want to test 🥲  I agree: what isn’t okay is that in four months, no one will want to read your `Given` and your test will be basically rendered useless, affecting the trust you had in it. 

## The Magic Pattern

<img src="https://github.com/olgam4/articles/blob/main/testing/better-testing/910Uj-uTAcL._SX600_.jpg" width="500" alt="Rescue Heroes to the Rescue">

Here they come to the rescue: `Builders`. Forget the past, finished are those times you had to know which parameter you had to put in first. Now, your `Given` is quickly read and reads like a story... But how?

``` java
public class CarBuilder {
    private Year buildYear = new Year(1990);
    private Engine engine = new WorkingEngine();
	private List<Passenger> passengers = new ArrayList<>();
    
    private CarBuilder() {}
    
    public static CarBuilder aCar() {
        return new CarBuilder();
    }
    
    public CarBuilder withBuildYear(Year year) {
        this.buildYear = year;
        return this;
    }
    
    public CarBuilder withEngine(Engine engine) {
        this.engine = engine;
        return this;
    }
    
    public CarBuilder withPassenger(Passenger passenger) {
        this.passengers.add(passenger)
        return this;
    }
    
    public static Car build() {
        return new Car(buildYear, engine, passengers);
    }
}
```

``` java
class CarTest {

    @Test
    givenARunningCar_whenStopping_thenEngineStops() {
        Car car = CarBuilder.aCar().build();
        car.start();

        car.stop();

        expect(car.isRunning).toBeFalse();
    }

    @Test
    givenAFaultyEngineAndARunningCar_whenStopping_thenCarExplodes() {
        Car car = CarBuilder.aCar().withEngine(FAULTY_ENGINE).build();
        car.start();

        assertThrows(CarExplosion.class, () -> {
            car.stop();
        });
    }
}
```

In this example, the building of a car takes seconds to read and understand because we've achieved something big: the S from the SOLID principles is respected, so is the O. You only have to point out what is different in this particular `Given` and voilà~

## What's next?

When you've used this pattern long enough, you will realise that it is now your `Builder` who knows way too much and creates everything itself. The problem is that if someday, you change how `Engine` works because you learnt that you had to use composition over inheritance... Then you have to change every `new` statement in your code to use this: even in your tests! That refactor won't be fun...

Well couldn't we use another `Builder` to achieve this? In my experience, I've found that `Builders` are better suited for complex objects you may want to parametrize. We found that we only wanted to *generate* some attribute, so that's what we did!

``` java
public class CarGenerator {
    private CarGenerator() {}
    
    public static Engine createEngine() {
        return new Engine();
    }
    
    public static List<Passenger> createPassengers() {
        return new ArrayList<>();
    }
    
    public static Year createYear() {
        return new Year(1990);
    }
}
```

``` java
public class CarBuilder {
    private final Year BASE_YEAR = createYear()
    private final Engine BASE_ENGINE = createEngine()
	private final List<Passenger> BASE_PASSENGERS = createPassengers()
    
    private Year buildYear = BASE_YEAR;
    private Engine name = BASE_ENGINE;
    private List<Passenger> passengers = BASE_PASSENGERS;
    
    private CarBuilder() {}
    
    public static CarBuilder aCar() {
        return new CarBuilder();
    }
    
    public CarBuilder withBuildYear(Year year) {
        this.buildYear = year;
        return this;
    }
    
    public CarBuilder withPassenger(Passenger passenger) {
        this.passengers.add(passenger)
        return this;
    }
    
    public CarBuilder withEngine(Engine engine) {
        this.engine = engine;
    }
    
    public static Car build() {
        return new Car(name, engine, passengers);
    }
}
```

Now, you have a way to generate your whole car easily and change its attributes to pilot your test. But a problem clearly remains...

## But isn't it an anti-pattern?

Your whole test battery uses this exact same `Bertha` car, an old model. The problem lies exactly there. We've created some magic value which every test depends one: one major point of failure in which we had put all our faith in...Normally, every test would be keen to this. You think you’re safe, you’ve thought of every possible detail...But are you? What if in production, some attribute combination breaks the price? Your boss won't be happy about it, especially if it could have been easily avoided.

So let me introduce you to...[Faker](https://github.com/faker-ruby/faker) 🎉 This beauty lets you randomize your tests which then serves the purpose of finding out some flaky tests and discovering cases you wouldn't have imagined could happen.

First of all, our previous test had a big flaw: a putrid magic number. As some of you may have noted, we used `1990` for the build year of our car. Every single test will have a thirty-something years old car, which may become a problem down the line. What if we forgot to test something about? Well randomizing this kind of thing will definitely help our noble cause. Simply add two constants for the minimum and maximum years and pick a random number in this range!

Since you already use a Generator for your `Car` attributes, it'll be a breeze to implement it!

``` java
public class CarGenerator {
    private final Year MINIMUM_YEAR = 1900;
    private final Year MAXIMUM_YEAR = 2022;
    private CarGenerator() {}
    
    public static createEngine() {
        return EngineGeneraor.createWorkingEngine(); // Our engine can also have its own builder, its own generator!
    }
    
    public static List<Passenger> createPassengers() {
        int quantityOfPassengers = Faker.instance().number().randomDigit();
        List<Passenger> passengers = new ArrayList<>();
        IntStream.range(0, quantityOfPassengers)
            .mapToObj(i -> createPassenger())
            .forEach(passengers::add);
        return passengers;
    }
    
    public static Passenger createPassenger() {
        return PassengerGenerator.create(); // So does the passenger!
    }
    
    public static Year createYear() {
        return new Year(Faker.instance().number().numberBetween(MINIMUM_YEAR, MAXIMUM_YEAR);
    }
}
```

There you go! You now have a car with the added benefit that on the day that any of your building blocks need changing, you will only have to update ONE line of code instead of creating a Pull request with 1000+ lines because "it is a refactor".

## Bravo! You did it

In the end, we've accomplished our main quest: reading our test is now that much easier. To top it all off, we can now easily change the way we instantiate the object we're testing, change its contructor signature and we won't have to refactor our whole code base. Also, our tests are now randomized and may help us catch flaky tests...

If you've made it this far, I want to thank you for reading and I hope I've helped you cleaning up those tests so that it is now easier for you and your team to keep them that way! 😌

Special thanks to:
