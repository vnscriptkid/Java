## Fundamentals

### Questions list
- Why do we need multi-threading?
  - Performance
  - Reponsiveness
- What is the difference between responsiveness vs performance?
  - Responsiveness can be achieved by concurrency
  - Performance can be achieved by parallelism
- Give an example about poor responsiveness with a single thread?
  - Request from one client that requires server a long time to process, thus blocking requests from other clients
- Give an example about responsiveness in User Interface?
  - User clicks on Play button watching movie on Netflix, the experience is smooth and there's no delay
- What is concurrency? Doing many tasks at the same time 
- Why don't we need multiple cores to achieve concurrency?
  - With single core CPU, we can run small piece of code from each thread, creating illusion of they run in parallel
- What is the difference between concurrency và parallelism?
  - Parallelism is through multi-threading on CPU with multiple cores
  - Concurrency is process of doing a little bit of everything
- How to trully achieve parallel processing? Multiple cores CPU
- By what do we achieve reponsiveness and performance?
- What is the difference between single-threaded vs multi-threaded programming?
- What is the role of OS?
  - Serves as a layer of abtraction, helping application to use resources like: hard disk, CPU
- Which elements does a process contain?
  - Metadata
  - Files that opened by program
  - Heap memory
  - At least 1 main thread
  - Instructions
- What is a process? context or instance of an application.
- What are threads, Where they live and what they contain?
  - A thread is a flow of execution through the process code
  - Contains: Stack, program counter (stores address of next instruction to execute)
- 1 process always contains at most 1 thread, is it true or false?
  - False, at least 1 thread (main thread)
- What threads share?
  - Metadata
  - Files
  - Code
  - Heap memory
- What is stack? Where does it reside in?
  - Stores functions in order of execution and local vars, LIFO
  - 1 thread has 1 stack
- What is instruction pointer? Where is it used in?
  - Store the next instruction to be executed
  - In stack
- Why stack has its own stack and instruction pointer?
  - So that different functions can run at the same time
- What are pros and cons of multi-threading?
- What are the impacts of performance?
- What is context switch and why we need it?
  - Is the process of CPU turning his attention from one thread to another thread
- What is the price of multitasking?
  - Switching between threads
- What are costs of using multi-threads?
  - Save data of current thread
  - Load data from another thread to CPU
- What is thrashing?
  - There's are too many threads, means too many context switching
- With what context switch happens? Threads and proccesses
- Compare context switching between threads vs between proccesses? Which is more expensive? Why?
  - Context swithching between threads is less expensive
  - Threads store way less data than proccesses
  - Threads in the same process shares lot of common things
- What happens when threads switching happens?
- What are the problems with FCFS?
  - Tasks come later might wait for a long time before it's executed
- What are the problems with Shortest Job First?
  - Tasks with long execution time might wait for a long time before it's executed 
- How actually OS schedules threads?
  - CPU time is divided into units as epochs
  - Every task has priority = static + bonus
- What is dynamic priority? How it's caculated? Where it's used?
  - In order to decide which task should be executed first
- Who sets static priority? Developers
- Who control the bonus - a variable in dynamic priority?
- What is epoch?
- What is starvation? Whet it happens? How to prevent it?
- List out types of threads? UI threads, Computational threads
- When to use multiple threads and when to use multiple processes (like Chrome) for 1 program 
  - Multithreads program: Threads share lot of common data
  - Multiprocesses program: No common data between processes, more isolation less overhead.

### Diagrams

- Inside Thread 

![image](https://user-images.githubusercontent.com/28957748/123540086-6a4d8280-d767-11eb-8e7b-039d8f755e88.png)

- Computer architecture

![image](https://user-images.githubusercontent.com/28957748/123540160-d03a0a00-d767-11eb-9b23-e63ea5b476b8.png)

- Single-threaded process

![image](https://user-images.githubusercontent.com/28957748/123540228-332ba100-d768-11eb-882a-a51bf8017596.png)

- Multi-threaded process

![image](https://user-images.githubusercontent.com/28957748/123540291-6a9a4d80-d768-11eb-96ab-a6cc63245e31.png)

- Single-core concurrency

![image](https://user-images.githubusercontent.com/28957748/123540356-c369e600-d768-11eb-840b-36f1a4d2fb02.png)

- Parallelism

![image](https://user-images.githubusercontent.com/28957748/123540390-eb594980-d768-11eb-942e-fc68ab619f23.png)

- Responsiveness with multi-threads

![image](https://user-images.githubusercontent.com/28957748/123540499-818d6f80-d769-11eb-876c-8580b59662bd.png)

- Responsiveness with single-thread

![image](https://user-images.githubusercontent.com/28957748/123540548-bf8a9380-d769-11eb-90c7-751e3d2d6c3a.png)

- Responsiveness in User Interface

![image](https://user-images.githubusercontent.com/28957748/123540578-ed6fd800-d769-11eb-96f2-27352107ebcf.png)

- Task scheduling

![image](https://user-images.githubusercontent.com/28957748/123542248-c23db680-d772-11eb-9a68-1ddc044cbd16.png)

![image](https://user-images.githubusercontent.com/28957748/123542278-f3b68200-d772-11eb-8840-8b113f6a0a2f.png)

- First come first serve

![image](https://user-images.githubusercontent.com/28957748/123542645-f87c3580-d774-11eb-8a77-854fb562b40c.png)


