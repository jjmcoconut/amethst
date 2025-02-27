
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
![[Pasted image 20240411234503.png|300]]
Ready queue is composed with multiple queues
- each queue has its own scheduling algorithm
- Scheduling must be done between queues
- Popular example: Separate queues for different priority

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
- 3412: x=5, y=4
- 3124: x=3, y=4

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



# 9. File systems

__Directory Structure__
- Metadata are stored in the file control block (i.e., i-node)
- For single indirect: 1000 can be linked, each data block is 4B then one single indirect block can cover up to 4MB
- double indirect: 4GB, triple indirect: 4TB
![[Pasted image 20240422130706.png|350]]![[Pasted image 20240422131153.png|350]]

__File size Distribution__
![[Pasted image 20240422131123.png|500]]

__File Types__
- File types help OS to perform reasonable operations on files, i.e.,
- What kinds of operations can OS do?
	- Disallow printing binary executable programs
	- Execute appropriate applications when double-clicking the mouse on some file icons

__Directory Structure__
![[Pasted image 20240422131611.png|300]]
- A collection of nodes containing information about all files
- Both the directory structure and the files reside on disk
- Good design principle: a directory itself as a file
	- we have different type of data, but want to save in the same place

__Naming__
- Naming (name resolution): process by which a system translates from user-visible names to system resources
- In the case of files, need to translate from strings (textual names) or icons to inumbers/inodes
- For global file systems, data may be spread over globe -> need to translate from strings or icons to some combination of physical server location and inumber

__Directory Organization__
- Directories organized into a hierarchical structure
	- Seems standard, but in early 70’s it wasn’t
	- Permits much easier organization of data structures
- Entries in directory can be either files or directories
- Files named by ordered set
	- (e.g., /classes/cs330/lecture01.pdf)

__Directory Structure__
![[Pasted image 20240422132140.png|400]]![[Pasted image 20240422132335.png|100]]
- Not really a hierarchy!
	- Many systems allow directory structure to be organized as an acyclic graph or even a (potentially) cyclic graph
	- Link: another name (pointer) to an existing file
	- we have a cycle structure in the picture: book->avi->book

- How many disk accesses to resolve “/classes/cs330/lecture01.pdf” (1MB)?
	- Where are the following informations stored?
		- we need 256 blocks(1MB/4KB=256)
		- index block to save each pointer of each block
		- ![[Pasted image 20240422132909.png|400]]
		- Above picture is inode(same as FCB: file control block)
		- We need all 12 of direct blocks and several in single indirect block
		- but where are these inodes stored?
- Answer
	- Read in file header for root (fixed spot on disk, PCB knows where inode of root is)
	- Read in first data block for root
	- Table of file name/index pairs. Search linearly – ok since directories typically very small
	- Read in file header for “classes”
	- Read in first data block for “classes”; search for “cs330”
	- Read in file header for “cs330”
	- Read in first data block for “cs330”; search for “lecture01.pdf”
	- Read in file header for “lecture01.pdf”
	- Read in data blocks for “lecture01.pdf”

__File Systems__
- Issues on directory
	- Most file operations involve searching the directory for the entry associated with the file name
	- How to resolve this?

__Open File(Cache)__
![[Pasted image 20240422135300.png|400]]
- Open-file table
	- To avoid constant searching, OS keeps a small table containing information about all open files (open-file table)
	- When a file operation is requested, the file is specified via an index into this table, so no searching is required
- File operations
	- Open(Fi)– search the directory structure on disk for entry Fi, and move the content of entry to memory
	- Close (Fi)– move the content of entry Fi in memory to directory structure on disk
- Several pieces of data are needed to manage open files:
	- File pointer
		- pointer to last read/write location, per process that has the file open
	- File-open count
		- counter of number of times a file is open – to allow removal of data from open-file table when last processes closes it
		- If multiple process access same file & one file wants to close it, in the system-wide open-file table should not close the file since another process is still using it.
	- Disk location of the file
		- cache of data access information
	- Access rights
		- per-process access mode information

Tree-Structured Directories
- Absolute or relative path name
- Creating a new file/directory is done in current directory
	- `mkdir <dir-name>`
- Delete a file
	- `rm <file-name>`

__File System Mounting__
![[Pasted image 20240422140310.png|450]]![[Pasted image 20240422140328.png|250]]
- Mounting
	- In Unix, it arranges all files accessible in one single big tree, the file hierarchy, rooted at “/”
	- Files can be spread out over several devices
		- A file system (from another device) must be mounted before it can be accessed
	- An unmounted file system is mounted at a mount point, which is typically an empty directory
- Example
	- The second partition of a hard disk is mounted with the command:
		- $ mount /dev/hda2 /new/subdir
	- and unmounted with the command:
		- $ umount /dev/hda2 or $ umount /new/subdir
- File system type
	- OS inspects the structures of a device & determines the type of file system
- A mounting point
	- Path is constructed from the mounting point
- Verification process
	- OS asks the device driver to read the device directory and verifies that the directory has the expected format
- Mounting semantics
	- Systems impose semantics to clarify functionality
	- Mounting point
		- Only allows an empty directory
		- Mount a new FS and hide existing FS; restore existing one after terminating mounting
	- Mounting
		- Allow one mount per FS
		- Allow multiple mountings

__File Sharing__
- Sharing of files on multi-user systems is desirable
- Sharing may be done through a protection scheme
- On distributed systems, files may be shared across a network
- Network File System (NFS) is a common distributed file-sharing method

__File Sharing – Multiple Users__
- User IDs identify users, allowing permissions and protections to be per-user
- Group IDs allow users to be in groups, permitting group access rights

__File Sharing – Remote File Systems__
- Uses networking to allow file system access between systems
	- Manually via programs like FTP
	- Automatically, seamlessly using distributed file systems
	- Semi automatically via the world wide web
- Client-server model allows clients to mount remote file systems from servers
	- Server can serve multiple clients
	- NFS is standard UNIX client-server file sharing protocol
	- CIFS is standard Windows protocol
	- Standard operating system file calls are translated into remote calls

