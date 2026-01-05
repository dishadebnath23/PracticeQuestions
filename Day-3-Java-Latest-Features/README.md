Practice Questions – Day 3 (Java Latest Features)

This document contains my practice answers for Day 3, focusing on some of the latest and commonly used Java features such as generics, records, functional interfaces, lambda expressions, and streams. The explanations are kept simple and aligned with interview expectations.

Q1. You are writing a utility method that processes a collection of numeric values.

How would you restrict the generic type to only numbers?

To restrict a generic type to only numeric values, I would use bounded generics with the Number class. This ensures that the method accepts only numeric data types like Integer, Double, or Float and prevents non-numeric types at compile time.

Example:
class Utility {
    public <T extends Number> void process(List<T> values) {
        // processing logic
    }
}

Explain when to use <? extends Number> vs <? super Integer>.

<? extends Number> is used when we only want to read values from a collection. It allows flexibility because the collection can contain any subclass of Number, such as Integer or Double.

<? super Integer> is used when we want to add Integer values into a collection. The collection can be of type Integer, Number, or Object.

A simple rule is:
extends is used for reading
super is used for writing

Give one practical use case for each.

<? extends Number> can be used when calculating the sum or average from a list of numeric values.

<? super Integer> can be used when adding integer values into a collection that accepts integers or their parent types.


--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Q2. Java introduced records to simplify data-carrying classes.

What problems do records solve compared to traditional POJOs?

Records remove a lot of boilerplate code that is usually written in POJOs, such as constructors, getters, equals(), hashCode(), and toString() methods. They provide a concise way to create immutable data classes and improve code readability and maintainability.

When would you not use a record?

Records should not be used when the class needs to be mutable, when complex business logic is required, or when inheritance from another class is needed. Records are best suited for simple data holder classes.


--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Q3. What is a functional interface?

A functional interface is an interface that contains exactly one abstract method. It is mainly used to support lambda expressions in Java.

Name two built-in functional interfaces.

Two commonly used built-in functional interfaces are Predicate and Function.

Show how a lambda expression improves readability compared to an anonymous class.

Using anonymous class:
Runnable r = new Runnable() {
    public void run() {
        System.out.println("Running");
    }
};

Using lambda expression:
Runnable r = () -> System.out.println("Running");

The lambda expression is shorter, cleaner, and easier to understand compared to the anonymous class.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Q4. What is a Stream in Java?

A Stream represents a sequence of elements that allows functional-style operations such as filtering, mapping, and reducing.

How is it different from a collection?

A collection is used to store data, whereas a stream is used to process data. Streams do not store elements and do not modify the original collection.

Explain the difference between intermediate and terminal operations.

Intermediate operations return a stream and are lazy in nature. Examples include filter() and map().

Terminal operations produce a result or side effect and trigger the execution of the stream. Examples include forEach(), collect(), and count().

Why are streams considered lazy?

Streams are considered lazy because intermediate operations are not executed until a terminal operation is invoked. This improves performance by avoiding unnecessary processing.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Q5. Given a list of employee objects.

Which stream operation would you use to filter employees by department?

The filter() operation is used to select employees belonging to a specific department.

employees.stream()
         .filter(e -> e.getDepartment().equals("IT"));

How would you transform employee names to uppercase?

The map() operation is used to transform employee names to uppercase.

employees.stream()
         .map(e -> e.getName().toUpperCase());

Which collector would you use to group employees by department?

Collectors.groupingBy() is used to group employees based on their department.

employees.stream()
         .collect(Collectors.groupingBy(Employee::getDepartment));
