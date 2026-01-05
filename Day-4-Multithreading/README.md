Practice Questions – Day 4 (Multithreading)

This document contains my practice answers for Day 4, focusing on Java multithreading concepts such as thread creation, synchronization, ExecutorService, thread safety, and deadlocks. The explanations are written in simple language and aligned with interview expectations.

Q1. What is the difference between creating a thread using Thread, Runnable, and ExecutorService?

Creating a thread by extending the Thread class means the class itself represents a thread. This approach is simple but limits flexibility because Java does not support multiple inheritance.

Creating a thread using Runnable involves implementing the Runnable interface and passing it to a Thread object. This is preferred over extending Thread because it separates the task from the thread and allows the class to extend another class if needed.

ExecutorService is a higher-level framework used to manage threads. Instead of manually creating and starting threads, we submit tasks to the executor, which handles thread creation, reuse, and scheduling internally.

Which approach is preferred in real applications and why?

In real applications, ExecutorService is preferred because it provides better control over thread management, improves performance using thread pools, and reduces the complexity of handling threads manually.

What problems does ExecutorService solve compared to manual thread creation?

ExecutorService solves problems such as excessive thread creation, poor resource management, and lack of scalability. It reuses threads, manages task queues, and provides better error handling.

Q2. You submit a task using ExecutorService.submit().

What does the submit() method return?

The submit() method returns a Future object, which represents the result of the asynchronous computation.

How do you retrieve the result of the task?

The result of the task can be retrieved by calling the get() method on the Future object.

What happens if Future.get() is called before the task is complete?

If get() is called before the task completes, the calling thread is blocked until the task finishes and the result becomes available.

Q3. Why is synchronization required in multi-threaded programs?

Synchronization is required to control access to shared resources. It ensures that only one thread can execute a critical section at a time, preventing data inconsistency and race conditions.

Explain the purpose of wait() and notify() with an example.

The wait() method causes the current thread to release the lock and wait until another thread calls notify() or notifyAll() on the same object.

The notify() method wakes up one waiting thread so it can continue execution.

Example:

class SharedResource {
    synchronized void produce() throws InterruptedException {
        wait();
        System.out.println("Resumed production");
    }

    synchronized void consume() {
        notify();
        System.out.println("Consumption done");
    }
}

Why must wait() and notify() be called inside a synchronized block?

wait() and notify() must be called inside a synchronized block because they operate on the object's monitor. Calling them without holding the lock results in an IllegalMonitorStateException.

Q4. Why are collections like ArrayList and HashMap not thread-safe?

ArrayList and HashMap are not thread-safe because they do not handle concurrent access internally. If multiple threads modify them simultaneously, it can lead to data inconsistency, race conditions, or runtime exceptions such as ConcurrentModificationException.

Name one thread-safe collection.

One thread-safe collection is ConcurrentHashMap.

When would you prefer ConcurrentHashMap over Collections.synchronizedMap()?

ConcurrentHashMap is preferred in high-concurrency environments because it uses fine-grained locking and allows multiple threads to read and write concurrently. Collections.synchronizedMap() locks the entire map, which reduces performance.

Q5. What is a deadlock in Java?

A deadlock is a situation where two or more threads are waiting for each other to release resources, causing the program to stop executing.

Explain a real-world scenario where a deadlock can occur.

A real-world example is two people holding different resources and waiting for each other to release them, such as one person holding a pen and waiting for paper, while the other holds paper and waits for the pen.

Show a piece of code where a deadlock can potentially occur.

class DeadlockExample {
    static final Object lock1 = new Object();
    static final Object lock2 = new Object();

    public static void main(String[] args) {

        Thread t1 = new Thread(() -> {
            synchronized (lock1) {
                synchronized (lock2) {
                    System.out.println("Thread 1 acquired both locks");
                }
            }
        });

        Thread t2 = new Thread(() -> {
            synchronized (lock2) {
                synchronized (lock1) {
                    System.out.println("Thread 2 acquired both locks");
                }
            }
        });

        t1.start();
        t2.start();
    }
}

Mention one way to prevent deadlocks in applications.

One way to prevent deadlocks is to always acquire locks in a fixed order. This avoids circular waiting between threads.