__File Sharing – Consistency Semantics__
- Consistency semantics specify how multiple users access a shared file simultaneously
	- Similar to process synchronization algorithms
		- Tend to be less complex due to disk I/O and network latency (for remote file systems)
	- Semantics for concurrent accesses:
		- What happens when one process reads while another writes?
		- What happens when two processes open the same file?
	- How much difference allowed?
		- In some situation, different users may have different view on the shared file, then we may define the level of difference(e.g. Google Docs, SNS)
			- For Google Docs we should make the change visible immediately
			- For likes or comments in Facebook, YouTube does not need to be immediate
- Unix file system (UFS) implements:
	- Writes to an open file visible immediately to other users of the same open file
	- Sharing file pointer to allow multiple users to read and write concurrently (i.e., fork())
- AFS has session semantics (Andrew File System)
	- A session begins/ends when a file is open/closed
	- Writes only visible to sessions starting after the file is closed
		- If conflict occurs when multiple people wants to write at same time -> Do not use AFS, use UFS

__Protection__ _(Not Important?)_
- File owner/creator should be able to control:
	- what can be done
	- by whom
- Types of access
	- Read
	- Write
	- Execute
	- Append
	- Delete
	- List

__Access Lists and Groups__ _(Not Important?)_
- Mode of access: read, write, execute
- Three classes of users
  ![[Pasted image 20240501132113.png|300]]
- Ask manager to create a group (unique name), say G, and add some users to the group.
- For a particular file (say game) or subdirectory, define an appropriate access.
  ![[Pasted image 20240501132147.png|300]]
- Example
	- Android is a single-user system using UNIX
	- For UNIX: different users are not trusted, but application between one user is trusted.
	- But there are situations where we do not want trust between applications(banking apps, ...)
	- We use protection for these

__Performance__
- Keeping data and metadata close together
- Buffer cache - separate section of main memory for frequently used blocks
- Synchronous writes sometimes requested by apps or needed by OS
	- No buffering / caching – writes must hit disk before acknowledgement
	- Asynchronous writes more common, buffer-able, faster
- free-behind and read-ahead – techniques to optimize sequential access

__Page Cache__
![[Pasted image 20240501140702.png|200]]
- A page cache caches pages rather than disk blocks using virtual memory techniques
- Memory-mapped I/O uses a page cache
- Routine I/O through the file system uses the buffer (disk) cache
- Caching file data using virtual address is far more efficient than caching through physical disk blocks

__Unified Buffer Cache__
![[Pasted image 20240501140731.png|200]]
- A unified buffer cache uses the same page cache to cache both memory-mapped pages and ordinary file system I/O to avoid double caching

__Reliability__
- File system consistency
	- File system can go into an inconsistent state if cached blocks are not written out due to the system crash
	- It is especially critical if it happens to directory / i-node / free-block-list blocks
	- Some utility programs for checking file system consistency
	- scandisk (Windows), fsck (UNIX)
- fsck : checking blocks
  ![[Pasted image 20240501140915.png|400]]
	- Read all the i-nodes and mark used blocks
	- Examines the free list and mark free blocks

__Recovery__
- Recovery from backup
	- Use system programs to back up data from disk to another storage device (magnetic tape, other magnetic disk, optical)
	- Recover lost file or disk by restoring data from backup
- Recovery from log

__Log Structured File Systems__
- Log structured (or journaling) file systems record each update to the file system as a transaction
- All transactions are written to a log
	- A transaction is considered committed once it is written to the log
		- Sometimes to a separate device or section of disk
	- However, the file system may not yet be updated
- The transactions in the log are asynchronously written to the file system
	- When the file system is modified, the transaction is removed from the log
- If the file system crashes, all remaining transactions in the log must still be performed
- For example, deleting a file on a Unix file system involves two steps:
	1. Removing its directory entry.
	2. Marking space for the file and its inode as free in the free space map.
- If a crash occurs between steps 1 and 2, there will be an orphaned inode and hence a storage leak.
- On the other hand, if only step 2 is performed first before the crash, the not-yet-deleted file will be marked free and possibly be overwritten by something else.

__WrapUp__

__File-System Implementation__
- Boot Control Block (BCB) contains info needed by system to boot OS from that partition
	- Needed if partition contains OS, usually first block of partition
- Partition Control Block (PCB) contains partition details (FS metadata)
	- Total # of blocks, # of free blocks, block size, free block pointers
- Directory structure organizes the files
	- Names and inode numbers, master file table
- Per-file File Control Block (FCB) contains many details about the file (file metadata)
	- Inode number, permissions, size, dates

__Allocation Methods__
- Allocation methods for how to allocate disk blocks to files:
  ![[Pasted image 20240424130611.png|500]]
- Contiguous allocation disadvantages: fragmentation, file size is fixed(cannot grow)
- Indexed allocation: uses one block as a list of indexes for allocated resources
	- disadvantage: needs more space & need to access separate block(expensive)

__Directory Structure__
- Metadata are stored in the file control block (i.e., i-node)
  ![[Pasted image 20240424131004.png|500]]
- data blocks are another directory table(?, need checking)

__Naming__
- How many disk accesses to resolve: “/users/i/insik.shin/thumbnail.jpg” (1KB)?
1) Read in i-node for root (fixed spot on disk)
2) Read in first data block for root
3) Read in i-node for “users”
4) Read in first data block for “users”; search for “i”
5) Read in i-node for “i”
6) Read in first data block for “i”; search for “insik.shin”
7) Read in i-node for “insik.shin”
8) Read in first data block for “insik.shin”; search for “thumbnail.jpg”
9) Read in i-node for “thumbnail.jpg”
10) Read in first data block for “thumbnail.jpg”


__Finding a Needle in a Haystack: Facebook’s Photo Storage__

__Main Goals for Photo Serving Method__
- Four main goals for photo serving method:
	- High throughput and low latency
		- Provide a good user experience
	- Fault-tolerant
		- Handle server crashes and hard drive failures
		- Lifespan of HDD is about 3~5 years, For 20PB we need 20k of 10TB HDD. -> average of 20. HDD fails every day.
	- Cost-effective
		- Save money over traditional approaches (reduce reliance on CDNs!)
	- Simplicity
		- Make it easy to implement and maintain
