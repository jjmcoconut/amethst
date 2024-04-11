
Lecture notes from Operating System & Lab taught by Insik Shin - KAIST
### Introduction

- Computer science is abstraction(making things simple)
- First design and then code
	- Divide and conquer method would be good for this lecture's project.

4 Computer system structure
1. Users
	- People who uses the computer
2. Hardware
	- provides basic computing resources
	- cpu, gpu, ram, etc.
3. Software(Application programs)
	- Defines way how to use system resources
4. Operating system
	- Controls & coordinates use of hardware
	![[Pasted image 20240226135211.png|200]] (We will consider User, Application as one)
	

Role of operating system (Similar to government)
- Facilitator
- Traffic Cop
- Example) File system(logical storage)
	- We save data physically on a disk sector(HDD).
	- However we do not care or know the disk sector -> we need a file system
	- File system is needed by everyone(Facilitator)
	- But the file system needs to be protected(Traffic Cop)
- The reason why this operating system works: People believe operating system works perfectly and also safe, but not sure with applications.
- If we want to reduce the code size(make it smaller& trustworthy)
	- Keep the traffic cop functionality, and give up the facilitator(Available at the application level).

Definition of operating system
- No universal definition
- Suggestion: Everything a vendor ships when you order an operating system
- The only program that need to be always running - Kernel or Operating System


### Computer System Organization

Keywords: Interrupt, System Call, Kernel

A simple model of a computer:

![[Pasted image 20240228131236.png|400]]

Can be divided into: Device, Memory, CPU

How can devices can be controlled?
1.  Device has a device controller(DC) for each device
2. Each device controller a local storage called buffer.
2. CPU and buffer communicates giving data
OS should have a Device Driver(DD) for each controller
1. DD loads proper registers within DC
2. mDc looks at registers and choose what to do
3. DC moves data to local buffer
4. DD moves data from local buffer to memory
DD is with the OS(CPU), DC is within the device

Some kind of negatives for this procedure?
- This involves the CPU to do the job, but CPU is an expensive source.
- CPU has to wait? - stays idle(busy waiting) while the DC does its job(2,3)
$\rightarrow$ Solution: Interrupt
- CPU can do some else job when DC is doing the job(2,3)
- Use interrupt to use CPU back again when CPu needs to do job 4
Interrupt driven I/O
1. DD loads proper register in DC
2. DC looks at registers and choose what to do
3. DC moves data device $\rightarrow$ local buffer
4. DC interrupts DD
5. DD returns control of OS fetch the information
This case CPU is free in the steps 2-4 

__Interrupt__
- Uses interrupt vector(contains addresses of all service routines)
- must save address of the interrupted instruction(the one CPU has doing)
- trap is software-generated interrupt
- OS is interrupt driven(?)

Example) OS is the only one that is trusted(availed to use DD to change devices)
![[Pasted image 20240228135114.png|500]]

Dual Mode Operation
- Kernel mode
	- privileged mode
	- all instructions may be executed
	- user threads is never run in this mode
- User mode
	- some commands are 'privileged'
	- user threads use this mode

Life cycle
1. System powered on: kernel mode
2. System booted & kernel init: kernel mode
3. user programs: user mode
4. Interrupt, trap, system call: kernel mode
	- Interrupt: hardware device
	- trap: cpu
	- system call: applications(communication mechanism Application $\leftrightarrow$ OS)
![[Pasted image 20240228135448.png|500]]

__System Calls__
- programming interface to the services provided by OS
- API(Application Program Interface) is used because it is compatible with various OS.
	- printf() in C can be used in Linux, Mac OS, Windows, ...
	- While write() system call may be different in each OS(?)
- Number is associated with system call - each number representing what to do
- system call interface invokes intended system call in OS kernel and returns status of the system call and return values

__OS Design__
Bottleneck: entire system is limited by some element
Previously: CPU was slow $\rightarrow$ CPU was a bottleneck
Now: I/O is slower $\rightarrow$ I/O became a bottleneck $\rightarrow$ we need to design a OS that considers this bottleneck
- Multi-programming
- Bigger cache

I/O bottleneck $\rightarrow$ Solution: multiprogramming
Any challenges?

### Process

How to provide multiprogramming?
Process: unit of execution and allocation $\rightarrow$ used for Virtual Machine Abstraction: Illusion that each process has its own computer
![[Pasted image 20240304132408.png|400]]
Sequential stream of instructions are usually called "program"

![[스크린샷 2024-03-04 13.46.11.png|300]]
- Stack: Temporary data(function parameters, return addresses, local variables)
- Static data: Global variables
- Heap: Memory that is allocated during running time
- Code: Program code(text)
Size of static data, code section is fixed. Stack, heap section is not.

To provide illusion: Should remember the state of the previous process(Maintain the environment, In this case environment is the process)

![[Pasted image 20240304132553.png|400]] - The stack, heap, data, code parts are separated by the other program $\rightarrow$ It does not care about the allocation of physical memory addresses

