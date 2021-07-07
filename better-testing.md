# Builder pattern

Have you ever heard that tests are supposed to “pilot” your development; you should think about the outcome, make sure your new functionality will work as intended and *only* then are you going to implement it.

Depending upon context, you’ll have your code interacting with something. Since your test should only be asserting one functionality is working, you don’t want your test to fail because of some context which has changed. If you’ve heard about the “Given When Then” strategy to testing, then you’ll know that our Given is the current state of our application. Sometimes, this boiler is incredibly tedious and different with every test you’re encountering.

## Toyato

```java
@Test
givenARunningCar_whenStopping_thenEngineStops()
    Year buildYear = new Year(1990)
    Engine engine = new WorkingEngine();
    List<Passenger> passagers = new ArrayList();
    Car car = new Car(buildYear, engine, passengers);
    car.start();

    car.stop();

    expect(car.isRunning).toBeFalse();
}

@Test
givenAFaultyEngineAndARunningCar_whenStopping_thenCarExplodes()
    Year buildYear = new Year(1990)
    Engine faultyEngine = new FaultyEngine();
    List<Passenger> passagers = new ArrayList();
    Car car = new Car(buildYear, faultyEngine, passengers);
    car.start();

    assertThrows(CarExplosion.class, () -> {
        car.stop();
    });
}
```

It’s all fun and games until your “given” takes fifty lines to read… Aren’t tests supposed to be easily readable and intuitive? Well, fifty declarations do the line, I’m definitely not understanding fully what you were trying to achieve in the first place, especially not four months after we've merged this.
Some would say that taking this setup into a private function in your test class would be enough, but imagine: now, you have four more functions to handle whatever case you had and you need to implement the same functions in some other test class because you need your real Domain Object there too...

I hear you crying: yes but it is normal to have different given states depending on what you want to test :’( I agree: what isn’t normal is that only you simply cannot understand those.

## Builders

Here they come to the rescue: builders. Finished are those times in which you had to remember which parameter came first and whatnot.

```java
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
    
    public CarBuilder withPassengers(Passenger passenger) {
        this.passengers.add(passenger)
        return this;
    }
    
    public static Car build() {
        return new Car(buildYear, engine, passengers);
    }
}
```

```java

@Test
givenARunningCar_whenStopping_thenEngineStops()
    Car car = CarBuilder.aCar().build();
    car.start();

    car.stop();

    expect(car.isRunning).toBeFalse();
}

@Test
givenAFaultyEngineAndARunningCar_whenStopping_thenCarExplodes()
    Car car = CarBuilder.aCar().withEngine(FAULTY_ENGINE).build();
    car.start();

    assertThrows(CarExplosion.class, () -> {
        car.stop();
    });
}
```

Now we only have the parameter which matter!

## Generators

When you've used this pattern long enough, you will realise that it is now your `Builder` who knows way too much and creates everything itself. The problem is that if someday, you change how `Engine` works because you learnt that you had to use composition over inheritance... Then you have to change every `new` statement in your code to use this: even in your tests! That refactor won't be fun...

Well we could use another builder for this purpose! But builders are for complex objects, my car has a price and name... I won't use a builder for this? Well I agree.

```java
public class CarGenerator {
    private CarGenerator() {}
    
    public static createEngine() {
        return new WorkingEngine()
    }
    
    public static List<Passenger> createPassengers() {
        return ArrayList<>();
    }
    
    public static Year createYear() {
        return new Year(1990);
    }
}
```

```java
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
    
    public CarBuilder withPassengers(Passenger passenger) {
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

## Randomness

Your whole test battery uses this same `Bertha` car, an old model. The problem lies exactly there. Every test is keen to this. You think you’re safe, you’ve thought of every possible detail, but you always use the same car! What if in production, if some attribute combination breaks the price? Your boss won't be happy about it, let me tell you.

So let me introduce you to...[Faker](https://github.com/faker-ruby/faker). This beauty lets you randomize your tests and this serves the purpose of finding out some flaky tests.

********* TALK ABOUT MAGIC NUMBER FOR 1990

Since you already use a Generator for your `Car` attributes, it'll be a breeze to implement it!

```java
public class CarGenerator {
    private final Year MINIMUM_YEAR = 1900;
    private final Year MAXIMUM_YEAR = 2022;
    private CarGenerator() {}
    
    public static createEngine() {
        return EngineGeneraor.createWorkingEngine();
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
        return PassengerGenerator.create();
    }
    
    public static Year createYear() {
        return new Year(Faker.instance().number().numberBetween(MINIMUM_YEAR, MAXIMUM_YEAR);
    }
}
```

So there you go! You now have a random car with the added benefit that on the day that any of your building blocks need changing, you will only have to update ONE line of code instead of creating a Pull request with 1000+ lines because "it is a refactor".

## Conclusion

In the end, we've accomplished our goal: reading our test is that much easier. To top it all off, we can now easily change the way we instantiate the object we're testing, change its contructor signature and we won't have to refactor our whole code base AND our tests and randomized to help us catch flaky tests...

If you've made it this far, I want to thank you for reading and I hope I've helped you cleaning up those tests so that it is now easier for you and your team to keep them that way! 😌

Special thanks to:
