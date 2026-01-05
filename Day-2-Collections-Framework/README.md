Practice Questions – Day 2 (Collections Framework)

This document contains my practice answers for Day 2, focusing on the Java Collections Framework. The questions are explained using simple language, practical reasoning, and interview-oriented explanations.

Q1. You need to store a list of customer IDs where order of insertion must be preserved and duplicate IDs are allowed.

Which Java collection would you use and why?

I would use an ArrayList. ArrayList preserves the order of insertion, meaning elements remain in the same order in which they are added. It also allows duplicate values, so the same customer ID can appear multiple times. ArrayList is efficient for read operations and is commonly used when indexing and iteration are required.

What would change if duplicates were not allowed?

If duplicates were not allowed, I would use a LinkedHashSet. LinkedHashSet does not allow duplicate values and also preserves the order of insertion. This makes it suitable when uniqueness and order are both required together.


---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Q2. In a multi-threaded application, multiple threads update a shared collection.

Why are normal collections like ArrayList or HashMap not thread-safe?

Normal collections like ArrayList and HashMap are not thread-safe because they do not handle concurrent access internally. If multiple threads modify the collection at the same time, it can lead to data inconsistency, race conditions, or runtime exceptions such as ConcurrentModificationException.

Name one thread-safe collection in Java.

One commonly used thread-safe collection is ConcurrentHashMap. It allows safe concurrent access by multiple threads without locking the entire map.

When would you prefer a Concurrent collection over Collections.synchronizedList()?

Concurrent collections are preferred in high-concurrency environments where performance is important. Collections.synchronizedList() locks the entire collection for each operation, whereas concurrent collections use fine-grained locking or non-blocking mechanisms, allowing better scalability.

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Q3. If an ArrayList is initialized with a size of 25 and a 26th element is added, what happens internally?

When the 26th element is added, the ArrayList automatically resizes its internal array. A new larger array is created, existing elements are copied into it, and then the new element is added. This resizing operation is expensive, which is why providing an appropriate initial capacity is recommended when the size is known in advance.


---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Q4. You are given a list of employee names where names may repeat and case should be treated as the same.

Input:
["John", "Alice", "john", "Bob", "Alice", "BOB"]

Task:
Remove duplicates, preserve insertion order, and print unique employee names.

To solve this problem, I use a LinkedHashMap. The key is the lowercase version of the name to handle case-insensitive comparison, and the value is the original name to preserve formatting.

Code example:

import java.util.*;

public class EmployeeNames {
    public static void main(String[] args) {

        List<String> names = Arrays.asList(
                "John", "Alice", "john", "Bob", "Alice", "BOB"
        );

        Map<String, String> uniqueNames = new LinkedHashMap<>();

        for (String name : names) {
            uniqueNames.putIfAbsent(name.toLowerCase(), name);
        }

        for (String name : uniqueNames.values()) {
            System.out.println(name);
        }
    }
}


