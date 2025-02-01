## Multiprocessing vs. Multithreading
Both multiprocessing and multithreading are techniques used to achieve concurrent execution in Python, but they differ significantly in how they manage tasks and how they utilize system resources.

### 1. Multiprocessing
Definition: Multiprocessing involves running multiple processes in parallel. Each process has its own memory space and Python interpreter. The operating system handles processes independently.

#### Key Characteristics:

 * Multiple Processes: Each task runs in its own separate process. Processes do not share memory and do not have access to each other's variables (except through inter-process communication).
 * Separate Memory Space: Each process has its own memory, so there is no risk of one process corrupting the memory of another (but communication between processes can be slower).
 * CPU-bound tasks: Multiprocessing is ideal for CPU-bound tasks (tasks that require heavy computation, like numerical calculations, image processing, etc.). Multiple processes can be distributed across different CPU cores, fully utilizing the available CPU resources.
 * Parallelism: True parallelism can be achieved because each process runs on a separate CPU core. This is beneficial for tasks that need intensive computation.

#### Advantages:

* True parallelism on multiple cores.
* Can fully utilize multiple CPUs for computational tasks.

#### Disadvantages:

* Higher memory consumption due to separate memory spaces.
* Communication between processes can be more complex and slower (using Queue, Pipe, or shared memory).
