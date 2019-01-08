# Java Concurrency
### Creating Threads to execute tasks concurrency
* The Thread and Object classes and the Runnable interface provide the necessary support for concurrency in Java.
* The Thread class has methods such as run(), start(), and sleep() that are useful for multi-threading
* The Object class has methods such as wait() and notify() that support concurrency
```java
Thread currentThread() // return reference of the current thread
void join()
...
```
### java.util.atomic
* Khi muốn thay đổi biến trong quá trình đa luồng, chúng ta kk nên để biến dạng primitive mà nên để dạng atomic
```java
AtomicBoolean
AtomicInteger
...
```
### java.util.concurrency
The synchronizers provided in the java.util.concurrent library and their uses are
* Semaphore
* CountDownLatch
* Exchanger
* CyclicBarrier
* Phaser