__Process Control Block__
![[Pasted image 20240304133107.png|300]]
PCB: repository for any information that may vary from process to process
used for: Context Switching

__Context switch__
![[Pasted image 20240304133509.png|400]]
Operating system does the context switch: kernel has to get control of the CPU constantly
How does the kernel get in charge? 
- Running process can pass control to kernel(system call, page fault, illegal instructions, ...)
- Timer interrupt
- I/O interrupt
Context switch needs time to change between process - In this time the CPU does not do anything
Need to reduce the context switch time. $\rightarrow$ Better hardware, multiple set of registers(CPU cache?)

__Creating a process__
1. Create PCB - state, context of resources
2. Create virtual resource - I/O state, ...

__int fork() (UNIX system)__
Creates a copy of itself: Child process
fork returns 
- Parent process: pid(process id) of the child
- Child process: 0
![[Pasted image 20240304135822.png|300]] $\rightarrow$![[Pasted image 20240304135852.png|300]]

__Lifecycle of process__
![[Pasted image 20240304140349.png|400]]
process termination
- When to terminate: After process does its job done
- What does it do: deallocate resources, PCB
- parent decides to terminate child process
	- Some OS does not child to continue if parent terminates - cascading termination

Parent-child correlation
![[Pasted image 20240304141046.png|400]]
Parent needs to wait() $\rightarrow$ If child exit() before parent's wait(), it becomes *zombie process*
If parent exit() before child exit() (Grandparents may terminate parent process or by illegal instructions) $\rightarrow$ Child process becomes an *orphaned process* $\rightarrow$ Re-parented to init process()
Init process: root of the process hierarchy(periodically invokes wait())

Problems of wait()
- If it is synchronous: it needs to keep checking all the child process if it is terminated or not
$\rightarrow$ Asynchronous way to wait()
- signal handlers: parent can use SIGCHLD signal (sth similar to interrupt)
- waitpid(): work on non-blocking mode
	- In this way we can improve performance
	- However it becomes more complicated