- Typical Design
  ![[Pasted image 20240424132419.png|500]]
	- If CDN has high cache hit ratios -> efficient(does not need to access Photo Storage which is Facebook)
	- How many days should the CDN store the cache?

__Background__
- Two types of workloads for image serving
	- Profile pictures – heavy access, smaller size
	- Photo albums – intermittent access, higher at beginning, decreasing over time (long tail)
- ![[Pasted image 20240424132905.png|400]]
	- 80 percent of the access requested for about the first 240 days.
	- If they choose to extend the age of cache twice, they need to double the storage size(costly).
		- Cannot have infinite cache age

__Facebook vs. Typical Websites__
- Typical websites
	- Small working set
	- Infrequent access of old content
	- ~99% CDN hit rate
- Facebook
	- Large working set
	- Frequent access of old content
	- 80% CDN hit rate

__Facebook’s Old Design__
- The old photo infrastructure consisted of several tiers:
	- Upload tier receives users’ photo uploads, scales the original images and saves them on the NFS storage tier.
	- Photo serving tier receives HTTP requests for photo images and serves them from the NFS storage tier.
	- NFS storage tier built on top of commercial storage appliances

__NFS based Design__
- Metadata bottleneck
	- Each image stored as a file
	- Large metadata size severely limits the metadata hit ratio (in the cache)
- Image read performance
	- ~10 iops / image read (large directories – thousands of files)
		- If we have deep directories then for one file access, we need a lot of disk accesses.
	- ~3 iops / image read (smaller directories – hundreds of files)
		- For usual file access we need at least 3 accesses:
			- read the directory metadata into memory
			- load the inode into memory
			- read the file contents
		- Facebook wants to shorten this process
			- We do not use symbolic names for images in Facebook -> does not need directory table
			- There is no reason not to use contiguous allocation method
				- Image size is fixed
				- People usually does not erase photos-> no deallocation
				- can use one location instead of inode
	- ~2.5 iops / image read (file handle cache)
		- Cache the filename-to-file-handle mapping
		- Custom system call: open_by_filehandle
		- A minor improvement (a low cache hit ratio)

Haystack
![[Pasted image 20240424140021.png|500]]
- Addresses the critical bottleneck in NFS-based approach
- Aims to limit the number of operations to only the ones necessary
- Reduces the memory used for filesystem metadata
- Stores multiple photos in a single file
- Two kinds of metadata
	- Application metadata
		- Information needed to construct a URL
	- Filesystem metadata
		- Identify the data necessary for a host to retrieve the photos
- Aims to retrieve the filename, offset, and size of a particular photo without any disk operations
- On a disk, a single very large file (100GB) is saved as `/hay/haystack_<logical volume id>`

Layout of Haystack Store file
- A Haystack Store file is a logical storage, and a needle is for a single image
- Main purpose: to reduce file system-level metadata (namespace directory and inode)
  ![[Pasted image 20240424140152.png|500]]

Haystack Index File
- The index file provides the minimal metadata required to locate a particular needle in the store
- Main purpose: allow quick loading of the needle metadata into memory without traversing the larger Haystack store file
- Index is usually less than 1% the size of the store file
  ![[Pasted image 20240424140207.png|500]]

Haystack - Summary
- Simplified metadata
	- No directory structures/file names
		- 64-bit ID
	- Results in easier lookups
- Reduced disk I/O
	- Optimized for random reads (~1 I/O per object read)
	- 1 MB of metadata for every 1GB of usable storage
	- 10 TB/node results in 10 GB of metadata
		- This amount is easily cacheable!
- 8,500 LOC (C++)
	- 2 engineers 4 months from inception to initial development

# Mass-Storage Systems

__Disk__
![[Pasted image 20240429131105.png|300]]
- Stack of magnetic platters
	- Rotate together on a central spindle at 3,600-15,000 RPM
- Disk arm assembly
	- Arms rotate around pivot, all move together
	- Arms contain disk heads – one for each recording surface
	- Heads read and write data to platters

__Properties of a Magnetic Hard Disk__
![[Pasted image 20240429131122.png|400]]
- Properties
	- Independently addressable element: sector(smallest unit on disk available to write)
		- OS always transfers groups of sectors together—“blocks”
	- A disk can access directly any given block either sequentially or randomly.
- Typical numbers (depending on the disk size):
	- 500 to more than 20,000 tracks per surface
	- 32 to 800 sectors per track
- Zoned bit recording
	- Constant bit density: more bits (sectors) on outer tracks
- Properties
	- Independently addressable element: sector
		- OS always transfers groups of sectors together— “blocks”
	- Cylinder: all the tracks under the head at a given point on all surfaces

__Magnetic Disk Characteristic__
- Read/write: three-stage process:
	- Seek time: position the head/arm over the proper track (into proper cylinder)
	- Rotational latency: wait for the desired sector to rotate under the read/write head
	- Transfer time: transfer a block of bits (sector) under the read-write head
- Disk Latency = Queuing Time + Controller time + Seek Time + Rotation Time + Xfer Time
  ![[Pasted image 20240429131534.png|500]]
- Highest Bandwidth:
	- Transfer large group of blocks sequentially from one track

__Typical Numbers of a Magnetic Disk__

| **Parameter**              | **Info / Range**                                                                                                                                                                                                                             |
| -------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Average seek time          | Typically 5-10 milliseconds.<br>Depending on reference locality, actual cost may be 25-33% of this number                                                                                                                                    |
| Average rotational latency | Most laptop/desktop disks rotate at 3600-7200 RPM (8- 16 ms/rotation). Server disks up to 15,000 RPM.<br>Average latency is halfway around disk yielding corresponding times of 4-8 milliseconds                                             |
| Controller time            | Depends on controller hardware                                                                                                                                                                                                               |
| Transfer time              | Typically 50 to 100 MB/s.<br>Depends on:<br>• Transfer size (usually a sector): 512B – 1KB per sector<br>• Rotation speed: 3600 RPM to 15000 RPM<br>• Recording density: bits per inch on a track<br>• Diameter: ranges from 1 in to 5.25 in |
| Cost                       | Drops by a factor of two every 1.5 years (or even faster).<br>$0.01/GB in 2021 ($0.025/GB in 2019)                                                                                                                                           |

