# A Neat Trick to Easily Upgrade the Readability of Your Unit Tests

<img src="https://github.com/olgam4/articles/blob/main/testing/better-testing/thought-catalog-mmWqrsjZ4Lw-unsplash.jpg " width="100%" alt="It seems way more relaxing to read this than to read some tests I wrote two years ago whilst learning TDD in uni.">

Have you ever heard that tests are supposed to "drive your development" (thus the name test-*driven* development): you should think about your desired outcome, make sure your new functionality will work as intended and *only* then are you going to implement it. That's what *TDD* is supposed to be. And… What if I told you that you could even upgrade your tests to more easily drive your development?

More often than not, your code will be interacting with something else, whether it be an API, some underlying techno or something entirely different. Since your test should only be asserting that the one functionality your working on is behaving, you don’t want your test to fail because of some exterior context which has changed, or more to the point: if the context hasn't changed, but its implementation has. If you’ve heard about the “Given When Then” strategy to testing, then you’ll know that our `Given` is the current state of our application. Sometimes, this becomes a boiler which is incredibly tedious and is bound to be different for almost every test along the way.

#### Don't forget that this article is highly opinionated and don't be shy to comment to enhance everyone's knowledge. With that out of the way... let's begin!

## Toyato Car Tests

So here we are: testing our Car implementation. You have to setup your car beforehand, then stop the car. The outcome depends on the given state. You could take this setup in a `@Setup` but you prefer sticking with the `GWT`. Just like me, you like your code to tell a story when it's being used.

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

But then... A problem occurs. It’s all fun and games until your `Given` now spans across fifty lines and takes five minutes to read… Aren’t tests supposed to be easily readable and intuitive? Well, personaly, I’m definitely not fully understanding what I was trying to achieve in the first place, especially not four months after we've merged this.
Some would say that taking this setup into a private function in your test class would be enough, but imagine: now, you have four more functions to handle whatever case you had and you need to implement the same functions in some other test class because you need your real Domain Object there too...

I hear you crying: yes but it is perfectly okay to have different given states depending on what you want to test 🥲  I agree: what isn’t okay is that in four months, no one will want to read your `Given` and your test will basically be rendered useless, affecting the trust you had in your application your ability to improve upon it. 

## The Magic Pattern

<img src="https://github.com/olgam4/articles/blob/main/testing/better-testing/910Uj-uTAcL._SX600_.jpg" width="500" alt="Rescue Heroes to the Rescue">

Here they come to the rescue: `Builders`. Forget the past: finished are those times you had to know which parameter you had to put in first. Now, your `Given` is quickly read and tells a story... But how?

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

Some might ask why do this. Doesn't it seem over-designed? Maybe. If you find yourself refactoring tests over and over again just because you now have a new dependacy which is passed through the constructor, well you now have only one single line to change, instead of all of these. Also, your `@Setup` should prepare your tests, but you shouldn't have to go back and forth between them, especially not when you have to copy/paste the entire thing in all those tests which aren't exactly like the happy path. Your setup is easy to manage and says exactly what it has to say. You could change `.aCar()` to `.aDefaultCar()`, but more often than not, `Builder` Pattern already means that.

## What's next?

"Oh my, nothing is perfect", says my teacher as they try to explain some complex algorithm. Unfortunately, the Heroes also aren't perfect. When you've used this pattern long enough, you will realize that it is now your `Builder` who knows way too much and creates everything itself. The problem is that if someday, you change how `Engine` works because you learnt that you had to use composition over inheritance... Then you have to change every `new` statement in your code to use this: even in your tests! That refactor won't be fun...(Seems like a trend, isn't it?)

Well couldn't we just use another `Builder` to achieve this? In my experience, I've found that `Builders` are better suited for complex objects you may want to parametrize. We understood that we only wanted to *generate* some attribute, so that's what we did!

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

### A Case for the Generator

Let's address the elephant in the room: most people will say that `Generators` are overkill. Sometimes, they are: don't just use something you found on the Internet without thinking it through first. `Generators` fall into the category of `Creational Patterns`. As for most of them, they help us *create* something we need without the hassle it generally comes with, with the added benefit to inject some `Mocks` down the line, especially in *TDD*. Why use them and not simply add constants directly in the `Builder`? Well simply put, we found ourselves having complex `Value Objects` needed to be instantiated and lots of lines of complicated code before you even could read the class. Moving it to `Generators` let us distinguish between different responsibilities and unclog our `Builders`. Then, `Generators` acted as simple "factories" which we used in our `Builders` to alleviate some *setup*, just like in our tests.

