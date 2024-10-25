## Database Selection Scenarios & Questions:

**Scenario 1: E-commerce Order Management**

You are designing a system to manage orders for a large e-commerce platform. Each order contains customer information, ordered items, shipping address, billing address, and payment details. The system needs to handle a high volume of orders with fast read and write speeds. 

**Question:** Which database would be most suitable for storing order information in this scenario?

a) Relational Database (SQL)
b) Key-value Store (NoSQL)
c) Column-oriented Database (NoSQL)

**Answer:** a) Relational Database (SQL)

**Explanation:** Relational databases excel at handling structured data with relationships, making them ideal for e-commerce orders where relationships between customers, orders, and products are crucial. 

---

**Scenario 2: Social Media Platform**

You are developing a social media platform where users can create profiles, post updates, follow other users, and send messages. The platform needs to handle a massive amount of unstructured data, including text, images, and videos.

**Question:** Which database type is best suited for storing user posts and media content in this scenario?

a) Relational Database (SQL)
b) Document Store (NoSQL)
c) Column-oriented Database (NoSQL)

**Answer:** b) Document Store (NoSQL)

**Explanation:** Document stores excel at handling semi-structured and unstructured data, making them suitable for storing social media posts with varying data types like text, images, and videos.

---

**Scenario 3: Sensor Data Analysis**

You need to build a system that collects and analyzes data from thousands of sensors in real-time. Each sensor transmits data points like temperature, pressure, and humidity every few seconds. The system needs to perform analytical queries on historical sensor data.

**Question:** Which database technology would be most suitable for storing and analyzing time-series sensor data in this scenario?

a) Relational Database (SQL)
b) Graph Database (NoSQL)
c) Column-oriented Database (NoSQL)

**Answer:** c) Column-oriented Database (NoSQL)

**Explanation:** Column-oriented databases are optimized for handling time-series data and performing analytical queries on large datasets, making them ideal for analyzing sensor data.

---

**Scenario 4: Banking Transaction System**

You are building a system to manage transactions for a large bank. The system needs to ensure data integrity, atomicity, and consistency for every transaction. 

**Question:** Which database technology would best guarantee ACID properties for financial transactions in this scenario?

a) Relational Database (SQL)
b) Key-value Store (NoSQL)
c) Wide-column Store (NoSQL)

**Answer:** a) Relational Database (SQL) 

**Explanation:** Relational databases are built upon ACID properties (Atomicity, Consistency, Isolation, Durability), ensuring reliable and consistent data management for critical transactions.

---

**Scenario 5: Content Management System (CMS)**

You are designing a CMS for a news website. The website will have articles, authors, and categories. The system needs flexibility in content structure and should handle frequent updates and revisions.

**Question:** Which database type offers the most flexibility in handling evolving data structures and content revisions in this scenario?

a) Relational Database (SQL)
b) Document Store (NoSQL)
c) Graph Database (NoSQL)

**Answer:** b) Document Store (NoSQL)

**Explanation:** Document stores allow for flexible schemas within documents, making them suitable for content management systems where content structure might change over time. 


## SQL Practice Questions:

**Table:** **Employees**

| Column Name | Data Type |
|---|---|
| EmployeeID | INT |
| FirstName | VARCHAR(50) |
| LastName | VARCHAR(50) |
| DepartmentID | INT |
| Salary | DECIMAL(10,2) |

**Sample Data:**

| EmployeeID | FirstName | LastName | DepartmentID | Salary |
|---|---|---|---|---|
| 1 | John | Doe | 1 | 60000 |
| 2 | Jane | Smith | 2 | 75000 |
| 3 | David | Lee | 1 | 55000 |
| 4 | Sarah | Jones | 3 | 80000 |
| 5 | Michael | Brown | 2 | 70000 |


**Table:** **Departments**

| Column Name | Data Type |
|---|---|
| DepartmentID | INT |
| DepartmentName | VARCHAR(50) |