__Disk Performance Examples__
- Assumptions:
	- Ignoring queuing and controller times for now
	- Avg seek time of 5ms,
	- 7200RPM -> Time for one rotation: 60000ms/7200 ~= 8ms
	- Transfer rate of 4MByte/s, sector size of 1 KByte
- Read sector from random place on disk:
	- Seek (5ms) + Rot. Delay (4ms) + Transfer (0.25ms)
	- Approx 10ms to fetch/put data: 100 KByte/sec
- Read sector from random place in same cylinder:
	- Rot. Delay (4ms) + Transfer (0.25ms)
	- Approx 5ms to fetch/put data: 200 KByte/sec
- Read next sector on same track:
	- Transfer (0.25ms): 4 MByte/sec
- Key to using disk effectively (especially for file systems) is to minimize seek and rotational delays

__Disk Scheduling__
- Disk can do only one request at a time; What order do you choose when handling queued requests?
	- Request denoted by (track, sector)
	  ![[Pasted image 20240429132634.png|500]]
- Scheduling algorithms:
	- First In First Out (FIFO)
	- Shortest Seek Time First
	- SCAN
	- C-SCAN
- In our examples we will ignore the sector
	- Consider only track #
	  ![[Pasted image 20240429132718.png|200]]

__FIFO: First In First Out__
- Schedule request in the order they arrive in the queue
- Example:
	- Request queue: 2, 1, 3, 6, 2, 5
	- Scheduling order: 2, 1, 3, 6, 2, 5
	- ![[Pasted image 20240429132926.png|200]]
- Pros: Fair among requesters
- Cons: Order of arrival may be to random spots on the disk -> Very long 

__SSTF: Shortest Seek Time First__
- Pick the request that’s closest to the head on the disk
	- Although called SSTF, include rotational delay in calculation, as rotation can be as long as seek
- Example:
	- Request queue: 2, 1, 3, 6, 2, 5
	- Scheduling order: 5, 6, 3, 2, 2, 1
	- ![[Pasted image 20240429133052.png|200]]
- Pros: reduce seeks
- Cons: may lead to starvation(aging is a solution)

__SCAN__
- Implements an Elevator Algorithm: take the closest request in the direction of travel
- Example:
	- Request queue: 2, 1, 3, 6, 2, 5, 7
	- Head is moving towards center
	- Scheduling order: 5, 3, 2, 2, 1, 6, 7
	- ![[Pasted image 20240429133517.png|200]]
- Pros: No starvation, Low seek
- Cons: favor middle tracks

__C-SCAN__
- Like SCAN but only serves request in only one direction
- Example:
	- Request queue: 2, 1, 3, 6, 2, 5, 7
	- Head only servers request on its way from center towards edge
	- Scheduling order: 5, 6, 7, 1, 2, 2, 3
	- ![[Pasted image 20240429134131.png|200]]
- Pros: Fairer than SCAN
- Cons: longer seeks on the way back

__Solid State Disks (SSDs)__
- 1995 – Replace rotating magnetic media with non-volatile memory (battery backed DRAM)
	- Since 2009, use NAND Flash: Single Level Cell (1-bit/cell), Multi-Level Cell (2-bit/cell)
- Sector addressable, but stores 4-64 “sectors” per memory page
	- page is the smallest unit of read/write in SSD(HDD: sector)
- No moving parts (no rotate/seek motors)
	- Eliminates seek and rotational delay (0.1-0.2ms access time)
	- Very low power and lightweight

__SSD Architecture – Reads__
Reading data similar to memory read (25μs)
- No seek or rotational latency
- Transfer time: transfer a block of bits (sector)
	- Limited by controller and disk interface (SATA: 300-600MB/s)
- Latency = Queuing Time + Controller time + Xfer Time
- Highest Bandwidth: Sequential OR Random reads

__SSD Architecture – Writes__
- Writing data is complex! (~200μs – 1.7ms )
	- Can only write empty pages (erase takes ~1.5ms)
		- HDD can overwrite on existing data
		- SSD needs to erase first then write
	- Controller maintains pool of empty pages by coalescing used sectors (read, erase, write), also reserve some % of capacity
- Write and erase cycles require “high” voltage
	- Damages memory cells, limits SSD lifespan
	- Controller uses ECC, performs wear leveling
- Result is very workload dependent performance
	- Latency = Queuing Time + Controller time (Find Free Block) + Xfer Time
	- Highest BW: Seq. OR Random writes (limited by empty pages)
		- Sequential easier to implement since can write all data to same pg
- __Rule of thumb__: writes 10x more expensive than reads, and erases 10x more expensive than writes

__QUIZ__
- Q1: The block is the smallest addressable unit on a disk: F
- Q2: An SSD has zero seek time: T
- Q3: For an HDD, the read and write latencies are similar: T
- Q4: For an SSD, the read and write latencies are similar: F
- Q5: Consider the following sequence of requests (2, 4, 1, 8), and assume the head position is on track 9. Then, the order in which SSTF services the requests is: 8, 4, 2, 1

__SSD Summary__
- Pros (vs. hard disk drives):
	- Low latency, high throughput (eliminate seek/rotational delay)
	- No moving parts: Very light weight, low power, silent, very shock insensitive
	- Read at memory speeds (limited by controller and I/O bus)
- Cons
	- Expensive (3-20x disk)
		- Hybrid alternative: combine small SSD with large HDD
	- Asymmetric block write performance: read pg/erase/write pg
		- Controller garbage collection (GC) algorithms have major effect on performance
	- Limited drive lifetime
		- 1-10K writes/page for MLC NAND
		- Avg failure rate is 6 years, life expectancy is 9–11 years
- These are changing rapidly!


# 12. I/O Systems
![[Pasted image 20240508123546.png|500]]

__I/O Subsystem__
- I/O subsystem is a major concern of OS design
	- Two conflicting trends with I/O device technology
		- Increasing standardization of s/w and h/w interfaces
			- We do not need to care about the I/O devices we use.(We can use SSD, RAM from any kind of company)
			- Good to incorporate advanced device generations
		- Increasingly broad variety of I/O devices
			- Imposing difficulties: some new devices are unlike previous ones

