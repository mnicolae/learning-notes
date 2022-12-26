- [Clean Code: A Handbook of Agile Software Craftsmanship](https://www.goodreads.com/book/show/3735293-clean-code)
  * [2. Meaningful Names](#2-meaningful-names)
  * [3. Functions](#3-functions)
  * [4. Comments](#4-comments)
  * [5. Formatting](#5-formatting)
  * [7. Error Handling](#7-error-handling)
  * [Use Exceptions Rather Than Return Codes](#use-exceptions-rather-than-return-codes)
    + [Write Your Try-Catch-Finally Statement First](#write-your-try-catch-finally-statement-first)
    + [Use Unchecked Exceptions](#use-unchecked-exceptions)
    + [Provide Context with Exceptions](#provide-context-with-exceptions)
    + [Define Exception Classes in Terms of a Caller's Needs](#define-exception-classes-in-terms-of-a-caller-s-needs)
    + [Define the Normal Flow](#define-the-normal-flow)
    + [Don't Return Null](#don-t-return-null)
    + [Don't Pass Null](#don-t-pass-null)
- [8. Boundaries](#8-boundaries)
  * [Using Third-Party Code](#using-third-party-code)
  * [Exploring and learning boundaries](#exploring-and-learning-boundaries)
  * [Learning Tests Are Better Than Free](#learning-tests-are-better-than-free)
  * [Using Code That Does Not Yet Exist](#using-code-that-does-not-yet-exist)
  * [Clean Boundaries](#clean-boundaries)

## 2. Meaningful Names

* Use intention-reveling names. The name of a variable, function, or class should answer why it exists, what it does, and how it is used.
* Avoid disinformation
* Make meaningful distinctions
* Use pronounceable and searchable names. Longer names trump shorter names, and any searchable name trumps a constant in code.
* Avoid encodings. Trend toward smaller classes and shorter functions.
* Member prefixes. If you must encode the interface or the implementation, choose the implementation.
* Avoid mental mapping. Clarity is king. Class and objects should be nouns or noun phrases. Methods should have verbs or verb phrases. Accessors, mutators and predicates should be named for their value and prefixed with get, set and is. Factory methods.
* Don't be cute
* Pick one word per abstract concept
* Don't pun
* Use solution domain names vs. use problem domain names
* Add meaningful context. Can be done through prefixes or classes.
* Don't add gratuitous context. Shorter names are generally better than longer ones, so long as they are clear.

## 3. Functions

* Small!
* Blocks within if, else, while statements, and so on should be one line long.
* The indent level of a function should not be greater than one or two.
* Do one thing
* One level of abstraction per function
* Reading Code from Top to Bottom: The Stepdown rule.
* Switch statements
* Use descriptive names.
* Function arguments. The ideal number of arguments for a function is zero (niladic). Next comes one (monadic), followed closely by two (dyadic). Three arguments (triadic) should be avoided where possible. More than three (polyadic) requires very special justification and then shouldn’t be used anyway. Output arguments are harder to understand than input arguments.
* Common monadic functions. Asking a question about the argument or transforming it into something else and returning it. Choose names that make the distinction clear. Event; overall program is meant to interpret the function call as an event and use the argument to alter the state of the system.
* Flag arguments. Avoid.
* Dyadic functions. Be aware that the come at a cost, and you should take advantage of what mechanisms are available to you to convert them into monads.
* Argument objects.
* Argument lists.
* Verbs and keywords. Choosing good names for a function can go a long way towards explaining the intent of the function and intent of the arguments.
* Have No Side Effects. Temporal coupling.
* Output Arguments. Much of the need for output arguments disappears in OO languages because this is intended to act as an output argument.
* Command query separation. Functions should either do something or answer something, but not both.
* Prefer Exceptions to Returning Error Codes. When you return an error code, you create the problem that the caller must deal with error immediately. The benefit of using exceptions is that the error processing code can be separated from the happy path code and can be simplified.
* Extract Try/Catch Blocks.
* Error Handling Is One Thing.
* The `Error.java` dependency magnet
* DRY (Don't Repeat Yourself)
* Structured Programming. Single-entry, single-exit rule. One return statement in a function, no break or continue statements in a loop.
* How do you write functions like this? Writing software is like any other kind of writing (i.e., an incremental process)

## 4. Comments

* Comments are failures.
* Programmers can't realistically maintain them.
* Comments Do Not Make Up for Bad Code.
* Explain Yourself in Code.
* Good Comments: Legal Comments, Informative Comments, Explanation of Intent, Clarification, Warning of Consequences, TODO, Amplification, Javadocs in Public APIs
* Bad Comments: Mumbling, Redundant Comments, Misleading Comments, Mandated Comments, Journal Comments, Noise Comments, Scary Noise.
* Don't Use a Comment When You can Use a Function or a Variable.
* Position Markers. Refrain from using.
* Closing Brace Comments. Try to shorten functions instead.
* Attributes and Bylines. Refrain from using, source control system is better at that.
* Commented-Out Code. Don't do this!
* HTML Comments. Abomination.
* Nonlocal Information. If you must write a comment, then make sure it describes the code it appears near.
* TMI.
* In-obvious Connection. The connection between a comment and the code it describes should be obvious.

## 5. Formatting

* Vertical formatting. Small files are better than larger files.
* Newspaper metaphor.
* Vertical openness between concepts. Each group of lines represent a thought and should be separate from each other with blank lines.
* Vertical density.
* Vertical distance. Concepts that are closely related should be kept vertically close to each other.
* Variable declarations. Variables should be declared as closed to their usage as possible.
* Instance variables. Should be declared at the top of the class.
* Dependent functions. If one function calls another, they should be vertically close, and the caller should be above the callee, if at all possible.
* Conceptual affinity.
* Vertical ordering. A function that is called should be below a function that does the calling.
* Horizontal formatting. Strive to keep lines short.
* Horizontal Openness and Density.
* Horizontal Alignment.
* Indentation.
* Breaking Indentation. TL;DR don't.
* Dummy Scopes. 
* Team Rules.

## 7. Error Handling

## Use Exceptions Rather Than Return Codes

* Old approach: either set an error flag or return an error code that the caller could check.
* Problem: clutters the caller with error checks; it is also easy to forget to check all errors.
* Solution: throw an exception when you encounter an error.
* Benefit: 1) cleaner from lack of error handling obstruction, 2) you will not miss errors you would have to check otherwise

### Write Your Try-Catch-Finally Statement First

* Try block transaction analogy.
* Catch is responsible to leave program in a consistent state. Think of it as doing the rollback in a database transaction.
* Helps you think what the user of the code should expect, no matter what goes wrong with the code that is executed in the try.
* Add tests that force exceptions, then add behaviour to handler to satisfy the tests.

### Use Unchecked Exceptions

* Checked exception are not necessary for the production of robust software.
* Cost of checked exceptions? Violation of open/closed principle and encapsulation.
* Benefit? None unless you are writing a critical library and must catch that checked exception.

### Provide Context with Exceptions

* Goal: provide enough context to determine the source and location of an error.
* Guideline: 1. create informative error messages and instantiate the exception with them. 2. Mention a. the operation that failed and b. the type of failure. Log the exception in the catch.

### Define Exception Classes in Terms of a Caller's Needs

* Most important concern in defining exception classes is how they are caught.
* Handling 3rd party library call exceptions guidance.
* Use different exception classes only if you want to catch one exception and allow the other one to pass through.

### Define the Normal Flow

* Special case pattern.
* Create a class or configure an object so that it handles a special case for you.

### Don't Return Null

* Guidance 1: if you are tempted to return null from a method, consider throwing an exception or returning a special case object instead.
* Guidance 2: if you are calling a non-null returning method for a third-party library, consider wrapping that with a method that throws an exception or returns a special case object.
* Example of empty list as special case object.

### Don't Pass Null

* Guidance: avoid passing null in your code whenever possible.
* No good way to deal with a null that is passed by a caller accidentally.

# 8. Boundaries

## Using Third-Party Code

* Example of using generics to improve code readability.
* Better way: do not pass 3rd party interfaces around system. Encapsulation is one way to achieve that.

## Exploring and learning boundaries

* Concept of learning tests; call the third-party APIs, as we expect to use them in our application. Controlled experiments.

## Learning Tests Are Better Than Free

* Additional benefits; validate for breaking changes during upgrades.
* Boundary tests.

## Using Code That Does Not Yet Exist

* Write interface under your control. Add adapter when 3rd party API is ready.

## Clean Boundaries

* Manage 3rd party interfaces by having very few places in the code that refer to them.
* Solutions/patterns: 1. encapsulate them, or 2. use an adapter to convert from perfect to provided interface.