**Sample Data:**

| DepartmentID | DepartmentName |
|---|---|
| 1 | IT |
| 2 | Marketing |
| 3 | Sales |


**Questions:**

**1.** Write a SQL query to retrieve the first name, last name, and salary of all employees earning more than $65,000.

**2.** Write a SQL query to find the average salary of employees in each department. Display the department name and average salary.

**3.** Write a SQL query to list the employees who belong to the 'Marketing' department. Include their first name, last name, and department name.

**4.** Write a SQL query to find the employee with the highest salary in each department. Display the department name, employee's first name, last name, and salary.

**5.** Write a SQL query to update the salary of the employee with EmployeeID '3' to $60,000.

## SQL Practice Questions - Answers:

Here are the answers to the SQL questions, based on the provided tables and data:

**1. Retrieve employees earning more than $65,000:**

```sql
SELECT FirstName, LastName, Salary
FROM Employees
WHERE Salary > 65000;
```

**2. Average salary of employees in each department:**

```sql
SELECT d.DepartmentName, AVG(e.Salary) AS AverageSalary
FROM Employees e
JOIN Departments d ON e.DepartmentID = d.DepartmentID
GROUP BY d.DepartmentName;
```

**3. List employees in the 'Marketing' department:**

```sql
SELECT e.FirstName, e.LastName, d.DepartmentName
FROM Employees e
JOIN Departments d ON e.DepartmentID = d.DepartmentID
WHERE d.DepartmentName = 'Marketing';
```

**4. Find the highest salary in each department:**

```sql
SELECT d.DepartmentName, e.FirstName, e.LastName, e.Salary
FROM Employees e
JOIN Departments d ON e.DepartmentID = d.DepartmentID
WHERE (e.DepartmentID, e.Salary) IN (
    SELECT DepartmentID, MAX(Salary)
    FROM Employees
    GROUP BY DepartmentID
);
```

**5. Update the salary of EmployeeID '3':**

```sql
UPDATE Employees
SET Salary = 60000
WHERE EmployeeID = 3;
```

## Spring Boot MCQ Quiz (Medium to Advanced)

**Instructions:** Choose the best answer for each question.

**1. Which annotation is used to enable Spring Boot's auto-configuration mechanism?**
    a) @EnableAutoConfiguration
    b) @SpringBootApplication
    c) @Configuration
    d) @ComponentScan

**2. What is the purpose of Spring Boot Actuator?**
    a) To manage database connections.
    b) To monitor and manage Spring Boot applications.
    c) To handle RESTful API requests.
    d) To configure logging levels.

**3. How can you customize the default banner that appears when a Spring Boot application starts?**
    a) By placing a banner.txt file in the classpath.
    b) By setting the spring.banner.location property in application.properties.
    c) By implementing the Banner interface.
    d) All of the above.

**4. What is the role of @ConditionalOnProperty annotation in Spring Boot?**
    a) To inject values from properties files.
    b) To define conditional bean creation based on property values.
    c) To validate property values.
    d) To define default values for properties.

**5. Which embedded servlet container is used by Spring Boot by default?**
    a) Tomcat
    b) Jetty
    c) Undertow
    d) It depends on the project dependencies.

**6. How can you configure Spring Boot to use a different profile for a specific environment?**
    a) By setting the spring.profiles.active system property.
    b) By creating an application-{profile}.properties file.
    c) By using the @Profile annotation on configuration classes.
    d) All of the above.

**7. What is the purpose of @SpringBootTest annotation?**
    a) To run unit tests for individual components.
    b) To perform integration testing with a fully running Spring Boot application context.
    c) To mock external dependencies during testing.
    d) To define test-specific configurations.

**8. What is Spring Boot DevTools used for?**
    a) To build and package Spring Boot applications.
    b) To deploy Spring Boot applications to cloud platforms.
    c) To provide developer-friendly features like automatic restarts and live reload.
    d) To monitor performance bottlenecks in production.

