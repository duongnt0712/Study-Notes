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
### Why we need to use functional interface?
`Functional Interfaces`are mainly used in `Lambda Expressions`, `Method References` and `Constructor References`. 
`Functional Interfaces` serves as a data type of `Lambda Expressions`. Since a `Functional Interface` contains only one abstract method, the implementation of that method becomes the code that gets passed as an argument to another method. 
### Java's built-in Functional Interface
#### Functions
The most simple and general case: parameterized by the types of its argument and a return value.
```java
public interface Function<T, R> { … }
```
