Context Switching in Go
Context switching occurs when the scheduler pauses the execution of one goroutine and starts or resumes another. This is necessary for various reasons, including when a goroutine performs a synchronous system call that might block its execution, like I/O operations, network requests, or sleep calls.


Synchronous Context Switching
Synchronous context switching occurs when a goroutine performs a blocking operation, causing the scheduler to switch to another runnable goroutine to continue execution. This type of context switching is necessary when a goroutine cannot proceed until the blocking operation is complete.

Key Points:
Blocking Operation: The goroutine explicitly waits for an operation to complete (e.g., reading a file, waiting for network response).
Scheduler Intervention: The Go scheduler intervenes to pause the blocked goroutine and switch to another ready-to-run goroutine.
Explicit Wait: The goroutine that initiated the blocking operation will not proceed until the operation is complete, causing the scheduler to manage other runnable goroutines.


How Context Switching Works Here
When Task is called, it starts by printing a message and then performs time.Sleep(2 * time.Second), which simulates a blocking operation.
The Go runtime's scheduler detects that the goroutine is blocked and performs a context switch, allowing another runnable goroutine to execute.
This way, other tasks can run while some tasks are waiting for their synchronous system call to complete, demonstrating the efficient management of blocked goroutines.


Output-
Task 1 is starting
Task 2 is starting
Task 3 is starting
Task 4 is starting
Task 5 is starting
Task 1 is done
Task 2 is done
Task 3 is done
Task 4 is done
Task 5 is done
All tasks have been processed.


This output demonstrates how Go handles context switching due to synchronous system calls, allowing multiple goroutines to run concurrently without being bottlenecked by blocking operations. 

