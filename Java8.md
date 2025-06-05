
# Java 8 Lambda Expressions and Functional Interfaces

## Functional Interfaces

A functional interface is an interface that contains **exactly one abstract method**. Java 8 introduced the `@FunctionalInterface` annotation to mark interfaces as functional interfaces.

### Key Points:
- Contains exactly one abstract method
- Can contain default and static methods
- Used as the basis for lambda expressions

### Built-in Functional Interfaces

Java 8 introduced several built-in functional interfaces in the `java.util.function` package:

1. **Predicate\<T>**: Represents a predicate (boolean-valued function) of one argument
   ```java
   @FunctionalInterface
   public interface Predicate<T> {
       boolean test(T t);
   }
   ```

2. **Function\<T, R>**: Represents a function that accepts one argument and produces a result
   ```java
   @FunctionalInterface
   public interface Function<T, R> {
       R apply(T t);
   }
   ```

3. **Consumer\<T>**: Represents an operation that accepts a single input argument and returns no result
   ```java
   @FunctionalInterface
   public interface Consumer<T> {
       void accept(T t);
   }
   ```

4. **Supplier\<T>**: Represents a supplier of results
   ```java
   @FunctionalInterface
   public interface Supplier<T> {
       T get();
   }
   ```

## Lambda Expressions

Lambda expressions provide a clear and concise way to implement functional interfaces using an expression. They enable you to treat functionality as a method argument.

### Syntax:
```
(parameters) -> expression
```
or
```
(parameters) -> { statements; }
```

### Examples:

#### Simple Lambda Expression
```java
// Old way (Anonymous class)
Runnable runnable1 = new Runnable() {
    @Override
    public void run() {
        System.out.println("Hello from anonymous class");
    }
};

// Lambda expression
Runnable runnable2 = () -> System.out.println("Hello from lambda");
```

#### Lambda with Parameters
```java
// Using Predicate
Predicate<String> isLongerThan5 = s -> s.length() > 5;
System.out.println(isLongerThan5.test("Hello")); // false
System.out.println(isLongerThan5.test("Hello World")); // true

// Using Function
Function<String, Integer> stringLength = s -> s.length();
System.out.println(stringLength.apply("Hello")); // 5
```

#### Lambda with Multiple Statements
```java
Consumer<String> printUpperCase = s -> {
    String result = s.toUpperCase();
    System.out.println(result);
};
printUpperCase.accept("hello"); // HELLO
```

## Creating Custom Functional Interfaces

You can create your own functional interfaces:

```java
@FunctionalInterface
interface MathOperation {
    int operate(int a, int b);
}

public class Calculator {
    public static void main(String[] args) {
        // Addition using lambda
        MathOperation addition = (a, b) -> a + b;
        
        // Subtraction using lambda
        MathOperation subtraction = (a, b) -> a - b;
        
        // Multiplication using lambda
        MathOperation multiplication = (a, b) -> a * b;
        
        // Division using lambda
        MathOperation division = (a, b) -> a / b;
        
        System.out.println("10 + 5 = " + operate(10, 5, addition));
        System.out.println("10 - 5 = " + operate(10, 5, subtraction));
        System.out.println("10 * 5 = " + operate(10, 5, multiplication));
        System.out.println("10 / 5 = " + operate(10, 5, division));
    }
    
    private static int operate(int a, int b, MathOperation mathOperation) {
        return mathOperation.operate(a, b);
    }
}
```

## Method References

Method references are a shorthand notation for lambda expressions that call a specific method. They are denoted by the double colon (`::`) operator.

### Types of Method References:
1. Reference to a static method: `ContainingClass::staticMethodName`
2. Reference to an instance method of a particular object: `containingObject::instanceMethodName`
3. Reference to an instance method of an arbitrary object of a particular type: `ContainingType::methodName`
4. Reference to a constructor: `ClassName::new`

### Examples:

```java
// Static method reference
Function<String, Integer> parseInt = Integer::parseInt;
System.out.println(parseInt.apply("5")); // 5

// Instance method reference of a particular object
String greeting = "Hello";
Supplier<Integer> lengthSupplier = greeting::length;
System.out.println(lengthSupplier.get()); // 5

// Instance method reference of an arbitrary object
Function<String, String> toUpperCase = String::toUpperCase;
System.out.println(toUpperCase.apply("hello")); // HELLO

// Constructor reference
Supplier<List<String>> listSupplier = ArrayList::new;
List<String> list = listSupplier.get(); // Creates new ArrayList
```

## Advantages of Lambda Expressions

1. **Concise code**: Less boilerplate code
2. **Increased readability**: More expressive and focused on what to do, not how to do it
3. **Support for functional programming**: Enables functional style programming
4. **Facilitate parallel processing**: Easy integration with Stream API
5. **Elimination of anonymous classes**: Simplified implementation of single-method interfaces

## Limitations of Lambda Expressions