**9. How can you configure Spring Boot to use a custom auto-configuration class?**
    a) By using the @EnableAutoConfiguration annotation with the "exclude" attribute.
    b) By creating a META-INF/spring.factories file and specifying the custom configuration class.
    c) By defining a bean of type AutoConfigurationImportSelector.
    d) By setting the spring.autoconfigure.exclude property in application.properties.

**10. What is the significance of the SpringApplication class in a Spring Boot application?**
    a) It is responsible for bootstrapping the Spring Boot application.
    b) It provides utility methods for accessing application properties.
    c) It manages the lifecycle of Spring beans.
    d) It handles HTTP requests and responses.

---

**Answer Key:**

1.  b) @SpringBootApplication
2.  b) To monitor and manage Spring Boot applications.
3.  d) All of the above.
4.  b) To define conditional bean creation based on property values.
5.  a) Tomcat
6.  d) All of the above.
7.  b) To perform integration testing with a fully running Spring Boot application context.
8.  c) To provide developer-friendly features like automatic restarts and live reload.
9.  b) By creating a META-INF/spring.factories file and specifying the custom configuration class.
10. a) It is responsible for bootstrapping the Spring Boot application. 


## Advanced Java MCQ Quiz (Threading, Concurrency, Lambda, and Stream)

**Instructions:** Choose the best answer for each question.

**1. Which of the following is NOT a valid way to create a new thread in Java?**
    a) Implement the Runnable interface and override the run() method.
    b) Extend the Thread class and override the run() method.
    c) Pass a lambda expression with a single parameter to the Thread constructor.
    d) Use the Callable interface with a Future object.

**2. What is the purpose of the `volatile` keyword in Java concurrency?**
    a) It ensures that a variable is only accessible from a single thread at a time.
    b) It guarantees that changes to a variable are immediately visible to all threads.
    c) It prevents deadlocks by acquiring locks in a specific order.
    d) It allows multiple threads to access a shared resource without synchronization.

**3. What is the difference between `wait()` and `sleep()` in Java?**
    a) `wait()` releases the lock on the object, while `sleep()` does not.
    b) `sleep()` throws an InterruptedException, while `wait()` does not.
    c) `wait()` can only be called within a synchronized block, while `sleep()` can be called anywhere.
    d) Both a) and c). 

**4. Which interface is used to represent a function that accepts one argument and produces a result in Java 8?**
```
```
    a) Predicate<T>
    b) Consumer<T>
    c) Supplier<T>
    d) Function<T, R>
    

**5. What is the output of the following code snippet?**

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
numbers.stream()
       .filter(n -> n % 2 == 0)
       .forEach(System.out::print);
