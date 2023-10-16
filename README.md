# JavaSE-Predicate

In Java, Predicate is a functional interface from the java.util.function package. 

It represents a predicate, which is a boolean-valued function that takes an argument and returns true or false.

Here's the basic structure of the Predicate interface:

```java
@FunctionalInterface
public interface Predicate<T> {
    boolean test(T t);
}
```

The test method is the key method in the Predicate interface. It takes an argument of type T and returns a boolean.

Let me show you an example to make it clearer. Suppose you have a list of integers, and you want to filter out the even numbers. You can use a Predicate for this:

```java
import java.util.Arrays;
import java.util.List;
import java.util.function.Predicate;

public class PredicateExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

        // Define a Predicate to test if a number is even
        Predicate<Integer> isEven = number -> number % 2 == 0;

        // Use the Predicate to filter the list
        numbers.removeIf(isEven);

        // Print the filtered list
        System.out.println("Odd numbers: " + numbers);
    }
}
```

In this example, the isEven predicate tests whether a given number is even. 

The removeIf method is then used to remove all elements that satisfy the condition specified by the predicate. 

The result is a list containing only odd numbers.

# More predicate samples in Java

## Example 1: Filtering Strings

```java
import java.util.Arrays;
import java.util.List;
import java.util.function.Predicate;

public class StringPredicateExample {
    public static void main(String[] args) {
        List<String> words = Arrays.asList("apple", "banana", "orange", "grape", "kiwi");

        // Define a Predicate to test if a word starts with "a"
        Predicate<String> startsWithA = word -> word.startsWith("a");

        // Use the Predicate to filter the list
        words.removeIf(startsWithA);

        // Print the filtered list
        System.out.println("Words not starting with 'a': " + words);
    }
}
```

## Example 2: Filtering Objects

```java
import java.util.Arrays;
import java.util.List;
import java.util.function.Predicate;

class Person {
    String name;
    int age;

    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

public class ObjectPredicateExample {
    public static void main(String[] args) {
        List<Person> people = Arrays.asList(
                new Person("Alice", 25),
                new Person("Bob", 30),
                new Person("Charlie", 22),
                new Person("David", 35)
        );

        // Define a Predicate to test if a person is older than 25
        Predicate<Person> isOlderThan25 = person -> person.age > 25;

        // Use the Predicate to filter the list
        people.removeIf(isOlderThan25);

        // Print the filtered list
        System.out.println("People younger than 25: " + people);
    }
}
```

## Example 3: Combining Predicates

```java
import java.util.Arrays;
import java.util.List;
import java.util.function.Predicate;

public class CombinedPredicateExample {
    public static void main(String[] args) {
        List<String> words = Arrays.asList("apple", "banana", "orange", "grape", "kiwi");

        // Define Predicates
        Predicate<String> startsWithA = word -> word.startsWith("a");
        Predicate<String> endsWithE = word -> word.endsWith("e");

        // Combine Predicates using logical AND
        Predicate<String> startsAndEndsWith = startsWithA.and(endsWithE);

        // Use the combined Predicate to filter the list
        words.removeIf(startsAndEndsWith);

        // Print the filtered list
        System.out.println("Words not starting with 'a' and ending with 'e': " + words);
    }
}
```

These examples demonstrate different use cases of Predicate in filtering lists and objects based on certain conditions. If you have any specific scenarios or questions, feel free to ask!

# More advance topics about predicate in Java

Let's delve into some more advanced topics related to the Predicate interface in Java.

## 1. Negating a Predicate:
You can negate a predicate using the negate method. This means creating a new predicate that is the opposite of the original one.

```java
import java.util.function.Predicate;

public class NegatePredicateExample {
    public static void main(String[] args) {
        Predicate<String> startsWithA = s -> s.startsWith("A");
        Predicate<String> doesNotStartWithA = startsWithA.negate();

        System.out.println(startsWithA.test("Apple"));  // true
        System.out.println(doesNotStartWithA.test("Apple"));  // false
    }
}
```

## 2. Or and And Operations:
You can combine predicates using or and and methods. For example, you might want to filter elements that satisfy either one condition or another.

```java
import java.util.function.Predicate;

public class OrAndPredicateExample {
    public static void main(String[] args) {
        Predicate<String> startsWithA = s -> s.startsWith("A");
        Predicate<String> endsWithE = s -> s.endsWith("e");

        Predicate<String> startsOrEndsWith = startsWithA.or(endsWithE);
        Predicate<String> startsAndEndsWith = startsWithA.and(endsWithE);

        System.out.println(startsOrEndsWith.test("Apple"));  // true
        System.out.println(startsAndEndsWith.test("Apple"));  // false
    }
}
```

## 3. Chaining Predicates:
You can chain multiple predicates together to create a more complex condition. The and, or, and negate methods allow you to build up sophisticated logic.

```java
import java.util.function.Predicate;

public class ChainingPredicatesExample {
    public static void main(String[] args) {
        Predicate<String> lengthIsGreaterThan5 = s -> s.length() > 5;
        Predicate<String> startsWithA = s -> s.startsWith("A");
        Predicate<String> complexCondition = lengthIsGreaterThan5.and(startsWithA).negate();

        System.out.println(complexCondition.test("Apple"));  // false
        System.out.println(complexCondition.test("Orange")); // true
    }
}
```

## 4. Using Method References:
You can also use method references with predicates, which can make your code more concise.

```java
import java.util.function.Predicate;

public class MethodReferencePredicateExample {
    public static void main(String[] args) {
        // Using lambda expression
        Predicate<String> startsWithA1 = s -> s.startsWith("A");

        // Using method reference
        Predicate<String> startsWithA2 = "Apple"::startsWith;

        System.out.println(startsWithA1.test("Apple"));  // true
        System.out.println(startsWithA2.test("Apple"));  // true
    }
}
```

These advanced topics showcase the flexibility and power of the Predicate interface in Java, allowing you to build complex conditions and make your code more expressive. 