1. Limited to functional interfaces (single abstract method)
2. Cannot modify variables from enclosing scope (must be effectively final)
3. Cannot throw checked exceptions unless declared in the functional interface
4. Cannot have instance variables or methods

## Practical Use Cases

### Sorting Collections
```java
List<String> names = Arrays.asList("John", "Alice", "Bob", "Zack");

// Sort using lambda
names.sort((s1, s2) -> s1.compareTo(s2));

// Or even more concise with method reference
names.sort(String::compareTo);
```

### Working with Streams
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

// Filter even numbers, double them, and collect
List<Integer> result = numbers.stream()
    .filter(n -> n % 2 == 0)
    .map(n -> n * 2)
    .collect(Collectors.toList());
// result: [4, 8, 12, 16, 20]

// Using method references
numbers.stream()
    .filter(n -> n > 5)
    .forEach(System.out::println);
```

### Event Handling
```java
// JavaFX button click handling
Button button = new Button("Click Me");
button.setOnAction(event -> System.out.println("Button clicked"));
```

# Default and Static Methods in Java 8 Interfaces

## Default Methods

Default methods allow interfaces to have method implementations without requiring implementing classes to define them. This was introduced in Java 8 to enable interface evolution without breaking existing implementations.

### Key Points:
- Defined with the `default` keyword
- Have a complete implementation within the interface
- Implementing classes can use the default implementation or override it
- Allow backward compatibility when adding new methods to interfaces

### Syntax:
```java
interface MyInterface {
    default void newMethod() {
        System.out.println("Default implementation");
    }
}
```

### Use Cases:

#### 1. Adding functionality to existing interfaces
```java
interface Collection<E> {
    // Existing methods...
    
    default Stream<E> stream() {
        // Implementation that creates a stream
        return StreamSupport.stream(spliterator(), false);
    }
}
```

#### 2. Optional interface methods
```java
interface Logger {
    void log(String message);
    
    default void logError(String message) {
        log("ERROR: " + message);
    }
    
    default void logWarning(String message) {
        log("WARNING: " + message);
    }
}
```

#### 3. Template Method pattern
```java
interface DataProcessor {
    void processData(String data);
    
    default void process(String data) {
        // Pre-processing
        String preprocessed = preprocess(data);
        // Core processing
        processData(preprocessed);
        // Post-processing
        postprocess();
    }
    
    default String preprocess(String data) {
        return data.trim();
    }
    
    default void postprocess() {
        System.out.println("Processing complete");
    }
}
```

## Static Methods

Static methods in interfaces are methods that belong to the interface itself, not to the implementing classes. They provide utility functions related to the interface.

### Key Points:
- Defined with the `static` keyword
- Cannot be overridden by implementing classes
- Called using the interface name, not through an instance
- Useful for providing utility methods related to the interface

### Syntax:
```java
interface MyInterface {
    static void utilityMethod() {
        System.out.println("Static utility method");
    }
}
```

### Use Cases:

#### 1. Factory methods
```java
interface List<E> {
    // Existing methods...
    
    static <E> List<E> of(E... elements) {
        // Create an immutable list containing the specified elements
        return new ImmutableList<>(elements);
    }
}
```

#### 2. Helper methods
```java
interface Comparator<T> {
    int compare(T o1, T o2);
    
    static <T> Comparator<T> naturalOrder() {
        return (T o1, T o2) -> ((Comparable<T>) o1).compareTo(o2);
    }
    
    static <T> Comparator<T> reverseOrder() {
        return (T o1, T o2) -> ((Comparable<T>) o2).compareTo(o1);
    }
}
```

#### 3. Utility functions
```java
interface StringUtils {
    static boolean isEmpty(String str) {
        return str == null || str.isEmpty();
    }
    
    static String reverse(String str) {
        return new StringBuilder(str).reverse().toString();
    }
}
```

## Multiple Inheritance Challenges

When a class implements multiple interfaces with default methods having the same signature, Java follows these rules:

1. Class methods take precedence over interface default methods
2. If there's a conflict between default methods, the implementing class must override the method

```java
interface A {
    default void method() {
        System.out.println("A's method");
    }
}

interface B {
    default void method() {
        System.out.println("B's method");
    }
}