```

    a) 12345
    b) 135
    c) 24
    d) An error will occur.

**6. What is a race condition in the context of multithreading?**
    a) A situation where two threads try to acquire the same lock at the same time.
    b) A situation where the output of a program depends on the unpredictable timing of thread execution.
    c) A situation where a thread is permanently blocked waiting for a resource held by another thread.
    d) A situation where a thread holds multiple locks, potentially leading to a deadlock.

**7. What is the difference between `ConcurrentHashMap` and `Hashtable` in Java?**
    a) `ConcurrentHashMap` provides better concurrency than `Hashtable`.
    b) `Hashtable` is synchronized at the method level, while `ConcurrentHashMap` uses fine-grained locking.
    c) `ConcurrentHashMap` allows null keys and values, while `Hashtable` does not.
    d) Both a) and b).

**8. Which of the following statements about Java Stream API is FALSE?**
    a) Streams are not data structures.
    b) Streams are pipelines that process data sequentially.
    c) Streams can be reused multiple times.
    d) Streams can leverage multi-core architectures through parallel streams. 

**9. What will happen when you try to add or remove elements from a collection while iterating over it using an iterator?**
    a) It will throw a `ConcurrentModificationException`.
    b) It will result in undefined behavior.
    c) It will successfully modify the collection.
    d) It depends on the implementation of the collection.

**10. What is the purpose of the `CompletableFuture` class in Java?**
    a) It represents the result of an asynchronous computation.
    b) It allows creating and managing thread pools.
    c) It provides methods for thread-safe operations on shared data structures.
    d) It simplifies the implementation of the Runnable interface.

---

**Answer Key:**

1.  c) Pass a lambda expression with a single parameter to the Thread constructor.
2.  b) It guarantees that changes to a variable are immediately visible to all threads.
3.  d) Both a) and c). 
4.  d) Function<T, R>
5.  c) 24
6.  b) A situation where the output of a program depends on the unpredictable timing of thread execution.
7.  d) Both a) and b).
8.  c) Streams can be reused multiple times.
9.  a) It will throw a `ConcurrentModificationException`.
10. a) It represents the result of an asynchronous computation. 



## Java Coding Challenges (Lambda, Thread, Stream)

**Instructions:** Write Java code to solve the following problems.

---

**1. Parallel Array Processing with Threads:**

**Problem:**  You have a large array of integers. You need to calculate the sum of squares of all even numbers in the array. Implement a solution that utilizes multiple threads to speed up the computation.

**Requirements:**

* Divide the array into equal chunks for each thread to process.
* Ensure proper synchronization to avoid race conditions when merging results from different threads.
*  Demonstrate how to create, start, and join threads in your solution.

**Example:**

```java
int[] numbers = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10}; 
// Expected output: sum of squares of even numbers (4 + 16 + 36 + 64 + 100) = 220 
```

---
**2.  Custom Thread-Safe Cache:**

**Problem:** Implement a simple thread-safe in-memory cache with a fixed size. The cache should use a least recently used (LRU) eviction policy. 

**Requirements:**

* Use a `ConcurrentHashMap` to store cached data.
* Utilize a `ReentrantReadWriteLock` or similar mechanism to ensure thread safety for concurrent read and write operations.
* Implement the LRU policy using a doubly linked list to keep track of element usage.

---

**3.  Process Log File with Streams:**

**Problem:** You are given a log file where each line represents a log entry with the following format: `timestamp,log_level,message`.  

**Example:** 
```
2023-10-27 10:00:00,INFO,Application started.
2023-10-27 10:00:15,DEBUG,User logged in: JohnDoe
2023-10-27 10:01:00,WARN,Low disk space warning.
2023-10-27 10:01:30,ERROR,Database connection failed.
```

**Tasks:**

1. Read the log file and create a stream of log entries.
2. Filter the stream to get only entries with the log level "ERROR".
3. Print the timestamp and message of each error log entry. 

**Bonus:** Group the error log entries by date.

---

**4.  Complex Object Transformation with Stream:**

**Problem:** You have a list of `Order` objects. Each order has a list of `OrderItem` objects. Each `OrderItem` has a `product` (String), `quantity` (int), and `price` (double). 

**Tasks:**

1. Using streams, calculate the total value of each order (sum of `quantity * price` for each `OrderItem`).
2. Create a new list containing only the orders with a total value greater than $100.

---

**5. Prime Number Generator with Lambda:**

**Problem:** Write a program that generates a list of prime numbers within a given range using lambda expressions and streams. 

**Requirements:**

* Define a functional interface that represents a predicate to test if a number is prime.
* Implement the prime number check logic within a lambda expression.
* Use the `IntStream.rangeClosed()` method and your prime number predicate to generate the list of prime numbers.

---
## Java Coding Challenges: Solutions

Here are the solutions to the previously presented coding challenges:

---

**1. Parallel Array Processing with Threads**

```java
import java.util.ArrayList;
import java.util.List;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

public class ParallelArraySum {

