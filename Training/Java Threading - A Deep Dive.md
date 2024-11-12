---
Created by: Shudipto Trafder
Created time: 2024-11-12T17:50:00
Last edited by: Shudipto Trafder
Last edited time: 2024-11-12T17:54:00
tags:
  - java
---


### I. Introduction: Refreshing the Basics

#### 1. What are Threads?

* **Definition:** Threads are independent paths of execution within a program. They allow a program to perform multiple tasks concurrently, enhancing responsiveness and resource utilization.
* **Benefits:**
    * **Responsiveness:** Threads prevent UI freezes by allowing long tasks to run in the background.
    * **Resource Utilization:** Threads efficiently use CPU cycles, especially on multi-core processors.
    * **Scalability:**  Threads improve the performance of applications handling multiple users or requests.
* **Analogy:** Imagine a chef (program) preparing a meal. Using threads is like having multiple cooks working simultaneously on different tasks (chopping vegetables, boiling water, etc.), resulting in a faster and more efficient meal preparation.

#### 2. Creating and Starting Threads in Java

**2.1. Extending the `Thread` class:**

```java
public class MyThread extends Thread {
    @Override
    public void run() {
        System.out.println("Thread " + Thread.currentThread().getName() + " is running.");
    }

    public static void main(String[] args) {
        MyThread thread1 = new MyThread();
        thread1.setName("Thread-1");
        thread1.start(); 
    }
}
```
* **Explanation:**
    * We create a class `MyThread` that inherits from the `Thread` class.
    * We override the `run()` method, which contains the code we want our thread to execute.
    * We create an instance of `MyThread`.
    * We use `thread1.start()` to start the thread. This internally calls the `run()` method.

**2.2. Implementing the `Runnable` interface:**

```java
public class MyRunnable implements Runnable {
    @Override
    public void run() {
        System.out.println("Thread " + Thread.currentThread().getName() + " is running.");
    }

    public static void main(String[] args) {
        MyRunnable runnable = new MyRunnable();
        Thread thread2 = new Thread(runnable);
        thread2.setName("Thread-2");
        thread2.start();
    }
}
```

* **Explanation:**
    * We create a class `MyRunnable` that implements the `Runnable` interface.
    * We again override the `run()` method with our thread's logic.
    * We create an instance of `MyRunnable`.
    * We create a new `Thread` object, passing the `runnable` instance to its constructor.
    * We start the thread using `thread2.start()`, which calls the `run()` method of our `MyRunnable` object.

**2.3. Comparing and Contrasting:**

* **Extending `Thread`:**
    * Simpler for basic scenarios.
    * Limits flexibility as the class cannot extend other classes.
* **Implementing `Runnable`:**
    * More flexible, allowing classes to inherit from other classes.
    * Preferred approach in most cases.

**2.4. Essential `Thread` class methods:**

* `start()`: Initiates the execution of the thread, calling the `run()` method.
* `run()`: Contains the code that the thread will execute.
* `sleep(milliseconds)`: Pauses the current thread for a specified duration.
* `join()`: Waits for the thread to complete its execution before continuing with the main thread.

```java
public class MyRunnable2 implements Runnable {
    private static int counter = 0; // Shared resource

    @Override
    public void run() {
        for (int i = 0; i < 10000; i++) {
            counter++; // Incrementing the shared counter
        }
    }

    public static void main(String[] args) throws InterruptedException {
        MyRunnable runnable = new MyRunnable();
        Thread thread1 = new Thread(runnable, "Thread-1");
        Thread thread2 = new Thread(runnable, "Thread-2");

        thread1.start();
        thread2.start();

        thread1.join(); // Wait for thread1 to finish
        thread2.join(); // Wait for thread2 to finish

        System.out.println("Final Counter Value: " + counter); 
    }
}
```

### II. Thread Synchronization and Communication

**1. The Problem of Shared Resources**

* **Race Conditions:** Occur when multiple threads access and modify shared data concurrently, leading to unpredictable and incorrect results.

* **Example:** Imagine a simple counter incremented by multiple threads. 

```java
public class Counter {
    private int count = 0;

    public void increment() {
        count++; 
    }

    public int getCount() {
        return count;
    }
}
```

If multiple threads call `increment()` simultaneously, the final `count` value might be incorrect due to race conditions (e.g., two threads reading the same value before incrementing).

**2. Synchronization Tools**

**2.1. The `synchronized` Keyword**