Now, you have a way to generate your whole car easily and change its attributes to drive your test. But a problem clearly remains...

## Isn't it an anti-pattern?

Your whole test battery uses this exact same `Bertha` car, an old model. The problem lies exactly there. We've created some magic value which every test depends on: one major point of failure in which we had put all our faith in...Normally, every test would be keen to this. You think you’re safe, you’ve thought of every possible detail...But are you, really? What if in production, some attribute combination breaks the price? It has happened to me and we were flabbergasted to see it happen. Our boss wasn't be happy about it, especially since it could have been easily avoided. How you ask?

So let me introduce you to...[Faker](https://github.com/faker-ruby/faker) 🎉 This beauty lets you randomize your tests which then serves the purpose of finding out some tests may have been badly designed and discovering edge cases you wouldn't have imagined could happen. Yes, it does make your tests "flaky", but it helps you catch bad design before it creeps up on you. Also, reproductibility is of the most importance when testing. Therefore, you should always seed your randomness and log it somewhere in order to properly debug later. Don't forget to change those seeds though!

First of all, our previous test had a big flaw: a putrid magic number. As some of you may have noted, we used `1990` for the build year of our car. Every single test will have a thirty-something years old car, which may become a problem down the line. What if I forgot something? I know I always do. Well randomizing this kind of thing will definitely help our noble cause, and run your unit tests more than once. Simply add two constants for the minimum and maximum years and pick a random number in this range!

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

As I said earlier, it is now a great idea to run your tests more than one. If you see some tests failing once every five times because of randomness, be happy you caught it before it failed in production!

## Bravo! You did it ✨🥳

In the end, we've accomplished our main quest: reading our test is now that much easier. To top it all off, we can now easily change the way we instantiate the object we're testing, change its constructor signature and we won't have to refactor our whole code base. Also, our tests are now randomized and will help us find unheard of edge cases...If you still are not convinced, let me share with you a horrible example.

``` java
class UglyQuoteTest {
  @Test
  givenACompletedQuote_whenPaying_thenItShouldNotifyThePayingCenterWithTheRightPrice() {
    Id id = new Id(123L);
    Name name = "Olivier Gamache";
    Claim firstClaim = new Claim(WATER_DAMAGE);
    Claim secondClaim = new Claim(THEFT);
    Claim thirdClaim = new Claim(FIRE);
    List<Claim> claims = Arrays.AsList(firstClaim, secondClaim, thirdClaim);
    Address address = new Address('U8S 2T6');
    Time timestamp = Timestamp.now();
    PayingCenter payingCenter = Mock(PayingCenter.class);
    // We could go on and on and on and on...
    Quote quote = new Quote(id, name, claims, address, timestamp, payingCenter);
    
    Money price = quote.pay()
      
    verify(payingCenter).notify(price);
  }
}

class BeautifulQuoteTest {
  @Test
  givenACompletedQuote_whenPaying_thenItShouldNotifyThePayingCenterWithTheRightPrice() {
    Quote quote = QuoteBuilder.aQuote().withPayingCenter(Mock(PayingCenter.class))
    
    Money price = quote.pay()
      
    verify(payingCenter).notify(price);
  }
}
```

We could imagine that the `QuoteBuilder` uses `Generators` to randomize its setting, but you get the point! Doing it this way lets our team put more trust in our tests because they are simple to understand and to implement. If we need to change something, it will be in exactly one spot and we won't have to change our entire application. Note that the `Builder` pattern would be of great use elsewhere in your code: instantiating objects is somewhat crucial in `OOP`, so with that new tool in your toolbox, have fun coding! If you've made it this far, I want to thank you for reading and I hope I've helped you cleaning up those tests so that it is now easier for you and your team to keep them that way! 😌

Some of you may have feel some discomfort while reading the last test. Why return the price? Only to be sure it was called with it? Isn't that... bad? Also, wouldn’t the test fail since it isn’t the same object? You caught me. If you want to read more, stay tuned for my next article which will tackle how I like to use `Mockito Matchers` for testing!

Special thanks to:
[Rescue Heroes on Amazon Prime](https://www.amazon.com/Rescue-Heroes-Season-1-US/dp/B01MYWOO25)