    public static void main(String[] args) throws InterruptedException, ExecutionException {
        int[] numbers = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
        int numThreads = 4; // You can adjust this

        ExecutorService executor = Executors.newFixedThreadPool(numThreads);
        List<Future<Integer>> futures = new ArrayList<>();

        int chunkSize = numbers.length / numThreads;
        for (int i = 0; i < numThreads; i++) {
            int start = i * chunkSize;
            int end = (i == numThreads - 1) ? numbers.length : start + chunkSize;
            futures.add(executor.submit(() -> calculateSumOfSquares(numbers, start, end)));
        }

        int totalSum = 0;
        for (Future<Integer> future : futures) {
            totalSum += future.get();
        }

        executor.shutdown();
        System.out.println("Sum of squares of even numbers: " + totalSum);
    }

    private static int calculateSumOfSquares(int[] arr, int start, int end) {
        int sum = 0;
        for (int i = start; i < end; i++) {
            if (arr[i] % 2 == 0) {
                sum += arr[i] * arr[i];
            }
        }
        return sum;
    }
}
```

**Explanation:**

1. **Divide and Conquer:** We split the input array into equal chunks and assign each chunk to a separate thread.
2. **Thread Pool:**  We use an `ExecutorService` to manage our threads efficiently.
3. **Futures:** `Future` objects allow us to retrieve the results of asynchronous computations performed by each thread.
4. **Synchronization:** The `get()` method of the `Future` interface implicitly handles thread synchronization, ensuring we wait for all threads to complete before calculating the final sum.

---

**2. Custom Thread-Safe Cache:**

```java
import java.util.HashMap;
import java.util.Map;
import java.util.concurrent.locks.ReentrantReadWriteLock;

public class LRUCache<K, V> {

    private final int capacity;
    private final Map<K, Node<K, V>> cache;
    private final Node<K, V> head;
    private final Node<K, V> tail;
    private final ReentrantReadWriteLock lock = new ReentrantReadWriteLock();

    public LRUCache(int capacity) {
        this.capacity = capacity;
        this.cache = new HashMap<>();
        this.head = new Node<>(null, null);
        this.tail = new Node<>(null, null);
        head.next = tail;
        tail.prev = head;
    }

    public V get(K key) {
        lock.readLock().lock();
        try {
            Node<K, V> node = cache.get(key);
            if (node != null) {
                moveToHead(node);
                return node.value;
            }
        } finally {
            lock.readLock().unlock();
        }
        return null;
    }

    public void put(K key, V value) {
        lock.writeLock().lock();
        try {
            Node<K, V> node = cache.get(key);
            if (node != null) {
                node.value = value;
                moveToHead(node);
            } else {
                node = new Node<>(key, value);
                cache.put(key, node);
                addToHead(node);

                if (cache.size() > capacity) {
                    Node<K, V> removed = removeTail();
                    cache.remove(removed.key);
                }
            }
        } finally {
            lock.writeLock().unlock();
        }
    }

    private void addToHead(Node<K, V> node) {
        node.next = head.next;
        node.prev = head;
        head.next.prev = node;
        head.next = node;
    }

    private void removeNode(Node<K, V> node) {
        node.prev.next = node.next;
        node.next.prev = node.prev;
    }

    private void moveToHead(Node<K, V> node) {
        removeNode(node);
        addToHead(node);
    }

    private Node<K, V> removeTail() {
        Node<K, V> removed = tail.prev;
        removeNode(removed);
        return removed;
    }

    private static class Node<K, V> {
        K key;
        V value;
        Node<K, V> prev;
        Node<K, V> next;