* **Intrinsic Locks:** Every Java object has an intrinsic lock. Using `synchronized`, we can ensure that only one thread can acquire this lock at a time.

    * **Synchronized Methods:**
    ```java
    public class Counter { // ... previous code ...
        public synchronized void increment() {
            count++;
        }
    }
    ```
    - The `synchronized` keyword on the `increment()` method makes it atomic. Only one thread can enter this method at a time, preventing race conditions.

    * **Synchronized Blocks:**
    ```java
    public class Counter { // ... previous code ...
        public void increment() {
            synchronized (this) { 
                count++; 
            }
        }
    }
    ```
    - We can synchronize a specific block of code using `synchronized (object) {}`.  Here, `this` refers to the current `Counter` object's lock.

**2.2. Locks from `java.util.concurrent.locks` Package**

* **`ReentrantLock`:** Provides more flexible locking mechanisms compared to `synchronized`.

    ```java
    import java.util.concurrent.locks.ReentrantLock;

    public class Counter { // ... previous code ...
        private final ReentrantLock lock = new ReentrantLock();

        public void increment() {
            lock.lock(); 
            try {
                count++;
            } finally {
                lock.unlock(); 
            }
        }
    }
    ```
    - We explicitly acquire the `lock` before the critical section and release it in a `finally` block to guarantee release even if exceptions occur.

* **`ReadWriteLock`:** Optimizes for scenarios where reads are more frequent than writes.

    ```java
    import java.util.concurrent.locks.ReadWriteLock;
    import java.util.concurrent.locks.ReentrantReadWriteLock;

    // ... (similar to ReentrantLock example)
    private final ReadWriteLock rwLock = new ReentrantReadWriteLock();

    public int getCount() {
        rwLock.readLock().lock();
        try {
            return count;
        } finally {
            rwLock.readLock().unlock();
        }
    } 
    ```
    - Multiple threads can acquire the read lock simultaneously, but only one thread can acquire the write lock at a time.


**3. Inter-Thread Communication**

**3.1. `wait()`, `notify()`, and `notifyAll()`**

* **Producer-Consumer Problem:**  A classic example where one or more threads (producers) generate data and put it into a buffer, and other threads (consumers) retrieve and process that data.

```java
public class ProducerConsumer {
    private final Object lock = new Object();
    private final List<Integer> buffer = new ArrayList<>();
    private final int bufferSize = 10;

    public void produce(int value) throws InterruptedException {
        synchronized (lock) {
            while (buffer.size() == bufferSize) { 
                lock.wait(); 
            }
            buffer.add(value);
            lock.notifyAll();
        }
    }

    public int consume() throws InterruptedException {
        synchronized (lock) {
            while (buffer.isEmpty()) {
                lock.wait();
            }
            int value = buffer.remove(0);
            lock.notifyAll();
            return value;
        }
    }
}
```

* **Explanation:**
    - `wait()`:  The producer thread waits if the buffer is full, and the consumer thread waits if the buffer is empty.
    - `notifyAll()`:  Notifies all waiting threads on the lock. The waiting threads then compete to acquire the lock.

**3.2. Condition Objects**

* Provide more fine-grained waiting and signaling mechanisms than `wait()` and `notify()`

```java
import java.util.concurrent.locks.Condition;
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

// ... (Similar structure to the previous ProducerConsumer example)

public class ProducerConsumer {
    private final Lock lock = new ReentrantLock();
    private final Condition notFull = lock.newCondition();
    private final Condition notEmpty = lock.newCondition();
    // ... (rest of the code) 

    public void produce(int value) throws InterruptedException {
        lock.lock();
        try {
            while (buffer.size() == bufferSize) {
                notFull.await(); // Wait for notFull condition
            }
            buffer.add(value);
            notEmpty.signalAll(); // Signal notEmpty condition
        } finally {
            lock.unlock();
        }
    }

    // ... (consume() method will be similar, using notEmpty.await() and notFull.signalAll()) 
}
```

* **Explanation:**
    - We create two `Condition` objects: `notFull` and `notEmpty`.
    - The producer waits on `notFull` if the buffer is full and signals `notEmpty` when it adds an item.
    - The consumer waits on `notEmpty` if the buffer is empty and signals `notFull` when it removes an item.


### III. Advanced Concurrency Concepts

Now that we understand how to synchronize and coordinate threads, let's dive into more advanced concurrency concepts provided by Java.