__I/O Hardware__
- Incredible variety of I/O devices
	- Storage devices: disks, tapes, SSDs
	- Transmission devices: network cards, modems
	- Human-interface devices: screen, keyboard, mouse
	- Sensors in mobile devices: camera, GPS, accelerometer, gyro, temperature, blood pressure
	- Despite of variety, we need only a few concepts to understand how the devices are attached and how S/W can control H/W

__I/O Subsystem__
![[Pasted image 20240508123640.png|200]]
- Approaches
	- Basic I/O H/W accommodate a wide variety of devices
		- Ports, buses, device controllers
	- S/W: OS is structured to use device-driver modules
		- device drivers present a uniform device access interface to I/O subsystem, like system calls btw OS and applications
	- OS = File systems + Device Driver(In this image)

__I/O Hardware - Common concepts__
- Port
	- Connection point
- Bus (daisy chain or shared direct access)
	- ![[Pasted image 20240508131530.png|400]]
	- A set of wires (to connect different devices)
	- A protocol specifying messages sent on the wires
	- PCI bus (the common PC system bus)
- Controller (host adapter)
	- A collection of electronics that operates a port, a bus, or a device

__I/O Hardware – Controller Examples__
- A serial-port controller (simple)
	- ![[Pasted image 20240508123843.png|500]]
	- A single chip (or its portion) in computer that controls the signals on the wires of a serial port
- A SCSI bus controller (complex)
	- ![[Pasted image 20240508123921.png|500]]
	- A separate circuit board that plugs into computer
	- Contains a processor, microcode, private memory to process the SCSI protocol messages
	- Disk can have its own built-in (disk) controller that implements the disk side of the SCSI protocol, as well as many disk tasks (bad-sector mapping, prefetching, buffering, caching)
	- SCSI bus is good for adopting a new device
		- However the performance is focused on HDD.
		- Therefore if we put devices like SSD we can loose performance

__I/O Hardware__
- Communication btw CPU & devices
	- Controller has registers for data and control signals
	- CPU reads/writes bit patterns in these registers
- Devices have addresses, used by
	- Direct I/O instructions
		- Via I/O port address, bus lines, device registers
	- Memory-mapped I/O
		- Device registers are mapped into address space of the CPU
		- Example: graphics controller
		- Transfer of millions of byte: faster to write them directly into memory than to issue millions of I/O instructions for

Device I/O Port Locations on PCs(partial)

| I/O address range(hexadecimal) | device                    |
| ------------------------------ | ------------------------- |
| 000-00F                        | DMA controller            |
| 020-021                        | interrupt controller      |
| 040-043                        | timer                     |
| 200-20F                        | game controller           |
| 2F8-2FF                        | serial port(secondary)    |
| 320-32F                        | hard-disk controller      |
| 378-37F                        | parallel prot             |
| 3D0-3DF                        | graphics controller       |
| 3F0-3F7                        | diskette-drive controller |
| 3F8-3FF                        | serial port(primary)      |


__I/O Port Registers__
- Four categories for I/O port registers
	- Data-in registers
	- Data-out registers
	- Status registers
		- Host reads status, such as whether the current command has completed, whether a byte is available to be read, whether an error has occurred
	- Control registers
		- Host writes to start a command or to change the mode of a device

__Communication btw Host & Controller__
- Handshaking communication
	- ![[Pasted image 20240508124313.png|300]]
	- Complete protocol for interaction between host and controller is intricate, but its basic handshaking notion is simple
	- Host ’s writing a byte through a port
		1. Host repeatedly reads “busy” bit until it becomes clear
		2. Host sets “write” bit in the “command” register and writes a byte into “data-out” register
		3. Host sets “command-ready” bit
		4. When controller notices “command-ready” bit, it sets “busy” bit
		5. Controller reads “command” register, reads “data-out” register to get the byte, and does I/O to the device
		6. Controller clears “command-ready” bit, “error” bit (indicating successful I/O operation), and “busy” bit

__Polling__
- The previous loop is repeated for each byte
- In step 1, host is busy-waiting or polling
	- The basic polling operation is efficient
		- Can be done only with three CPU-instruction cycles
	- But polling becomes inefficient when it rarely finds a device to be ready
		- Then it may be more efficient to arrange for the controller to notify CPU when it becomes ready

__Interrupts__
- Hardware mechanism for interrupt
	- CPU has interrupt-request line that it senses after executing every instruction
	- I/O device controller raises an interrupt by asserting a signal on the line
	- CPU catches the interrupt and dispatches it to the interrupt handler
		- Interrupt handlers are usually device drivers(using Interrupt vector table to reach it)
		- We make Interrupt vector table when we boot the system
	- Handler clears the interrupt by servicing the device
- How to service interrupts: immediately or later
	- CPU often has two interrupt request lines
	- Non-maskable for urgent interrupts
	- maskable to ignore or delay some interrupts (I/O devices) to do some critical processing without any interrupts

__Inerrupt-Driven I/O Cycle__
- ![[Pasted image 20240508124415.png|500]]


__Direct Memory Access__
- Programmed I/O (PIO)
	- Task of watching status bits and feeding data into control register one byte at a time
	- Wasteful for an expensive general-purpose CPU to do PIO for large data movement, i.e., with a disk drive
- DMA Controller (Direct-Memory-Access)
	- Special-purpose processor(device) that transfers data directly between memory and I/O device bypassing CPU
	- It offloads the burden of CPU to do PIO for large transfer

__6 Step Process to Perform DMA Transfer__
- ![[Pasted image 20240508124512.png|500]]

# Abstraction for Multi-Device sound (loudspeaker) coordination for 5.1ch surround sound reproduction

 - Many home theater systems require pre-defined speaker layouts for better sound experience
 - If sound arrival time is less than 1ms then people recognizes as a same sound.
 - If bigger then we recognize it as a different sound
 - Goal: provide an illusion that MMA applications run over conventional loudspeaker configurations in mobile environments

__Moblie Maestro: Challenges__
- For high quality sound reproduction, Devices should be synchronized in terms of sound arrival time and level


# Virtualization 

