# Back to basic about multithread, parallelism ...
## Coroutine
 Combine from Co (co-working) and routine (functions), so coroutine is function that are cooperative.
### How are functions non-cooperative?
let see a code:
```c#
void PrintSomething(){
    Console.WriteLine(Hello());
}
string Hello(){
    return "1";
}
```
so, when a function calls (`PrintSomething`) a second function (`Hello`), the first cannot continue until the second function finishes and returns to where it was called. The control remains with the second function until it executes completely and only then can the control return to the first one.
### How can functions cooperate with one another?
Coroutines are functions where the control is transferred from one function to the other function in a way that the `exit point` from the first function and the entry point to the second function are `remembered` – without `changing the context`. Thus, each function remembers where it left the execution and where it should resume from.

assuming code:
```c#
void PrintSomething(){
    Console.WriteLine(Hello());
    ResumeHello();
}
string Hello(){
    return "1";
    ResumePrintSomething();
}
```
they remember the `exit  point` at here is `Resume xx` and can switch easily.

Using this concept, you can pass around values between functions in the middle of the execution without breaking away the context of each function.
Coroutines are cheaper than threads and hence, enable us to execute concurrent code without much effort.

Coroutine in some programing have each different implemented.

deep learn about coroutine: https://blog.panicsoftware.com/coroutines-introduction/
https://crystal-lang.org/reference/guides/concurrency.html

https://medium.com/@unmeshvjoshi/how-java-thread-maps-to-os-thread-e280a9fb2e06

## Yield
In computer science, yield is an action that occurs in a computer program during multithreading, of forcing a processor to relinquish control of the current running thread, and sending it to the end of the running queue, of the same scheduling priority.


