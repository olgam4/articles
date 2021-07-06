# Builder pattern

Have you ever heard that tests are supposed to “pilot” your development; you should think about the outcome, make sure your new functionality will work as intended and *only* then are you going to implement it.

Depending upon context, you’ll have your code interacting with something. Since your test should only be asserting one functionality is working, you don’t want your test to fail because of some context which has changed. If you’ve heard about the “Given When Then” strategy to testing, then you’ll know that our Given is the current state of our application. Sometimes, this boiler is incredibly tedious and different with every test you’re encountering.

## Insurance

```java
givenACompletedReceipted_whenAddingSavings_thenItTakesThemIntoAccount() {
	Receipt receipt = new Receipt(A_PERSON, A_TIME, AN_AMOUNT, …);

	Money total = receipt.save(STUDENT);

	expect(total).toEqual(TOTAL_MINUS_STUDENT_SAVINGS);
}

@Test(excpeted = IncorrectSavingType)
givenACompletedReceipted_whenAddingIncorrectSavings_thenItThrows() {
	Receipt receipt = new Receipt(A_PERSON, A_TIME, AN_AMOUNT, …);

	Money total = receipt.save(INCORRECT_SAVING);
}
```

And then, every single one of your tests have a different kind of `Receipt`. It’s all fun and games until your “given” takes fifty lines to read… Aren’t tests supposed to be easily readable and intuitive? Well, 50 lines do the line, I’m definitely not understanding fully what you were trying to achieve in the first place.

I hear you crying: yes but it is normal to have different given states depending on what you want to test :’( I agree: what isn’t normal is that only you can understand those.

## Builders

Here they come to the rescue: builders. Finished are those times in which you had to remember which parameter came first and whatnot.

```java
class ReceiptBuilder {
	
}
```

```java

@Test(excpeted = IncorrectSavingType)
givenACompletedReceipted_whenAddingIncorrectSavings_thenItThrows() {
	Receipt receipt = receiptBuilder.aReceipt().withSavingType(INCORRECT_TYPE).build();

	Money total = receipt.save(INCORRECT_SAVING);
}
```

Now we only have the parameter which matters!

## Generators

But then, your builder gets all chaotic and you’ve only moved the problem… 

```java
ReceiptGenerator.generate()
```

## Randomness

Every test is keen to this. You think you’re safe, you’ve thought of every possible detail, but you always use the same “John Doe”. Well… Then I tell you: use Faker :D
