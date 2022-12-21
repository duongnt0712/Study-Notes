## 1. Lambda Expressions
A lambda expression is a short block of code, quite similar to methods, but it doesn't need a name and it can be implemented right in the body of a method.

```java
(parameter1, parameter2) -> { code block }
```
- A lambda can be an argument to a method, a return type from a method or assigned to  a reference. 
```java
// Assigning a lambda expression to a variable 
Comparator comparator = (x, y) -> x.compareTo(y); 
Collections.sort(strings, comparator);
```
- Lambda Expressions never exist alone. There is always a `context` for the expression.
```java
// OK
Consumer cStrInterface = m -> System.out.println(m); 
// Fail
Object objInterface = m -> System.out.println(m);
```
## 2. Functional Interfaces
- Functional Interface is an interface with a single abstract method (SAM).
- Using annotation `@FunctionalInterface` to indicate. Recommend to use:
	- it triggers the compiler to generate errors if there are more than 2 abstract methods.
	- it generates a statement in the Javadocs.
-  Java 8's `default` / `static` methods are not abstract and do not count, a functional interface may still have multiple `default` / `static` method.
- `@Functional Interface` is used by Java's built-in functional interfaces: `Function`, `Supplier`, `Predicate`, `Consumer`, `Operator`, etc.
---
### Why we need to use functional interface?
- `Functional Interfaces`are mainly used in `Lambda Expressions`, `Method References` and `Constructor References`. 
- `Functional Interfaces` serves as a data type of `Lambda Expressions`. Since a `Functional Interface` contains only one abstract method, the implementation of that method becomes the code that gets passed as an argument to another method. 
---
### Java's built-in Functional Interface
#### Functions
The most simple and general case: parameterized by *the types of its argument* and *a return value*.
```java
public interface Function<T, R> { … }
```
The _Function_ interface also has a default _compose_ method that allows us to combine several functions into one and execute them sequentially: 
```java
Function<Integer, String> intToString = Object::toString; 
Function<String, String> quote = s -> "'" + s + "'"; 
Function<Integer, String> quoteIntToString = quote.compose(intToString); 

assertEquals("'5'", quoteIntToString.apply(5));
```
#### Supplier
The _Supplier_ functional interface is yet another _Function_ specialization that does not take any arguments. We typically use it for lazy generation of values.
```java
public double squareLazy(Supplier<Double> lazyValue) { 
	return Math.pow(lazyValue.get(), 2); 
}
```
```java
Supplier<Double> lazyValue = () -> {
	Uninterruptibles.sleepUninterruptibly(1000, TimeUnit.MILLISECONDS);
	return 9d; 
}; 
Double valueSquared = squareLazy(lazyValue);
```
Another use case for the _Supplier_ is defining logic for sequence generation.
- _Stream.generate_ method implements the _Supplier_ functional interface`
#### Consumer
As opposed to the _Supplier_, the _Consumer_ accepts a generified argument and returns nothing. It is a function that is representing side effects.
```java
List<String> names = Arrays.asList("John", "Freddy", "Samuel"); 
names.forEach(name -> System.out.println("Hello, " + name));
```
- _List.forEach_ method implements the _Consumer_ functional interface.
#### Predicate
The _Predicate_ functional interface is a specialization of a _Function_ that receives a generified value and returns a boolean.
```java
List<String> names = Arrays.asList("Angela", "Aaron", "Bob", "Claire", "David"); 

List<String> namesWithA = names.stream() 
			.filter(name -> name.startsWith("A")) 
			.collect(Collectors.toList());
```
- A typical use case of the _Predicate_ lambda is to filter a collection of values.
#### Operator
_Operator_ interfaces are special cases of a function that receive and return the same value type. The _UnaryOperator_ interface receives a single argument. One of its use cases in the Collections API is to replace all values in a list with some computed values of the same type.
```java
List<String> names = Arrays.asList("bob", "josh", "megan"); 
names.replaceAll(name -> name.toUpperCase());
// or just use: names.replaceAll(String::toUpperCase);
```
## 3. Method References
Method references are a special type of lambda expressions. They're often used to create simple lambda expressions by referencing existing methods.
There are 4 types of syntax:
- `Class::staticMethod`
  Refer to static method
- `object::instanceMethod (particular object)`
  Refer to an instance method using a reference to the supplied object
- `Class::instanceMethod (arbitrary object of particular type)`
  Invoke the instance method on a reference to an object supplied by the context
- `Class::new`
  Constructor reference
## 4. Default & Static Methods In Interfaces
### Default Methods in Interfaces
- When you already had an interface, `default` method helps you remain the interface as it is and add the implementation in the normal way without affecting the other methods.
- A class implements an interface which can inherited or overridden default method of that interface
### Static Methods in Interfaces
- Provide an implementation, which cannot be overridden.
- Access the method using the interface name
- Classes do not need to implement an interface to use its static methods.
## 5. Stream API
#### Benefits
- Process with data in declarative way
  `students.stream().map(Student::getName).collect(Collectors.toList());`
- Support parallel with ease
  `students.parallelStream().map(Student::getName).collect(Collectors.toList());`
- Calculate elements on demand. We can create infinite streams
  `Stream<Integer> evenNumbers = Stream.iterate(0, i -> i + 2)`
---
#### Create Stream
- Using `Stream.of()`
```java
Stream names = Stream.of("Gomez", "Morticia", "Wednesday"); Stream ints = IntStream.of(3, 1, 4, 1, 5, 9).boxed();
```
- Using Stream.iterate()
```java
Stream nums = Stream.iterate(BigDecimal.ONE, n -> n.add(BigDecimal.ONE)).limit(10);
```
- Using Stream.generate()
```java
Stream longs = Stream.generate(Math::random).limit(10);
```
- From a collection
```java
Stream names = Arrays.asList("Greg", "Marcia", "Peter", "Jan“).stream();
```
- From an array
```java
Stream names = Arrays.stream(new String[]{"Greg", "Marcia", "Peter", "Jan“});
```
- From `range` and `rangeClosed` methods.
```java
Stream ints = IntStream.range(10, 15).boxed(); // prints [10, 11, 12, 13, 14] 
Stream longs = LongStream.rangeClosed(10, 15).boxed(); // prints [10, 11, 12, 13, 14, 15]
```
---
#### Intermediate Operations