        Node(K key, V value) {
            this.key = key;
            this.value = value;
        }
    }
}
```

**Explanation:**

1. **Data Structures:** We use a `HashMap` to efficiently store and retrieve cached entries. A doubly linked list (`head` and `tail`) implements the LRU eviction policy.
2. **Thread Safety:** The `ReentrantReadWriteLock` allows concurrent reads while ensuring exclusive access during write operations. 
3. **LRU Implementation:**  The `addToHead`, `removeNode`, `moveToHead`, and `removeTail` methods maintain the order of elements in the linked list based on their access pattern.

---

**3.  Process Log File with Streams:**

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;
import java.util.Map;
import java.util.stream.Collectors;

public class LogFileProcessor {

    public static void main(String[] args) throws IOException {
        // Replace "your_log_file.log" with the actual path to your log file.
        String fileName = "your_log_file.log";

        // Filter for "ERROR" logs and print
        Files.lines(Paths.get(fileName))
                .filter(line -> line.contains("ERROR"))
                .forEach(System.out::println);

        // Bonus: Group by date and print
        Map<String, Long> errorsByDate = Files.lines(Paths.get(fileName))
                .filter(line -> line.contains("ERROR"))
                .collect(Collectors.groupingBy(
                        line -> line.substring(0, 10), // Extract date part
                        Collectors.counting()
                ));
        System.out.println("\nErrors by date: " + errorsByDate);
    }
}
```

**Explanation:**

1. **File Reading:** We use `Files.lines()` to efficiently read the log file line by line.
2. **Filtering:**  The `filter()` operation keeps only lines containing the "ERROR" log level. 
3. **Printing:** We use `forEach(System.out::println)` to print the filtered lines.
4. **Bonus (Grouping):**  We use `Collectors.groupingBy()` to group error logs by date and `Collectors.counting()` to count errors for each date. 

---

**4.  Complex Object Transformation with Stream:**

```java
import java.util.List;
import java.util.stream.Collectors;

class Order {
    List<OrderItem> items;
    // Constructor, getters, etc. 
}

class OrderItem {
    String product;
    int quantity;
    double price;
    // Constructor, getters, etc. 
}

public class OrderProcessor {

    public static void main(String[] args) {
        // Assuming you have a List<Order> called 'orders'
        List<Order> expensiveOrders = orders.stream()
                .filter(order -> order.getItems().stream()
                        .mapToDouble(item -> item.getQuantity() * item.getPrice())
                        .sum() > 100.00)
                .collect(Collectors.toList());

        System.out.println(expensiveOrders);
    }
}
```

**Explanation:**

1. **Nested Streams:** We use nested streams to process the `OrderItem` list within each `Order`.
2. **Mapping and Reduction:**  We use `mapToDouble` to calculate the total value of each `OrderItem` (`quantity * price`) and then `sum()` to calculate the total order value. 
3. **Filtering:**  The outer stream filters orders based on the total value calculated in the previous step. 
4. **Collection:** We collect the filtered orders into a new list.

---

**5. Prime Number Generator with Lambda:**

```java
import java.util.List;
import java.util.stream.Collectors;
import java.util.stream.IntStream;

@FunctionalInterface
interface PrimePredicate {
    boolean test(int number);
}

public class PrimeNumberGenerator {
    public static void main(String[] args) {
        // Define the range
        int start = 1;
        int end = 100;

        // Create a prime predicate using a lambda expression
        PrimePredicate isPrime = number -> {
            if (number < 2) return false;
            for (int i = 2; i <= Math.sqrt(number); i++) {
                if (number % i == 0) return false;
            }
            return true;
        };

        // Generate a list of prime numbers within the specified range
        List<Integer> primeNumbers = IntStream.rangeClosed(start, end)
                .filter(isPrime::test)    // Use the prime predicate
                .boxed()                  // Convert int to Integer
                .collect(Collectors.toList());

        // Print the generated list of prime numbers
        System.out.println("Prime numbers between " + start + " and " + end + ": " + primeNumbers);
    }
}

```

**Explanation:**

1. **Functional Interface:**  We define `isPrime` as an `IntPredicate`, which is a functional interface that takes an integer and returns a boolean. 
2. **Lambda Expression:** The prime number check logic is implemented within the lambda expression assigned to `isPrime`.
3. **IntStream:** We use `IntStream.rangeClosed` to generate a stream of integers within the specified range.
4. **Filtering and Collection:** The `filter` operation uses the `isPrime` predicate, and the results are collected into a list.