class C implements A, B {
    // Must override the conflicting method
    @Override
    public void method() {
        // Can call specific interface's implementation if needed
        A.super.method();
        // or B.super.method();
    }
}
```

## Best Practices

1. Use default methods sparingly and primarily for backward compatibility
2. Document default methods thoroughly
3. Consider using static methods for utility functions related to the interface
4. Avoid complex logic in default methods
5. Be aware of potential conflicts when implementing multiple interfaces

## Impact on Design

- Reduces the need for utility classes
- Enables evolution of APIs without breaking existing code
- Blurs the line between interfaces and abstract classes
- Facilitates multiple inheritance of behavior
- Supports composition over inheritance through interface delegation


# Java 8 Functional Interfaces: Predicate, Function, Consumer, and Supplier

## Predicate\<T>

A functional interface that represents a predicate (boolean-valued function) of one argument.

### Core Method:
```java
boolean test(T t)
```
- Evaluates this predicate on the given argument
- Returns true if the input argument matches the predicate, otherwise false

### Additional Default Methods:

```java
default Predicate<T> and(Predicate<? super T> other)
```
- Returns a composed predicate that represents a logical AND of this predicate and another
- Short-circuits when first predicate returns false

```java
default Predicate<T> or(Predicate<? super T> other)
```
- Returns a composed predicate that represents a logical OR of this predicate and another
- Short-circuits when first predicate returns true

```java
default Predicate<T> negate()
```
- Returns a predicate that represents the logical negation of this predicate

### Static Method:
```java
static <T> Predicate<T> isEqual(Object targetRef)
```
- Returns a predicate that tests if two arguments are equal according to Objects.equals()

### Example:
```java
Predicate<Integer> isPositive = num -> num > 0;
Predicate<Integer> isEven = num -> num % 2 == 0;

// Using test method
System.out.println(isPositive.test(5));  // true
System.out.println(isEven.test(5));      // false

// Using and, or, negate
Predicate<Integer> isPositiveAndEven = isPositive.and(isEven);
System.out.println(isPositiveAndEven.test(6));  // true
System.out.println(isPositiveAndEven.test(5));  // false

Predicate<Integer> isPositiveOrEven = isPositive.or(isEven);
System.out.println(isPositiveOrEven.test(-2));  // true (even)
System.out.println(isPositiveOrEven.test(-3));  // false (neither)

Predicate<Integer> isNotPositive = isPositive.negate();
System.out.println(isNotPositive.test(-5));  // true
```

## Function\<T, R>

A functional interface that represents a function that accepts one argument and produces a result.

### Core Method:
```java
R apply(T t)
```
- Applies this function to the given argument
- Takes input of type T and returns result of type R

### Additional Default Methods:

```java
default <V> Function<T, V> andThen(Function<? super R, ? extends V> after)
```
- Returns a composed function that first applies this function and then applies the after function

```java
default <V> Function<V, R> compose(Function<? super V, ? extends T> before)
```
- Returns a composed function that first applies the before function and then applies this function

### Static Method:
```java
static <T> Function<T, T> identity()
```
- Returns a function that always returns its input argument

### Example:
```java
Function<String, Integer> strLength = str -> str.length();
Function<Integer, Integer> doubleIt = num -> num * 2;

// Using apply
System.out.println(strLength.apply("Hello"));  // 5

// Using andThen
Function<String, Integer> lengthThenDouble = strLength.andThen(doubleIt);
System.out.println(lengthThenDouble.apply("Hello"));  // 10

// Using compose
Function<String, Integer> trimThenLength = strLength.compose(String::trim);
System.out.println(trimThenLength.apply("  Hello  "));  // 5

// Using identity
Function<String, String> identityFunction = Function.identity();
System.out.println(identityFunction.apply("Hello"));  // Hello
```

## Consumer\<T>

A functional interface that represents an operation that accepts a single input argument and returns no result.

### Core Method:
```java
void accept(T t)
```
- Performs this operation on the given argument
- Takes input of type T and returns no result (void)

### Additional Default Method:
```java
default Consumer<T> andThen(Consumer<? super T> after)
```
- Returns a composed Consumer that performs this operation followed by the after operation

### Example:
```java
Consumer<String> printUpperCase = str -> System.out.println(str.toUpperCase());
Consumer<String> printLength = str -> System.out.println("Length: " + str.length());

// Using accept
printUpperCase.accept("hello");  // HELLO

// Using andThen
Consumer<String> printUpperAndLength = printUpperCase.andThen(printLength);
printUpperAndLength.accept("hello");  
// Output:
// HELLO
// Length: 5
```

## Supplier\<T>

A functional interface that represents a supplier of results. Unlike other functional interfaces, it takes no arguments.

### Core Method:
```java
T get()
```
- Gets a result
- Takes no input and returns result of type T

### Example:
```java
Supplier<Double> randomValue = () -> Math.random();
Supplier<String> currentTime = () -> new java.util.Date().toString();

// Using get
System.out.println(randomValue.get());  // Random number between 0.0 and 1.0
System.out.println(currentTime.get());  // Current date and time
```

## Combined Example Using All Four Functional Interfaces

Here's an example that uses all four functional interfaces to process a list of products:

```java
import java.util.ArrayList;
import java.util.List;
import java.util.function.Consumer;
import java.util.function.Function;
import java.util.function.Predicate;
import java.util.function.Supplier;

class Product {
    private String name;
    private double price;
    
    public Product(String name, double price) {
        this.name = name;
        this.price = price;
    }
    
    public String getName() { return name; }
    public double getPrice() { return price; }
    
    @Override
    public String toString() {
        return "Product{name='" + name + "', price=" + price + "}";
    }
}