Thread vs Thread Pools:
**Thread:** Imagine a lone worker in a factory. You give them a task (like sewing a shirt), they do it, and then they clock out. Simple, right? But what if you have a LOT of shirts?  You'd spend all day just hiring and saying goodbye 👋

**Thread Pool:** Now imagine a room FULL of workers, ready to go. You throw a shirt in, someone grabs it, sews it, and gets ready for the next one. No more hiring delays!  🎉

**Here's the breakdown:**

**Threads:**

* **Pros:** Simple for small tasks.
* **Cons:** Creating and destroying them is slow. Overuse can hog resources.

**Thread Pools:**

* **Pros:** Efficient for many tasks. Reuses threads, saving time and resources.
* **Cons:**  Slightly more complex to set up initially.

**In a nutshell:** Use threads for quick, one-off jobs. Use thread pools when you've got a lot on your plate and need things running smoothly. 🚀 



**1. Thread Pools**

* **Motivation:**  Creating and destroying threads repeatedly is resource-intensive. Thread pools provide a solution by reusing a fixed number of threads for multiple tasks.
* **Benefits:**
    * Reduced thread creation overhead.
    * Efficient resource management.
    * Control over the maximum number of concurrent threads.
* **Using `ExecutorService` and `Executors`:**

```java
import java.util.concurrent.*;

public class ThreadPoolExample {
    public static void main(String[] args) {
        // Create a thread pool with a fixed number of threads 
        ExecutorService executor = Executors.newFixedThreadPool(5); 

        // Submit multiple tasks to the thread pool
        for (int i = 0; i < 10; i++) {
            Runnable task = new Task("Task " + i);
            executor.execute(task); 
        }

        // Shut down the executor (gracefully)
        executor.shutdown(); 
    }
}

class Task implements Runnable {
    private final String name;

    public Task(String name) {
        this.name = name;
    }

    @Override
    public void run() {
        System.out.println("Executing " + name + " on thread: " + Thread.currentThread().getName());
        // ... Task logic ... 
    }
}
```

* **Explanation:**
    * We create a thread pool using `Executors.newFixedThreadPool(5)`, which creates a pool with 5 threads.
    * `execute(Runnable task)` submits tasks to the pool. The pool manages thread allocation and execution.
    * `executor.shutdown()` initiates a graceful shutdown of the pool after all submitted tasks are completed. 

**2. The `volatile` Keyword**

* **Visibility Problem:** Changes made to variables by one thread might not be immediately visible to other threads due to caching mechanisms.
* **`volatile` to the Rescue:**  The `volatile` keyword ensures that a variable is read directly from main memory and written directly back to main memory, bypassing cache inconsistencies.

```java
public class VolatileExample {
    private volatile boolean flag = false;

    public void setFlag(boolean value) {
        this.flag = value;
    }

    public boolean getFlag() {
        return flag;
    }
}
```

* **Usage:** Useful for simple state flags shared between threads, where atomicity is not the primary concern.
* **Note:**  `volatile` does not provide mutual exclusion (like locks) and should not be used for complex operations that need atomicity.

**3. Atomic Variables (`java.util.concurrent.atomic`)**

* **Atomic Operations:**  Provide lock-free, thread-safe operations on single variables.
* **Example:** `AtomicInteger`

```java
import java.util.concurrent.atomic.AtomicInteger;

public class AtomicCounter {
    private AtomicInteger count = new AtomicInteger(0);

    public void increment() {
        count.incrementAndGet(); 
    }

    // ... other methods like get(), decrementAndGet(), etc.
}
```

* **Benefits:** Faster than synchronization mechanisms in certain cases (low contention), offering better performance for simple operations.

**4. Concurrent Collections**

* **Thread-Safe Data Structures:** Designed for concurrent access, providing thread-safety without explicit locking.
* **Examples:**
    * `ConcurrentHashMap`: A thread-safe map that allows concurrent reads and updates.
    * `ConcurrentLinkedQueue`:  A thread-safe, non-blocking queue.
* **Benefits:** Significantly improved performance in concurrent environments compared to synchronizing traditional collections.

**5. Fork/Join Framework (`java.util.concurrent.ForkJoinPool`)**

* **Divide and Conquer:** Designed for efficiently executing recursive tasks that can be broken down into smaller subtasks.
* **Work-Stealing Algorithm:**  Efficiently balances the workload among multiple threads.