__Concept of Virtualization__
- The common theme of all virtualization technologies is the hiding of technical detail, through encapsulation,
	- by multiplexing access
		- a single physical resource appears to function as multiple logical resources
	- by combining multiple physical resources as a single logical resource
	- by simplifying the control of resources (even in one-to-one
- Abstraction
	- by multiplexing access
		- a single physical resource appears to function as multiple logical resources
	- by combining multiple physical resources as a single logical resource
- “(OS) Virtualization” refers to the creation of a virtual machine
- A virtual machine is a software implementation of a machine (i.e., a computer) that executes programs like a physical machine

__Terminology__
- “Virtual machine” is a loaded term
	- E.g. Java Virtual Machine refers to a runtime environment (software) that can execute Java bytecode
- “VM” is a loaded abbreviation
	- JVM (Java Virtual Machine), Virtual Memory
- For our purposes, we will talk about Virtual Machine Monitors (VMM)
	- VMM is software that allows multiple guest OSes to run concurrently on one physical machine
		- Each guest runs on a virtual machine
	- VMM is sometimes called a hypervisor

__Virtual Hardware Examples__
- VMM exports a simple disk interface
	- Reads/writes are translated to a virtual filesystem on the real disk
		- Just like Pintos on QEMU
- Simple network interface
	- VMM acts like a NAT, multiplexing packets to and from multiple guests

__Virtualization Architecture__
- Type 1 (native/bare-metal)
	- Hypervisor runs directly on the host’s hardware to control the hardware and to monitor guest OSes. A guest OS runs on another level above the hardware
- Type 2 (hosted)
	- Hypervisor runs within a conventional operating system environment. (with in “Host OS”)

__Goal of Virtualization__
- Popek and Goldberg, 1974
1. Fidelity (Transparency): software on the VMM executes identically to its execution on hardware
	- Except for timing effects
2. Performance: A majority of guest instructions are executed by the hardware without VMM intervention
	- Counterexample: the JVM
3. Safety: the VMM manages all hardware resources
	- Guests cannot impact each other

__Advantages of Virtualization__
- Compatibility and functionality
	- Guests are oblivious to low-level hardware changes
	- Windows apps on Linux or vice-versa
- Consolidation
	- Multiple machines can be combined into one by running the OSes as guests
- Isolation, security and reliability of applications
	- A virtual machine for each (potentially untrusted) app
	- If a virtual machine crashes, all others are unaffected.
	- Data does not leak across virtual machines
- Checkpointing and migration
	- A guest OS can be written to disk or sent across the network, reloaded later or on a different machine
- OS debugging
	- Crash on developing OS do not (typically) affect Host OS
	- Debug : Memory dumps, CPU Registers, Serial / Parallel Port dumps
- Multiplatform debugging
	- App writers often target multiple platforms
		- E.g. Android, Windows, and Linux
	- Would you rather debug on three separate machines, or one machine with two guests?

__Cloud Computing__
- Cloud computing
	- The delivery of various computing services over the internet, allowing users to access and use computing resources without owning and maintaining physical hardware and infrastructure.
		- These services include storage, processing power, databases, networking, software, and more.
- Similar to the electricity grid
- Cloud computing takes virtualization to the next step
	- You don’t have to own hardware.
	- You can “rent” it as needed from a cloud.
	- Public cloud
		- e.g. Amazon EC2.
	- Also a company can create a private cloud.

__Types of virtualization__
- Full Virtualization
	- No Guest OS modification
	- Software approach
		- Binary translation
		- VMware
	- Hardware-assisted Virtualization
		- New privilege mode
- Paravirtualization
	- Guest OS modification
	- Software approach
		- Hypercalls
		- Xen

## x86 Virtualization

__Classic Virtualization__
- Popek and Goldberg’s Criteria:
	1. Fidelity (Transparency) – run any software
	2. Performance – run it fairly fast
	3. Safety – VMM manages all hardware
- Trap-and-Emulate: a real solution that supports the above criteria

__Trap-and-Emulate Virtualization__
Important ideas from Trap-and-Emulate Virtualization
1. De-Privilege OS
	- Executes guest operating systems directly but at lesser privilege level, user-level
	- Instructions that read or write privileged state – trap
	- VMM intercepts the trap and emulates the trapping instruction against the virtual machine state

__Virtual Hardware Examples__
- VMM exports a simple disk interface
	- Reads/writes are translated to a virtual filesystem on the real disk
		- Just like Pintos on QEMU

__Classic VMM: Primary and Shadow structures__
- Privileged state of each guest differs from that of the underlying hardware
- Basic function of VMM is to meet guest’s expectation
- To accomplish this VMM derives shadow structures from guest-level primary structures
	- Primary structures reflect the state of guest
	- VMM-level shadow structures are copies of guests primary structures
- These structures are kept coherent using – memory tracing

__Classical VMM: Memory Tracing__
- On-CPU privileged state – handled trivially
	- Includes page table pointer register, processor status register, etc
	- Guest access to these registers coincide with trapping instructions
	- On trap, VMM refers to the corresponding shadow of the guest register structure in the instruction emulation
- Off-CPU privileged data
	- Guest access to these does not coincide with trapping instructions
	- Example : Guest PTEs are considered privileged data – but, accessing this is not accompanied by traps
	- They can be modified by shadow structures of PTEs
	- VMM cannot maintain coherency of shadow structures
- VMMs use hardware page protection mechanisms to trap access to in memory primary structures – memory tracing

__Classic VMM : Memory Tracing Example__
- Guest PTEs for which shadow PTEs are constructed may be writeprotected
- Guest access to these cause traps (tracing faults)
- VMM decodes the faulting guest instruction, emulates its effect on primary structure and propagates the change to shadow structures
	1. De-Privilege OS
	2. Shadow structures and memory tracing

__Problem: How to Virtualize the MMU?__
- On x86, each OS expects that it can create page tables and install them in the cr3 register
	- The OS believes that it can access physical memory
- However, virtualized guests do not have access to physical memory
- Using trap (or binary translation), the VMM can replace writes to cr3
	- Store the guest’s root page in the virtual CPU cr3
	- The VMM can now walk to guest’s page tables
- However, the guest’s page tables cannot be installed in the physical CPU…

__Guest’s Page Tables Are Invalid__
- Guest OS page tables map virtual page numbers (VPNs) to physical frame numbers (PFNs)
- Problem: the guest is virtualized, doesn’t actuallyknow the true PFNs
	- The true location is the machine frame number(MFN)
	- MFNs are known to the VMM and the host OS
- Guest page tables cannot be installed in cr3
	- Map VPNs to PFNs, but the PFNs are incorrect
- How can the MMU translate addresses used bythe guest (VPNs) to MFNs?

__Shadow Page Tables__
- Solution: VMM creates shadow page tables thatmap VPN → MFN (as opposed to VPN→PFN)

__Building Shadow Tables__
- Problem: how can the VMM maintain consistentshadow pages tables?
	- The guest OS may modify its page tables at any time
	- Modifying the tables is a simple memory write, not a privileged instruction
		- Thus, no helpful CPU exceptions :(
- Solution: mark the hardware pages containing the guest’s tables as read-only
	- If the guest updates a table, an exception is generated
	- VMM catches the exception, examines the faulting write, updates the shadow table

__Dealing With Page Faults__
- It is possible that the shadow table may be inconsistent
- If a guest page faults, this could be a:
	- True miss: actual page fault
	- Hidden miss: the shadow table is inconsistent; there is a valid VPN→PFN mapping in the guest’s page tables
- VMM must disambiguate true and hidden misses
	- On each page fault, the VMM must walk the guest’s tables to see if a valid VPN→PFN mapping exists
	- If so, this is a hidden miss
		- Update the shadow table and retry the instruction
	- Otherwise, forward the page fault to the guest OS’s handler

__Pros and Cons__
- The good: shadow tables allow the MMU to directly translate guest VPNs to hardware pages
	- Thus, guest OS code and guest apps can execute directly on the CPU
- The bad:
	- Double the amount of memory used for page tables
		- i.e. the guest’s tables and the shadow tables
	- Context switch from the guest to the VMM every time a page table is created or updated
		- Very high CPU overhead for memory intensive workloads 

__More VMM Tricks__
- The VMM can play tricks with virtual memory just like an OS can
- Paging:
	- The VMM can page parts of a guest, or even an entire guest, to disk
	- A guest can be written to disk and brought back online on a different machine!
- Shared pages:
	- The VMM can share read-only pages between guests
	- Example: two guests both running Windows XP 

__Trap-and-Emulate (cont.)__
- Traps are expensive (~3000 cycles)
- Important enhancements
	- “Paravirtualization” to reduce traps (e.g., Xen)
		- Modify guest OS to provide higher-level information to VMM
		- Approach relaxes Popek and Goldberg’s fidelity requirement
		- But gains in performance Virtual Machines 10
	- Hardware VM modes (e.g., IBM s370)

__Can x86 Trap and Emulate?__
- No
	- Even with 4 execution modes!
	- Key problem: dual-purpose instructions don’t trap
- Classic Example: popf instruction
	- Same instruction behaves differently depending on execution mode
	- User Mode: changes ALU flags
	- Kernel Mode: changes ALU and system flags
	- Does not generate a trap in user mode 

![[Pasted image 20240527131554.png|250]]
__Protected Mode__
- Most modern CPUs support protected mode
- x86 CPUs support three rings with different privileges
	- Ring 0: OS kernel
	- Ring 1, 2: device drivers
	- Ring 3: userland
- Most OSes only use rings 0 and 3

__Software VMM: To overcome obstacles on x86__
![[Pasted image 20240527131638.png|300]]
- Execute guest on Interpreter
	- But fetch-decode-execute cycle of interpreter reduces performance
- Binary Translation of the guest
	- VMM can switch between BT mode and direct execution mode
	- Privileged instructions are changed to function calls to code in VMM

__Binary Translation (VMWare)__
- Characteristics
	- Binary – input is machine-level code
	- Dynamic – occurs at runtime
	- On demand – code translated when needed for execution
	- System level – makes no assumption about guest code
	- Only need to translate OS code
		- Makes applications run fast by default
	- Most instruction sequences don’t change
	- Instructions that do change:
		- Indirect control flow: call/ret, jmp
		- PC-relative addressing
		- Privileged instructions

__Binary Translation Example__
- Guest OS Assembly
```
do_atomic_operation:
cli
mov eax, 1
xchg eax, [lock_addr]
test eax, eax
jnz spinlock
…
…
mov [lock_addr], 0
sti
ret
```
- Translated Assembly
```
do_atomic_operation:
call [vmm_disable_interrupts]
mov eax, 1
xchg eax, [lock_addr]
test eax, eax
jnz spinlock
…
…
mov [lock_addr], 0
call [vmm_enable_interrupts]
ret
```

__Pros and Cons__
- Advantages of binary translation
	- It makes it safe to virtualize x86 assembly code
	- Translation occurs dynamically, on demand
		- No need to translate the entire guest OS
	- App code running in the guest does not need to be translated
- Disadvantages
	- Translation is slow
	- Wastes memory (duplicate copies of code in memory)
	- Translation may cause code to be expanded or shortened
		- Thus, jmp and call addresses may also need to be patched

__Caching Translated Code__
- Typically, VMMs maintain a cache of translated code blocks
	- LRU replacement
- Thus, frequently used code will only be translated once
	- The first execution of this code will be slow
	- Other invocations occur at native speed

__Virtualization Performance__
- Guest code executes on the physical CPU
- However, that doesn’t mean its as fast as the host OS or native applications
	1. Guest code must be binary translated
	2. Shadow page tables must be maintained
	- Page table updates cause expensive context switches from guest to VMM
	- Page faults are at least twice as costly to handle 

__Hardware Techniques__
- Modern x86 chips support hardware extensions designed to improve virtualization performance
1. Reliable exceptions during privileged instructions
	- Known as AMD-V and VT-x (Intel)
	- Released in 2006
	- Adds vmenter/vmexit instructions (like sysenter/sysret)
	- allows classic trap-and-emulate
1. Extended page tables for guests
	- Known as RVI (AMD) and EPT (Intel)
	- Adds another layer onto existing page table to map PFN→MFN

__AMD-V and VT-x__
- Annoyingly, AMD and Intel offer different implementations
- However, both offer similar functionality
- vmenter: instruction used by the hypervisor to context switch into a guest
	- Downgrade CPU privilege to ring 3
- vmexit: exception thrown by the CPU if the guest executes a privileged instruction
	- Saves the running state of the guest’s CPU
	- Context switches back to the VMM

__Configuring vmenter/vmexit__
- The VMM tells the CPU what actions should trigger vmexit using a VM Control Block (VMCB)
	- VMCB is a structure defined by the x86 hardware
	- Fields in the struct tell the CPU what events to trap
	- Examples: page fault, TLB flush, mov cr3, I/O instructions, access of memory mapped devices, etc.
- The CPU saves the state of the guest to the VMCB before vmexit
	- Example: suppose the guest exits due to device I/O
	- The port, data width, and direction (in/out) of the operation get stored in the VMCB

__Benefits of AMD-V and VT-x__
- Greatly simplifies VMM implementation
	- No need for binary translation
	- Simplifies implementation of shadow page tables
- Warning: the VMM runs in userland, but use of AMD-V and VT-x requires ring 0 access
	- Host OS must offer APIs that allow VMMs to configure VMCB and setup callbacks for guest OS exceptions
	- Example: KVM on Linux

__Problem with AMD-V and VT-x__
- Some operations are much slower when using vmexit vs. binary translation

__Benefits of AMD-V and VT-x__
- Greatly simplifies VMM implementation
	- No need for binary translation
	- Simplifies implementation of shadow page tables
- … however, sophisticated VMMs still use binary translation in addition to vmenter/vmexit
	- VMM observes guest code that causes frequent vmexits
	- Hot spots may be binary translated or dynamically patched to improve performance
	- Similar to Just-In-Time (JIT) compilation

__Second Level Address Translation__
- AMD-V and VT-x help the VMM control guests
- … but, they don’t address the need for shadow page tables
- Second level address translation (SLAT) allows the MMU to directly support guest page tables
	- Intel: Extended Page Tables (EPT)
	- AMD: Rapid Virtualization Indexing (RVI)
	- Also known as Two Dimensional Paging (TDP)
	- Introduced in 2008

__SLAT Implementation__
- VMM installs first and second level tables in the MMU
	- Context switch to the guest via vmenter
- Steps to translate an address:
	1. MMU queries the level 1 (guest) table
	2. MMU queries the level 2 (VMM) table
- If any step yields an invalid PTE then page fault to the VMM (vmexit)

__Advantages of SLAT__
- Huge performance advantages vs. shadow page tables
- When guests mov cr3, the CPU updates vmcr3 register
	- No need to vmexit when guest OS switches context
- EPT can be filled on-demand or pre-initialized with PFN→MFN entries
	- On-demand:
	- Slower, since many address translations will trigger hidden misses
	- … but hardware pages for the guest can be allocated when needed
	- And, the EPT table will be smaller
- Preallocation:
	- No need to vmexit when the guest OS creates or modifies it’s page tables
	- … but hardware pages need to be reserved for the guest
	- And, the EPT table will be larger

__Disadvantages of SLAT__
- Memory overhead for EPT
	- … but not as much as shadow page tables
- TLB misses are twice as costly
	- SLAT makes page tables twice as deep, hence it takes twice as long to resolve PTEs

__EPT Performance Evaluation__
- Microbenchmarks by the VMWare team
- Normalized to shadow page table speeds (1.0)
	- Lower times are better

# FLUID: Enabling next-generation multi-device paradigm

__Multi-device Computing Model__
- Transparent cross-device resource sharing
	- allows an app executing on one device to use resources on another device transparently
		- physical resources: camera, sensors, etc
		- logical(app) service: login, browsing, PDF viewer, etc

__What does FLUID do?__
- Partitions an app at the unit of UI, distributes UIs across different devices, and runs each UI simultaneously on different devices

__Existing solutions__
- Customized apps
	- Extra engineering efforts
	- Low applicability
- Screen mirroring
	- Low flexibility
		- Supports only full screen
	- Low responsiveness(for higher resolutions)
- App migration
	- Low flexibility
		- Supports only full screen
		- Cannot support concurrent usage

__Goal__
- Design a new mobile platform that supports multi-device computing by distributing UI objects to different devices in a flexible, transparent and responsive manner

![[Pasted image 20240529140154.png|500]]
__FLUID overview__
- Key idea: separation between app logic & UI parts
	- Distributing target UI objects to remote devices and rendering them
	- Giving an illusion as if app logic and UI objects were in the same process by extending intra-app interaction to multi-device environments

__Why is FLUID good?__
- Flexibility
	- Allows users to interact with multiple devices, via fine-grained UI distribution, with maximum flexibility
- Transparency
	- Support legacy apps without any modification
	- Develop new multi-surface apps under the existing programming model
- Responsiveness
	- Require less network transmission when moving UIs instead of full screen

__Problems__
- How to maintain interaction between app logic & UI objects?
	- Such interaction is achieved via local function calls
	- However, local functions cannot be executed across devices
	- Our solution: transparent RPC transformation in Andriod VM (ART)
		- ![[Pasted image 20240529140620.png|400]]
- How to split & distribute UI objects?
	-  ![[Pasted image 20240529140906.png|400]]
	- We aim to minimize the amount of network transfer(graphical states) needed for UI rendering to reduce network overhead
	- However, for some app-specific custom UIs, it is not easy to precisely determine which graphical states are used
	- Our solution: selective UI distribution

__Limitation of FLUID: No cross-platfrom support__
- Multi-device environment often consists of heterogeneous devices
	- Where different device types typically have different major platforms
- FLUID only support UI distribution between Andriod devices

__Goal: FLUID + XP__
- Design a mobile platform that supports multi-device interaction by distributing UIs to different devices
	- In flexible, transparent and responsive manner
	- Also with cross platform support

![[Pasted image 20240603132527.png|500]]
__FLUID-XP overview__
- Key idea: UI Tree partitioning & Subtree streaming
	1. Separate Target UIs fro the original UI Tree
	2. Render the partitioned subtree on a virtual display
	3. Stream the pixels of virtual display to guest device's wrapper app

__FLUIDGPT: GPT-based Autonomous App Execution__
![[Pasted image 20240603135202.png|500]]