public class FunctionalInterfacesDemo {
    public static void main(String[] args) {
        // Supplier: provides a list of products
        Supplier<List<Product>> productSupplier = () -> {
            List<Product> products = new ArrayList<>();
            products.add(new Product("Laptop", 1200.00));
            products.add(new Product("Phone", 800.00));
            products.add(new Product("Headphones", 150.00));
            products.add(new Product("Mouse", 25.00));
            products.add(new Product("Keyboard", 60.00));
            return products;
        };
        
        // Get products from supplier
        List<Product> productList = productSupplier.get();
        
        // Predicate: filters products with price greater than $100
        Predicate<Product> isPremium = product -> product.getPrice() > 100.00;
        
        // Function: transforms Product to a formatted string
        Function<Product, String> formatProduct = product -> 
            String.format("Premium Product: %s - $%.2f", 
                         product.getName(), product.getPrice());
        
        // Consumer: prints the formatted string
        Consumer<String> printInfo = System.out::println;
        
        // Process the products using all four functional interfaces
        System.out.println("Premium Products:");
        productList.stream()
            .filter(isPremium)             // Use Predicate
            .map(formatProduct)            // Use Function
            .forEach(printInfo);           // Use Consumer
        
        // Calculate total value of all products
        double totalValue = productList.stream()
            .mapToDouble(Product::getPrice)
            .sum();
        
        System.out.println("\nTotal inventory value: $" + totalValue);
    }
}
```

Output:
```
Premium Products:
Premium Product: Laptop - $1200.00
Premium Product: Phone - $800.00
Premium Product: Headphones - $150.00

Total inventory value: $2235.0
```

This example demonstrates:
- **Supplier**: Creates and supplies a list of products
- **Predicate**: Filters for premium products (price > $100)
- **Function**: Transforms Product objects into formatted strings
- **Consumer**: Prints the formatted product information



# Java 8 Stream API

The Stream API provides a functional approach to processing collections of objects. Introduced in Java 8, it enables declarative, sequential, and parallel data processing.

## Stream Basics

A stream is a sequence of elements supporting sequential and parallel aggregate operations.

```java
// Creating streams
Stream<String> streamFromCollection = Arrays.asList("a", "b", "c").stream();
Stream<String> streamFromValues = Stream.of("a", "b", "c");
Stream<Integer> infiniteStream = Stream.iterate(1, n -> n + 1);
```

## Key Characteristics
- Not a data structure
- Designed for lambdas
- Does not modify the original data source
- Lazy evaluation
- Can be traversed only once
- Supports parallel operations

## Intermediate Operations

These operations transform a stream into another stream and are lazy (not executed until a terminal operation is invoked).

### filter()
Filters elements based on a predicate.

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
List<Integer> evenNumbers = numbers.stream()
    .filter(n -> n % 2 == 0)
    .collect(Collectors.toList()); // [2, 4, 6, 8, 10]
```

### map()
Transforms each element using the provided function.

```java
List<String> names = Arrays.asList("John", "Jane", "Jack");
List<Integer> nameLengths = names.stream()
    .map(String::length)
    .collect(Collectors.toList()); // [4, 4, 4]
```

### flatMap()
Transforms each element into a stream and then flattens the streams into a single stream.

```java
List<List<Integer>> nestedList = Arrays.asList(
    Arrays.asList(1, 2, 3),
    Arrays.asList(4, 5, 6),
    Arrays.asList(7, 8, 9)
);

List<Integer> flatList = nestedList.stream()
    .flatMap(Collection::stream)
    .collect(Collectors.toList()); // [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### distinct()
Returns a stream with unique elements.

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 2, 1, 3, 4, 5);
List<Integer> distinctNumbers = numbers.stream()
    .distinct()
    .collect(Collectors.toList()); // [1, 2, 3, 4, 5]
```

### sorted()
Returns a sorted stream.

```java
List<String> names = Arrays.asList("John", "Alice", "Bob", "Zack");
List<String> sortedNames = names.stream()
    .sorted()
    .collect(Collectors.toList()); // [Alice, Bob, John, Zack]

// Custom comparator
List<String> sortedByLength = names.stream()
    .sorted(Comparator.comparing(String::length))
    .collect(Collectors.toList()); // [Bob, John, Zack, Alice]
```

### peek()
Returns a stream with the same elements after performing an action on each element (useful for debugging).

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
List<Integer> result = numbers.stream()
    .peek(n -> System.out.println("Processing: " + n))
    .map(n -> n * 2)
    .collect(Collectors.toList());
```

### limit()
Truncates the stream to contain no more than the specified number of elements.

```java
List<Integer> firstFive = Stream.iterate(1, n -> n + 1)
    .limit(5)
    .collect(Collectors.toList()); // [1, 2, 3, 4, 5]
```

### skip()
Discards the first n elements of the stream.

```java
List<Integer> numbersAfterTwo = Stream.iterate(1, n -> n + 1)
    .skip(2)
    .limit(3)
    .collect(Collectors.toList()); // [3, 4, 5]
