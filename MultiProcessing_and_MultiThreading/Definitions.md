## Multiprocessing vs. Multithreading
Both multiprocessing and multithreading are techniques used to achieve concurrent execution in Python, but they differ significantly in how they manage tasks and how they utilize system resources.

### 1. Multiprocessing
#### Definition:
Multiprocessing involves running multiple processes in parallel. Each process has its own memory space and Python interpreter. The operating system handles processes independently.

#### Key Characteristics:

 * Multiple Processes: Each task runs in its own separate process. Processes **do not share memory** and **do not have access** to each other's variables (except through inter-process communication).
 * Separate Memory Space: Each process has its own memory, so there is no risk of one process corrupting the memory of another (but communication between processes can be slower).
 * CPU-bound tasks: Multiprocessing is ideal for CPU-bound tasks (tasks that require heavy computation, like numerical calculations, image processing, etc.). Multiple processes can be distributed across different CPU cores, fully utilizing the available CPU resources.
 * Parallelism: True parallelism can be achieved because each process runs on a separate CPU core. This is beneficial for tasks that need intensive computation.

#### Advantages:

* True parallelism on multiple cores.
* Can fully utilize multiple CPUs for computational tasks.

#### Disadvantages:

* Higher memory consumption due to separate memory spaces.
* Communication between processes can be more complex and slower (using Queue, Pipe, or shared memory).

Code:
```
from multiprocessing import Pool

def square(x):
    return x * x

with Pool(4) as p:  # Create a pool with 4 processes
    results = p.map(square, [1, 2, 3, 4])
print(results)  # [1, 4, 9, 16]

```
### 2. Multithreading

#### Definition: 
Multithreading involves running multiple threads within the same process. All threads **share the same memory space**, which makes communication between threads easier.

#### Key Characteristics:

  * Multiple Threads: Threads are lighter-weight than processes and share memory space with other threads. They can directly access shared data structures.
  * Shared Memory: All threads within a process share the same memory space, so they can access and modify the same data. However, you must manage concurrent access (via locks, semaphores, etc.) to avoid race conditions.
  * I/O-bound tasks: Multithreading is ideal for I/O-bound tasks (e.g., web requests, reading/writing files, etc.). Threads can wait on I/O operations without blocking other threads, allowing the CPU to continue performing other tasks.
  * Concurrency (not true parallelism): Because of Python’s Global Interpreter Lock (GIL), multithreading in Python does not achieve true parallelism for CPU-bound tasks. The GIL prevents multiple threads from executing Python bytecodes simultaneously on multiple CPU cores, even on multi-core systems.

 #### Advantages:

  * Lower memory overhead since all threads share the same memory space.
  * Easier communication between threads (since they share memory).
  * Ideal for I/O-bound tasks where the program spends time waiting on external resources.

#### Disadvantages:

  * Global Interpreter Lock (GIL) for python: For CPU-bound tasks, the GIL prevents true parallelism, as only one thread can execute Python bytecode at a time in a process.
  * Potential issues with thread synchronization (race conditions, deadlocks).

    ```
    import threading

    def print_numbers():
        for i in range(5):
            print(i)
    
    thread1 = threading.Thread(target=print_numbers)
    thread2 = threading.Thread(target=print_numbers)
    
    thread1.start()
    thread2.start()
    
    thread1.join()
    thread2.join()

```