__Cooperating processes__
Ex) Chrome browser
What if browsers run as single process: if one web site causes problem, the entire browser will crash
Chrome has 3 categories of processes:
- Browser: UI, disk & network I/O
- Renderer: Render web pages, HTML, ...(# of tabs)
- Plug-in: such as adblock.
Internet $\rightarrow$ network I/O(browser) $\rightarrow$ render engine, DOM tree(renderer) $\rightarrow$ compositor $\rightarrow$ GPU thread(browser)
Why do we separate into different processes
- Advantage:
	- fault isolation(fault is available but the impact is not great as before)
	- Security
		- Renderer only uses CPU(cannot access memory, I/O)
		- Everything else should be done by browser process (same-origin policy?)
- Disadvantage: having multiple processes decreases the speed

![[Pasted image 20240306133701.png|450]]
Shared Memory mapping
- Region of memory is shared by cooperating process
- More efficient(Does not use system calls)
Message passing
- Communication takes place by message exchanged btw cooperating process
- Safe but slow(uses system calls)

POSIX shared memory
```
// Creates shared memory content
segment_id = shmget(IPC PRIVATE, size, S_IRUSR | S_IWUSR);

// Getting access to shared memory
shared_memory = (char *) shmat(id, NULL, 0); 

// Writing on the shared memory
sprintf(shared_memory,"HI");

// Detach shared memory
shmdt(shared_memnory);
```

__Process vs Thread__

|                              | Process                              | Thread                                                                         |
| ---------------------------- | ------------------------------------ | ------------------------------------------------------------------------------ |
| Switch overhead              | high(memory/IO bottleneck)           | low                                                                            |
| CPU state                    | low                                  | low                                                                            |
| Memory/IO state              | high                                 | none                                                                           |
| Process/thread creation load | high                                 | low                                                                            |
| CPU protection               | yes                                  | yes                                                                            |
| Memory/IO protection         | yes(secured, hard to share memory)   | no(non-secured, easy to share memory)                                          |
| Sharing overhead             | high(context switch)                 | low(thread switch)                                                             |
| Image                        | ![[Pasted image 20240306140207.png]] | ![[Pasted image 20240306140241.png]]Has multiple PC, SP, stack for each thread |
Inter-process collaboration is hard $\rightarrow$ Make concept of thread $\rightarrow$ Does new concept thread work with the traditional architecture? $\rightarrow$ Yes -> Thread unit of scheduling -> Process are containers of threads

__Thread states__
Thread should do context switches as process does but in different way
State shard by all threads in process/ addr space
- Content of memory
- I/O state
State private to each thread
- TCB
- CPU registers
- execution stack
	- parameters, temporary variables
	- return PCs

__Thread management__
- OS(OS takes care of all thread operation)
	- System call based, TCB
- User level(User-level library takes care of all thread operation)
	- Done by procedure calls(no kernel involved $\rightarrow$ x10~100 faster)
	- transparent to OS(may not match well)
	- OS can make poor scheduling decision(may not fully utilize CPUs)

__Threading Models__
- Many to one
	- Bottleneck with kernel threads
- One to one
	- Each user thread has a kernel thread -> making kernel thread takes time
- Many to many
	- java

### Scheduling
Scheduling - To obtain maximum CPU utilization
Scheduling criteria
1. CPU ultilization
2. Throughput
	- Number of processes that complete their execution per unit time
3. Turnaround time
	- Amount of time to execute a particular process
4. Waiting time
	- Amount of time waiting in the ready queue
5. Response time
	- Amount of time it take until the first response from the request submit

#### Scheduling Algorithms

##### First-Come, First-Served(FCFS)

| Process | Burst Time |
| ------- | ---------- |
| P1      | 24         |
| P2      | 3          |
| P3      | 3          |

Then the resulting order would be
![[Pasted image 20240411232921.png|400]]
- Average waiting time = $(0+24+27)/3 = 17$

##### Shortest Job First

| Process | Burst Time |
| ------- | ---------- |
| P1      | 6          |
| P2      | 8          |
| P3      | 7          |
| P4      | 3          |

![[Pasted image 20240411233305.png|400]]
- Average waiting time: $(3+16+9+0)/4=7$
- Optimal strategy but, difficult to know the length of next CPU request
##### Round Robin
Each process gets a small unit of CPU time. After that time the process is preempted and added to the end of ready queue

| Process | Burst Time |
| ------- | ---------- |
| P1      | 24         |
| P2      | 3          |
| P3      | 3          |

![[Pasted image 20240411233728.png|400]]
- Average waiting time: $(6+4+7)/3=5.66$
- Higher average turnaround than SJF, but better response

##### Priority Scheduling
Priority number is associated with each process
- Problem-Starvation: low priority process may never execute
- Solution-Aging: Increase priority as time progresses.

##### Multilevel Queue
Ready queue is composed with multiple queues
- each queue has its own scheduling algorithm
- Scheduling must be done between queues
- Popular example: Separate queues for different priority
![[Pasted image 20240411234503.png|300]]

##### Multilevel Feedback Queue
Multilevel queue + allows process to move around queues
![[Pasted image 20240411234829.png|300]]
Multilevel feedback queues favor:
1. Short CPU bursts
2. I/O bound
3. Interactive

### 6. Synchronization
Race condition: where several processes access and manipulate the same data concurrently and the outcome of the execution depends on the particular order in which the access takes place

#### 6.2 The Critical-Section Problem
- Critical section: 
	  Section that the data is shared with at least one other process
- Mutual Exclusion:
	  Ensuring that only one thread executes critical section
- Synchronization:
	  Multiple threads work together to do some action
- Lock:
	  Prevents someone from doing something
Suppose we have 2 threads A,B:
```
y=0; (initial value)
thread A:
	x=1;      (1)
	x=y+1;    (2)
thread B:
	y=2;      (3)
	y=y*2;    (4)
```
Then just by different orders we have different results
3412: x=5, y=4
3124: x=3, y=4

Advantages of Concurrent Threads 
- Allows transparent overlapping of computation and I/O
- Allows use of parallel processing when available
Problems we need to care about when using concurrency
- Programs must be insensitive to arbitrary interleavings
- Without careful design shared variables can become completely inconsistent.

#### Priority Inversion
Scenario where a lower-priority task blocks the execution of a higher-priority task
- It negates the principle of priority based scheduling

How does it happen?
![[Pasted image 20240412001815.png|500]]
1. TL holds a shared resource R
2. TM preempts TL
3. TH task wants to access R
4. TH needs to wait until TL releases R, and TL needs to wait until TM to finish
The problem here is that TH needs to wait for TM to finish for no reason.
It may be critical if the TH is an important thread

##### Solution: Priority Inheritance
![[Pasted image 20240412002217.png|500]]
- TH increases the priority of TL equivalent to TH.
- After TL executing the critical section priority of TL is returned to its original priority

#### Too Much Milk

__First Case__
![[Pasted image 20240412002825.png|300]]
This may result in having 2 milk.

__Second Case - Leaving a note__
![[Pasted image 20240412003147.png|200]]  ![[Pasted image 20240412002947.png|300]]
Leaving a note is not enough
If executed as above we get 2 milk

__Third Case - Early Notes__
![[Pasted image 20240412003126.png|350]] ->
![[Pasted image 20240412003303.png|350]]
Still possible to have 2 milk.

__Fourth Case - 2 note solution__
![[Pasted image 20240412003613.png|400]]
- Critical section: 
```
  if(noMilk){
	  buy Milk;
  }
```
- This solution works but its not good
	- Complex
	- Code A is different from B
	- A is busy waiting - consumes CPU
__Solution: Use lock__
- Lock.Acquire(): wait until lock is free, then take it
- Lock.Release(): unlock, waking up anyone waiting\
Therefore the above code can be changed into
```
milklock.Acquire();
if(noMilk){
	buy Milk;
}
milklock.Relase();
```
Section between Acquire() and Release() is the critical section