```

## Terminal Operations

These operations produce a result or a side-effect and mark the end of the stream.

### forEach()
Performs an action for each element (similar to enhanced for-loop).

```java
List<String> names = Arrays.asList("John", "Jane", "Jack");
names.stream()
    .forEach(System.out::println);
```

### collect()
Transforms the stream into a collection or another data structure.

```java
// Collecting to List
List<String> list = Stream.of("a", "b", "c")
    .collect(Collectors.toList());

// Collecting to Set
Set<String> set = Stream.of("a", "b", "c", "a")
    .collect(Collectors.toSet());

// Collecting to Map
Map<String, Integer> map = Stream.of("apple", "banana", "cherry")
    .collect(Collectors.toMap(
        Function.identity(),  // Key is the string itself
        String::length        // Value is the length
    ));
```

### count()
Returns the count of elements in the stream.

```java
long count = Stream.of("a", "b", "c").count(); // 3
```

### anyMatch(), allMatch(), noneMatch()
Returns a boolean result based on matching elements with a predicate.

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

boolean hasEven = numbers.stream().anyMatch(n -> n % 2 == 0); // true
boolean allEven = numbers.stream().allMatch(n -> n % 2 == 0); // false
boolean noneNegative = numbers.stream().noneMatch(n -> n < 0); // true
```

### findFirst() and findAny()
Returns an Optional with the first or any element.

```java
Optional<Integer> first = Stream.of(1, 2, 3).findFirst(); // Optional[1]
Optional<Integer> any = Stream.of(1, 2, 3).findAny(); // Often Optional[1] but no guarantee
```

### reduce()
Performs a reduction operation using an identity value and an accumulation function.

```java
// Sum
int sum = Stream.of(1, 2, 3, 4, 5)
    .reduce(0, (a, b) -> a + b); // 15

// Max
Optional<Integer> max = Stream.of(1, 2, 3, 4, 5)
    .reduce(Integer::max); // Optional[5]

// String concatenation
String concatenated = Stream.of("a", "b", "c")
    .reduce("", String::concat); // "abc"
```

### min() and max()
Returns the minimum or maximum element based on a comparator.

```java
Optional<Integer> min = Stream.of(5, 3, 1, 4, 2)
    .min(Integer::compareTo); // Optional[1]

Optional<String> longestName = Stream.of("John", "Alice", "Bob")
    .max(Comparator.comparing(String::length)); // Optional[Alice]
```

### toArray()
Returns an array containing the elements of the stream.

```java
Object[] array = Stream.of("a", "b", "c").toArray();
String[] stringArray = Stream.of("a", "b", "c").toArray(String[]::new);
```

## Advanced Stream Operations

### Grouping and Partitioning

```java
class Person {
    private String name;
    private int age;
    private String country;
    
    // Constructor, getters, setters
}

List<Person> people = // initialize list

// Group by country
Map<String, List<Person>> peopleByCountry = people.stream()
    .collect(Collectors.groupingBy(Person::getCountry));

// Count people by country
Map<String, Long> countByCountry = people.stream()
    .collect(Collectors.groupingBy(
        Person::getCountry, 
        Collectors.counting()
    ));

// Partition by age (above/below 18)
Map<Boolean, List<Person>> adultVsMinor = people.stream()
    .collect(Collectors.partitioningBy(p -> p.getAge() >= 18));
```

### Numeric Streams

```java
// IntStream, LongStream, DoubleStream
IntStream intStream = IntStream.range(1, 6); // 1, 2, 3, 4, 5
LongStream longStream = LongStream.rangeClosed(1, 5); // 1, 2, 3, 4, 5

// Statistical operations
IntSummaryStatistics stats = IntStream.of(1, 2, 3, 4, 5).summaryStatistics();
System.out.println("Count: " + stats.getCount());
System.out.println("Sum: " + stats.getSum());
System.out.println("Min: " + stats.getMin());
System.out.println("Max: " + stats.getMax());
System.out.println("Average: " + stats.getAverage());
```

## Practical Examples

### Example 1: Processing Student Data
```java
class Student {
    private String name;
    private double gpa;
    private List<String> courses;
    
    // Constructor, getters, setters
}

List<Student> students = // initialize list

// Finding top students
List<Student> topStudents = students.stream()
    .filter(student -> student.getGpa() > 3.5)
    .sorted(Comparator.comparing(Student::getGpa).reversed())
    .limit(3)
    .collect(Collectors.toList());

// Finding all unique courses
Set<String> allCourses = students.stream()
    .flatMap(student -> student.getCourses().stream())
    .collect(Collectors.toSet());

// Average GPA
double averageGpa = students.stream()
    .mapToDouble(Student::getGpa)
    .average()
    .orElse(0.0);
```