```java
import java.util.concurrent.ForkJoinPool;
import java.util.concurrent.RecursiveTask;

public class RecursiveSum extends RecursiveTask<Long> {
    // ... 
    
    @Override
    protected Long compute() {
        if (/* problem is small enough */) {
            // Compute the result directly
        } else {
            // Divide the problem into subtasks
            RecursiveSum subtask1 = new RecursiveSum(/* ... */);
            RecursiveSum subtask2 = new RecursiveSum(/* ... */);

            // Fork the subtasks
            subtask1.fork(); 
            subtask2.fork();

            // Join the results of the subtasks
            return subtask1.join() + subtask2.join();
        }
    }
}
```

* **Benefits:** Highly efficient for parallel processing of tasks that can be effectively broken down recursively.

**6. Deadlocks**
* **Definition:** A situation where two or more threads are blocked forever, each waiting for the other to release the resource that it needs.
* **Conditions for Deadlock:**
    1. Mutual Exclusion
    2. Hold and Wait
    3. No Preemption
    4. Circular Wait
* **Strategies:**
    * **Prevention:** Design to avoid one or more of the deadlock conditions (e.g., acquire locks in a consistent order).
    * **Avoidance:**  Use algorithms to detect potential deadlocks before they happen (e.g., Banker's algorithm).
    * **Detection and Recovery:**  Detect deadlocks when they occur and implement recovery mechanisms (e.g., thread termination).


### IV. Practical Considerations and Tools

This section focuses on the practical aspects of working with threads in Java, including design principles, debugging tools, and common patterns.

**1. Thread Safety and Immutability**

* **Thread Safety:**  A class or method is thread-safe if it behaves correctly when accessed concurrently by multiple threads. 

    * **Strategies:**
        -  **Confinement:** Limiting access to shared data (e.g., using local variables).
        -  **Immutability:** Making shared objects immutable (unchangeable) after creation. 
        -  **Synchronization:**  Using locks (`synchronized`, `ReentrantLock`, etc.) to protect shared data.
        -  **Thread-Safe Data Structures:** Utilizing concurrent collections like `ConcurrentHashMap`.

* **Immutability:**

    * An immutable object cannot be modified after creation, inherently making it thread-safe.
    * **Example:**
       ```java
       public final class ImmutableData { 
            private final String name;
            private final int id;

            public ImmutableData(String name, int id) {
                this.name = name;
                this.id = id;
            }

            // Only getter methods; no setters
            public String getName() { 
                return name;
            }

            public int getId() { 
                return id;
            }
        }
       ```
    * **Benefits:**  Simplifies concurrency, eliminates the need for defensive copying, and makes code easier to reason about. 

**2. Thread Debugging and Profiling**
* **Challenges:** Concurrency bugs can be difficult to reproduce and debug due to their non-deterministic nature.
* **Tools and Techniques:**
    * **Debugger Breakpoints:** Set conditional breakpoints in your IDE to pause execution when specific threads reach certain points.
    * **Logging:**  Add logging statements to your code to track thread execution and data flow. Use a thread-safe logging framework like Log4j or SLF4j.
    * **Profiling Tools:** Use profilers like JProfiler, YourKit, or VisualVM to monitor thread activity, identify bottlenecks, and analyze performance.
    * **Stress Testing:** Subject your application to high load and concurrent access to uncover hidden concurrency issues.

**3. Common Threading Patterns**
* **Worker Thread Pattern:**
    * Create a fixed number of worker threads in a thread pool.
    * Threads wait in a queue for tasks to arrive.
    * When a task is available, a worker thread takes it from the queue and processes it.
    * Efficient for handling a large number of short-lived tasks. 

* **Thread-Per-Request Pattern:**
    * Create a new thread for each incoming request.
    * Simple to implement, but can be inefficient for a large number of requests due to thread creation overhead.

* **Producer-Consumer Pattern (Covered in Detail in Part II):**
    * Useful for scenarios where one or more threads produce data and others consume it, allowing for asynchronous processing and buffering.

* **Other Patterns:**  Many other threading patterns exist, each suited for specific scenarios. Explore them as you encounter different concurrency challenges.

**Key Takeaways:**
* Designing for thread safety is crucial. Favor immutability, confinement, and understand when to apply synchronization.
* Leverage debugging and profiling tools to diagnose and resolve concurrency issues.
* Familiarize yourself with common threading patterns to solve recurring concurrency problems effectively.