### Example 2: Text Processing
```java
String text = "This is a sample text with some words repeated words";

// Word frequency count
Map<String, Long> wordFrequency = Arrays.stream(text.toLowerCase().split("\\s+"))
    .collect(Collectors.groupingBy(
        Function.identity(),
        Collectors.counting()
    ));

// Words sorted by length
List<String> wordsSortedByLength = Arrays.stream(text.split("\\s+"))
    .distinct()
    .sorted(Comparator.comparing(String::length).thenComparing(Function.identity()))
    .collect(Collectors.toList());
```

### Example 3: File Processing
```java
// Reading and processing a file
try (Stream<String> lines = Files.lines(Paths.get("data.txt"))) {
    // Count lines containing a specific word
    long count = lines
        .filter(line -> line.contains("Java"))
        .count();
} catch (IOException e) {
    e.printStackTrace();
}
```

### Example 4: Parallel Processing
```java
// Sequential processing
long start = System.currentTimeMillis();
long count = Stream.iterate(0L, i -> i + 1)
    .limit(1_000_000)
    .filter(num -> num % 2 == 0)
    .count();
System.out.println("Sequential time: " + (System.currentTimeMillis() - start) + "ms");

// Parallel processing
start = System.currentTimeMillis();
count = Stream.iterate(0L, i -> i + 1)
    .limit(1_000_000)
    .parallel()
    .filter(num -> num % 2 == 0)
    .count();
System.out.println("Parallel time: " + (System.currentTimeMillis() - start) + "ms");
```

## Best Practices

1. **Prefer method references** over lambda expressions when possible
2. **Use parallel streams carefully** - they're not always faster and can cause thread safety issues
3. **Avoid stateful operations** in parallel streams
4. **Close streams** that are backed by I/O resources
5. **Use appropriate collector** for the needed result type
6. **Consider using specialized streams** (IntStream, LongStream, DoubleStream) for primitive types
7. **Use lazy intermediate operations** before terminal operations that short-circuit


# Java 8 Date and Time API

## Problems with Legacy Date/Time Classes

The old `java.util.Date`, `java.util.Calendar`, and `java.text.SimpleDateFormat` classes had several drawbacks:

1. **Mutable and not thread-safe**: Date and Calendar objects could be modified after creation
2. **Poor API design**: Inconsistent methods and confusing month numbering (January = 0)
3. **Limited functionality**: Difficult to perform common operations like date comparisons
4. **Time zone handling issues**: Complex and error-prone time zone management
5. **No support for ISO-8601**: Standard date and time format not directly supported
6. **Performance concerns**: Calendar class was heavyweight with poor performance

```java
// Legacy date handling
Date date = new Date();  // Current date and time
Calendar calendar = Calendar.getInstance();
calendar.set(2023, Calendar.JANUARY, 15); // Note: January is 0!
Date specificDate = calendar.getTime();

// Formatting with SimpleDateFormat (not thread-safe)
SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
String formattedDate = sdf.format(date);
```

## Java 8 Date and Time API (java.time)

Java 8 introduced a new date and time API in the `java.time` package, based on the Joda-Time library, with these improvements:

1. **Immutable and thread-safe**: All classes are immutable
2. **Clear separation of concerns**: Different classes for different needs
3. **Fluent API**: Method chaining for better readability
4. **Comprehensive**: Support for various date/time concepts
5. **ISO-8601 compliant**: Follows the standard by default
6. **Better time zone handling**: First-class support for time zones

## Core Classes in java.time

### LocalDate

Represents a date without time or time zone (YYYY-MM-DD).

```java
// Creating LocalDate instances
LocalDate today = LocalDate.now();
LocalDate specificDate = LocalDate.of(2023, Month.JANUARY, 15);
LocalDate dateFromString = LocalDate.parse("2023-01-15");

// Operations
LocalDate tomorrow = today.plusDays(1);
LocalDate lastMonth = today.minusMonths(1);
LocalDate withDayOfMonth = today.withDayOfMonth(1); // First day of current month

// Information extraction
int year = today.getYear();
Month month = today.getMonth();
int day = today.getDayOfMonth();
DayOfWeek dayOfWeek = today.getDayOfWeek();
int daysInMonth = today.lengthOfMonth();
boolean isLeapYear = today.isLeapYear();

// Comparing dates
boolean isBefore = today.isBefore(tomorrow);
boolean isAfter = tomorrow.isAfter(today);
```

### LocalTime

Represents a time without date or time zone (HH:MM:SS.nanos).

```java
// Creating LocalTime instances
LocalTime now = LocalTime.now();
LocalTime specificTime = LocalTime.of(13, 30, 15); // 13:30:15
LocalTime timeFromString = LocalTime.parse("13:30:15");

// Operations
LocalTime plusHours = now.plusHours(2);
LocalTime minusMinutes = now.minusMinutes(30);
LocalTime withHour = now.withHour(10); // Sets hour to 10

// Information extraction
int hour = now.getHour();
int minute = now.getMinute();
int second = now.getSecond();
int nano = now.getNano();

// Comparing times
boolean isBefore = LocalTime.of(9, 0).isBefore(LocalTime.of(10, 0)); // true
```

### LocalDateTime

Represents both date and time without a time zone.

```java
// Creating LocalDateTime instances
LocalDateTime now = LocalDateTime.now();
LocalDateTime specificDateTime = LocalDateTime.of(2023, Month.JANUARY, 15, 13, 30, 15);
LocalDateTime fromDateAndTime = LocalDateTime.of(LocalDate.now(), LocalTime.now());
LocalDateTime parsed = LocalDateTime.parse("2023-01-15T13:30:15");

// Operations
LocalDateTime plusDays = now.plusDays(1);
LocalDateTime minusHours = now.minusHours(2);
LocalDateTime withYear = now.withYear(2024);

// Extracting components
LocalDate date = now.toLocalDate();
LocalTime time = now.toLocalTime();
```

### ZonedDateTime

Represents date and time with a time zone.

```java
// Creating ZonedDateTime instances
ZonedDateTime nowInSystemTZ = ZonedDateTime.now();
ZonedDateTime nowInParis = ZonedDateTime.now(ZoneId.of("Europe/Paris"));
ZonedDateTime specificZDT = ZonedDateTime.of(
    LocalDateTime.of(2023, Month.JANUARY, 15, 13, 30),
    ZoneId.of("America/New_York")
);

// Operations
ZonedDateTime inDifferentZone = nowInSystemTZ.withZoneSameInstant(ZoneId.of("Asia/Tokyo"));
ZonedDateTime plusWeeks = nowInSystemTZ.plusWeeks(2);

// Information
ZoneId zone = nowInSystemTZ.getZone();
ZoneOffset offset = nowInSystemTZ.getOffset();
```

### Instant

Represents a point in time (timestamp) in UTC, useful for machine time.

```java
// Creating Instant instances
Instant now = Instant.now(); // Current timestamp
Instant specificInstant = Instant.ofEpochSecond(1623851789);
Instant fromString = Instant.parse("2023-01-15T13:30:15Z");

// Operations
Instant plus5Minutes = now.plusSeconds(300);
Instant minus2Hours = now.minusSeconds(7200);

// Converting
long epochSeconds = now.getEpochSecond();
ZonedDateTime zdt = now.atZone(ZoneId.systemDefault());

// Comparing
boolean isBefore = now.isBefore(plus5Minutes);
long secondsBetween = now.until(plus5Minutes, ChronoUnit.SECONDS);
```

## Duration and Period

### Duration
Represents a time-based amount of time (seconds, nanoseconds).

```java
// Creating Duration
Duration twoHours = Duration.ofHours(2);
Duration tenMinutes = Duration.ofMinutes(10);
Duration betweenTimes = Duration.between(LocalTime.of(10, 0), LocalTime.of(12, 30));
Duration betweenInstants = Duration.between(Instant.now(), Instant.now().plusSeconds(3600));

// Operations
Duration plusDuration = twoHours.plus(tenMinutes);
Duration multiplied = twoHours.multipliedBy(3);

// Information
long seconds = twoHours.getSeconds();
boolean isNegative = twoHours.isNegative();

// Conversion
long inMinutes = twoHours.toMinutes();
```

### Period
Represents a date-based amount of time (years, months, days).

```java
// Creating Period
Period twoMonths = Period.ofMonths(2);
Period threeWeeks = Period.ofWeeks(3);
Period customPeriod = Period.of(1, 6, 15); // 1 year, 6 months, 15 days
Period betweenDates = Period.between(
    LocalDate.of(2020, 1, 1),
    LocalDate.of(2023, 6, 15)
);

// Operations
Period plusPeriod = twoMonths.plusDays(10);
Period normalized = Period.of(0, 13, 0).normalized(); // Converts to 1 year, 1 month

// Information
int years = betweenDates.getYears();
int months = betweenDates.getMonths();
int days = betweenDates.getDays();
```

## Formatting and Parsing

Java 8 introduced `DateTimeFormatter` for thread-safe formatting and parsing.

```java
// Predefined formatters
LocalDate date = LocalDate.now();
String basicIsoDate = date.format(DateTimeFormatter.BASIC_ISO_DATE); // 20230615
String isoDate = date.format(DateTimeFormatter.ISO_DATE); // 2023-06-15

// Custom formatters
DateTimeFormatter customFormatter = DateTimeFormatter.ofPattern("dd/MM/yyyy");
String formattedDate = date.format(customFormatter); // 15/06/2023
LocalDate parsedDate = LocalDate.parse("15/06/2023", customFormatter);

// Localized formatters
DateTimeFormatter localizedFormatter = 
    DateTimeFormatter.ofPattern("d MMMM yyyy").withLocale(Locale.FRENCH);
String frenchDate = date.format(localizedFormatter); // 15 juin 2023
```

## Temporal Adjusters

Provides common date operations like "first day of month" or "next Monday."

```java
LocalDate date = LocalDate.now();

// Using built-in adjusters
LocalDate firstDayOfMonth = date.with(TemporalAdjusters.firstDayOfMonth());
LocalDate lastDayOfYear = date.with(TemporalAdjusters.lastDayOfYear());
LocalDate nextMonday = date.with(TemporalAdjusters.next(DayOfWeek.MONDAY));
LocalDate previousOrSameSaturday = date.with(TemporalAdjusters.previousOrSame(DayOfWeek.SATURDAY));

// Custom adjuster
TemporalAdjuster nextWorkingDay = temporal -> {
    LocalDate ld = LocalDate.from(temporal);
    DayOfWeek dow = ld.getDayOfWeek();
    
    if (dow == DayOfWeek.FRIDAY) {
        return ld.plusDays(3); // Skip to Monday
    } else if (dow == DayOfWeek.SATURDAY) {
        return ld.plusDays(2); // Skip to Monday
    }
    return ld.plusDays(1);
};

LocalDate nextWorkDay = date.with(nextWorkingDay);
```

## Time Zones and Offsets

### ZoneId and ZoneOffset

```java
// Working with ZoneId
Set<String> allZoneIds = ZoneId.getAvailableZoneIds();
ZoneId parisZone = ZoneId.of("Europe/Paris");
ZoneId systemZone = ZoneId.systemDefault();

// Working with ZoneOffset
ZoneOffset offset = ZoneOffset.of("+05:30"); // India
ZoneOffset hoursOffset = ZoneOffset.ofHours(-5); // EST
```

### Converting Between Time Zones

```java
// Converting between time zones
LocalDateTime dateTime = LocalDateTime.now();
ZonedDateTime tokyoTime = dateTime.atZone(ZoneId.of("Asia/Tokyo"));
ZonedDateTime newYorkTime = tokyoTime.withZoneSameInstant(ZoneId.of("America/New_York"));

// Converting to/from Instant
Instant instant = tokyoTime.toInstant();
ZonedDateTime backToTokyo = instant.atZone(ZoneId.of("Asia/Tokyo"));
```

## Practical Examples

### Date/Time Calculations

```java
// Age calculation
LocalDate birthDate = LocalDate.of(1990, 5, 15);
LocalDate currentDate = LocalDate.now();
Period age = Period.between(birthDate, currentDate);
System.out.println("You are " + age.getYears() + " years, " + 
                   age.getMonths() + " months, and " + 
                   age.getDays() + " days old");

// Meeting scheduler across time zones
LocalDateTime meetingInLocalTime = LocalDateTime.of(2023, 6, 15, 10, 0); // 10 AM
ZonedDateTime meetingInNewYork = meetingInLocalTime.atZone(ZoneId.of("America/New_York"));

// What time is this in other time zones?
ZonedDateTime meetingInTokyo = meetingInNewYork.withZoneSameInstant(ZoneId.of("Asia/Tokyo"));
ZonedDateTime meetingInParis = meetingInNewYork.withZoneSameInstant(ZoneId.of("Europe/Paris"));

System.out.println("Meeting in New York: " + meetingInNewYork.format(DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm")));
System.out.println("Meeting in Tokyo: " + meetingInTokyo.format(DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm")));
System.out.println("Meeting in Paris: " + meetingInParis.format(DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm")));
```

### Time Measurement

```java
// Measuring execution time
Instant start = Instant.now();
// ... code to measure ...
Instant end = Instant.now();
Duration timeElapsed = Duration.between(start, end);
System.out.println("Time taken: " + timeElapsed.toMillis() + " milliseconds");
```

### Recurring Events

```java
// Next payment date (e.g., monthly subscription on the 15th)
LocalDate today = LocalDate.now();
LocalDate nextPaymentDate = today.withDayOfMonth(15);
if (today.getDayOfMonth() >= 15) {
    nextPaymentDate = nextPaymentDate.plusMonths(1);
}
System.out.println("Next payment on: " + nextPaymentDate);

// Every two weeks meeting
LocalDate firstMeeting = LocalDate.of(2023, 1, 10);
LocalDate upcomingMeeting = firstMeeting;
while (upcomingMeeting.isBefore(today)) {
    upcomingMeeting = upcomingMeeting.plusWeeks(2);
}
System.out.println("Next bi-weekly meeting: " + upcomingMeeting);
```

## Best Practices

1. **Use appropriate types**: Choose the right class for your needs (LocalDate for date-only, etc.)
2. **Use immutable objects**: Don't try to modify date/time objects; use the returned instances
3. **Be clear about time zones**: Always specify time zones when working with times across zones
4. **Use DateTimeFormatter for formatting**: Avoid legacy SimpleDateFormat
5. **Use java.time API consistently**: Avoid mixing with legacy date/time classes
6. **Use TemporalAdjusters for complex date operations**: They make common operations simple
7. **Be aware of DST transitions**: When working near DST transitions, be careful with calculations