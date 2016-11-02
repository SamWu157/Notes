9/26/2016

## OS Intro

### Purpose of an OS
* two primary jobs:
    1. Manage system resources (memory, file systems, network connections, etc.)
    2. Provide user applications a convenient interface for accessing these resources


### Resource Management
* OS must make sure two programs don't access same file at same time
* manage resources:
    * **Time**: program competing to use CPU time
    * **Memory**: program requires memory and may request more memory while running
    * **I/O Devices**: program often need to receive user input
    * **Network Interfaces**: programs communicate over the network


### Multiplexing
* Time Multiplexing: allowing each program a certain amount of time to access a resource before OS switches to another program
    * process scheduler: determines how long each program can use CPU
* Space Multiplexing: allowing each program a certain amount of space in a resource
    * running program is given a chunk of system's memory to use for execution


### Security
* OS has ability to access any running program, so sensitive info is easily obtained
* OS are common targets for attacks because they have so much control


### Before OS
* Konrad Zuse's Z3 computer: used vacuum tubes and supported floating point
* ENIAC: uses human as OS


### Early Computers
* Programmed manually by humans via plugboards/punch cards
* very small number of resources
* No networks, minimal I/O
* only ran a single program at a time


### Miniaturization
* Transistors


### Programming Advances
* programming languages and compilers provide abstraction over hardware


### Running Jobs
* Programmers could create software on punch cards


### Saving time with batches
* read a batch of punch cards to magnetic tape


### IBM System/360
* utilized integrated circuits
* allowed different computers to use the same software


### Multiprogramming
* OS partitioned memory in to multiple pieces and allow CPU to work on separate job while I/O processed


### Spooling
* Simultaneous Peripheral Operation On Line
* simplified loading and unloading batches
* OS used spooling to load new jobs from magnetic disk to empty partitions of memory to run when old jobs were finished


### Timesharing
* allowed multiple users to connect to a computer via an online terminal


### MULTICS
* could support hundreds of simultaneous timesharing users
* one large computer for a city and resident could simply plug in as needed


### UNIX
* Ken Thompson and Dennis Ritchie develop UNIX and C
* System V and BSD
* POSIX: standard for running programs on any UNIX system
* clones of UNIX: Minix and GNU


### GNU/Linux
* Richard Stallman created GNU as a free clone of UNIX
* Linux Torvald created Linux, a kernel
* Two were merged to create GNU/Linux OS
* usually packaged in to "distribuitions"


### CP/M
* Intel produced 8080 microprocessor in 1970's
* Gary Kidall developed OS called Control Program for Microcomputers(CP/M) that used 8080 with 8 inch floppy disks for storage


### DOS
* Bill Gates obtained rights to Disk Operating System(DOS)
* rebranded as MS-DOS and packaged with BASIC interpreter for IBM computers
* dominated IBM PC market


### Apple Computer
* Steve Jobs and Steve Wozniak founded Apple Computer, Inc to sell personal computers
* became successful and key rival to IBM and Microsoft
* late 1970's, Jobs visited Xerox PARC and saw the graphical user interface(GUI)
* led Jobs to develop GUI for their own os
* Microsoft developed Windows as GUI for MS-DOS


### Embedded/Mobile Operating Systems
* Internet of Things: many devices now contain computers
* All require os in some form
* os for mobile devices
* Some developers such as Microsoft and Google looking to merge the platforms, so single os cover both 

### Cloud Computing
* In 1980's there was drastic shift away from timesharing systems to personal computers
* Now experiencing reverse
* Cloud-based systems are effectively same as timesharing systems
* Users access resources in centralized, shared system from external terminals to perform tasks


9/28/2016

## Hardware and Concepts

### Von Neuman Architecture
* slide 1 picture


### Hardware Review
1. CPU
2. Memory
3. Video Controller
4. USB Controller
5. Storage Controller
6. Network Interface
* many of the components contained on single piece of hardware (motherboard or mainboard)


### The processor
* Central Processing Unit(CPU): "brain" of the computer
    * responsible for executing instructions specified in software running on machine
* For each instruction executed, CPU must perform an _instruction cycle_


### Fetch Cycle
1. CPU reads address of next instruction from program counter(PC)
2. instruction is read from memory to instruction register(IR)
3. PC is updated for the next instruction

### Execute Cycle
1. CPU decodes instruction loaded in IR
2. Based on contents(opcode, registers, etc.) CPU performs various actions
3. register or memory contents may be read/modified during execution
4. Pipelining makes this overall process more complex

### Status registers
* CPU maintains register know as status register
* Normally user applications cannot modify entire register but can read contents and modify some portion
* utilized during system calls and I/O
* In x86, FLAGS, EFLAGS, and RFLAGS


### Execution Modes
* two execution modes: _user mode_ and _kernel mode_
* CPU's status register controls which mode is being used
* kernel mode: CPU can execute all instructions and fully utilize hardware
    * OS runs in kernel mode
* user mode: only a subset of instructions and hardware features are accessible
    * user programs run in user mode


### System Calls
* switches CPU out to operating system which is running in kernel mode
* often done with TRAP instruction
* control is returned to user program after OS performed necessary work


### Memory
* system memory contains both instructions and data for all running processes
    * Random Access Memory(RAM): any memory address can be accessed in same amount of time
* running process wil utilize memory for data from both stack(function calls) and heap(dynamic allocation) as well as area of memory for instructions and static data
* CPU will maintain register values such as stack pointer(SP)


### Memory hierarchy
1. CPU registers(1 nanosecond, less than 1KB)
2. CPU cach(2 nanosecond, roughly 1 MB)
3. Main memory(10 nanosecond, roughly 1 - 10 GB)
4. Secondary storage(10 milisecond, roughly 1 TB)

### CPU cache
* split in to several layers: L1, L2, L3, etc.
* L1 will be faster but smaller and more expensive
* layers may be split into separate instruction and data cache because instructions and data are accessed in different ways


### Magnetic Disk Storage
* most popular form of secondary storage
* generally called hard disks or hard drives
* orders of magnitude slower, cheaper, and larger than main memory
* function by rotating platters at thousands of RPM with a read/write head for each surface
* Data is written to platter in concentric circles
* platters are separated in to _sectors_ that are usually 512 bytes each
* several miliseconds to access hard disk


### Virtual Memory
* contents of RAM are split into pages that are written back to secondary storage to make space for other data
* CPU uses memory management unit that must remap memory addresses to convert between address referenced in process to actual physical address where data is stored
* in Linux: _swap space_


### I/O devices
* to access, computer will have controller for device
* controller: piece of hardware that physically controls the connected device
* OS will communicate with controller when accessing device
* device will respond to controller and perform actions requested
* To utilize controller: OS requires a _device driver_
* driver is piece of software that is provided by manufacturer of controller and placed in OS


### Device drivers
* Each device controllers has a set of registers used for communication with the OS
    * e.g. disk controller will have registers indicating the disk address, memory address, and whether to read or write data
    * device drive will write to these registers
    * may be special I/O instructions for reading or writing these registers depending on system


### I/O methods
* _busy waiting_: OS shifts control to driver to perform I/O and driver sits in loop polling the device register to verify when it has finished and then returns back to OS
    * simpliset way
    * wasteful
* _interrupt_: OS works on something else after starting I/O process and controller generates interrupt signal to OS that it has finished


### Buses
* _bus_: connection between two hardware components


### Booting the computer
* mainboard of system contains software called Basic Input/Output System(BIOS)
* first job when computer boots up is to perform a Power On Self Test(POST) of hardware
    * when successful, BIOS determines which storage device contains instructions needed to load computer's OS
        * once _boot device_ is determined, BIOS will read first sector into memory and execute instructions found there
            * contains code called _boot loader_ which will have ability to load rest of OS


### Processes
* a program that is currently being executed on machine
* every process has an _address space_ in memory where process is allowed to read or write
* each process also has list of associated resources that include registers such as program counter/stack pointer, any open files, related process, etc.
* a container that should have all of the info required to run that program


### Process management
* OS manages which process has access to resources including time to execute on CPU
* process can be in one of three states:
    1. Running
    2. Blocked
    3. Ready
* running process switched to blocked if it needs to wait for I/O
* OS will choose a ready process and begin running it
* blocked process can then become ready when I/O finishes
* running process might switch to ready if OS decides it has executed long enough and forcefully swaps it with another


### Process table
* OS maintains _process table_ to manage processes
* process table: an array that contains entries for each process on the system
* when process is switched out, all register contents and resources such as which files are open must be recorded
    * information is stored in process table entry for that process
* process that has been suspended so another can execute consists of its process table entry along with its address space in memory(called _core image_)


### Process hierarchy
* process may have ability to run additional processes resulting in a tree structure representing a root process calling _child processes_ which may also call additional processes
* _interprocess communication_: process often need to communicate with each other


### Address Space
* Moder OS partitions computers' memory into separate address space for each process
* Internally, process might all reference the same addresses, but OS can translate to actual physical addresses using MMU(Memory management unit)
* most OS also utilize virtual memory to extend size of system's memory


### Files
* File systems are generally formed as tree structure
* will have a root directory(/ in Unix-like systems)
* each directory can contain subdirectories or files
* file system also manage permissions for each file and directory so only authorized users can access them


### Process and files
* every process has notion of its _working directory_
* Any relative path(does not start with /) is resolved based on process' working directory
* in order to read/write a file, process must _open_ it
* if OS allows(might not if file is already open), it returns back a _file descriptor_ which is an integer value
* process will use file descriptor in any subsequent operations for that file


### File systems
* in Unix-like OS, file-system must be _mounted_ first to access a file system
    * can be done with file systems stored on hard disk, CD, USB, flash drive, etc.
* In Windows, each file system can be referenced by first specifying an identifying driver letter then path to file
* Unix-like systems, only a single root directory and new file systems are mounted as branches beneath root directory


### Special files
* Unix-like systems have notion of _special files_
* not actual files, but virtual files created by OS to refer to I/O devices or convenient things like a file that is an endless stream of random numbers
* _block special files_ and _character special files_
* block special files: act as if they are block devices such as hard disks
* character special files: provide a character stream


### Pipes
* another "psudofile" related to both files and processes
* used to connect two process together
* One process can write to a pipe while another can read from it
* each process accesses the pipe as if it was a normal file


### Main concepts
* operating system acts as bridge between hardware and user programs
* must manage resources of system for all running programs
* running programs encapsulated in processes, which exist in OS's process table
* OS must manage address space for each process
* To access secondary storage, user program will utilize file system and OS will translate to a form hardware can understand via controller and device driver


10/03/2016

## Processes

### Processes
* instance of a program currently being executed by a computer
    * include instructions to execute, register contents, and open resources for that process
* CPU must switch between processes


### Multiprogramming
* concept of a single CPU switching between process so each one is given execution time


### Process switching
* depending on OS, process priority, etc., rate that a process performs computation will not be uniform
* if executing same program later may not be possible to reproduce the same execution time
* So it is important that programs are not written with assumptions about execution time


### Program vs. process
* _program_: specifies an algorithm in a form that can be understood by CPU
* _process_: some kind of activity that includes a program, input, output, and state information
* One physical CPU is shared by many processes and there is some scheduling algorithm that will determine when a process can have time to execute
* program is simply set of instructions stored first on disk(secondary storage) and eventually in RAM(main memory) for each process that corresponds to it
* same program can be running many times simultaneously and each one has a _different_ process


### Process creation
* four main events that cause a process to be created:
    1. System initialization
    2. Execution of process-creation system call by existing process
    3. User requests creating a new process(by entering command, clicking icon, etc.)
    4. initiation of batch job
* operation system is booted, will create many process for various tasks
* _foreground process_: interacts with users on the system
* _background process_: runs in the background often sleeping for long periods of time until a specific event triggers it to run
    * _dameon_
* running process can also issue system call to create new process
    * useful if computer has multiple CPUs and work can be parallelized
* user on system can also start program, which creates new process
* mainfram systems a batch job might be submitted that causes processes to be created to handle each job in batch
* every way of creating new process is the same: existing process will perform a system call to create new process
* In Unix-like systems, _fork_: system call that creates a new process
    * After performing fork system call, both process have same memory image, environment strings, and open resources
    * child will usually execute another system call, execve, which will run new program
    * split in these two steps to allow new child process to perform specific actions after fork but before launching new program
* On Windows, _CreateProcess_ is used to create new process
    * also loads appropriate program into that process
    * function has 10 different parameters which can include the program to execute, command line arguments being passed, security attributes, other settings, priority information, window settings, etc.


### Process termination
* once a process is created it will perform whatever job it has been designated and then eventually end under one of the following conditions
    1. Normal exit (voluntary)
    2. Error exit (voluntary)
    3. Fatal error (involuntary)
    4. Killed by another purpose (involuntary)
* usually a process terminates when it has finished its job
    * sends a system call indicating that it has finished
    * Unix-like system, exit
    * Windows, ExitProcess
    * process might also exit this way due to user choosing to exit via user interface
* might aslo choose to terminate if it has detected an error it cannot handle
    * results in voluntary exit, but due to error instead of success
* might also involuntarily exit due to a fatal error such as attempting to execute an illegal instruction, divide by zero, or access a memory location outside of its address space
* process might terminate if another process executes a system call telling the OS to kill the first process
* Unix, kill
* Windows, TerminateProcess
* to do either, originator must have necessary permission to kill target process
* in both Unix and Windows, when a process is killed all processes created by that process remain alive


### Process hierarchies
* when one process creates another, they become associated
* child process can also create other processes, forming a hierarchy
* In Unix, a process and all descendant processes form a process group
    * user sends a signal from the keyboard, signal is transmitted to all processes in the group that are associated with the keyboard
    * each process can then individually _catch_ the signal or ignore the signal


### Unix Initialization
* e.g. of process hierarchy, is when Unix is intialized
* First, a special process known as _init_ starts running
    * will read a file indicating how many terminals there are and forks a process for each terminal
        * those processes then wait for a user to login
            * if login is sucessful, login process will execute a _shell_ for accepting commands from the user
* as a result, all process in the system belong to the same tree with _init_ as the root


### Windows hierarchy
* no process hierarchy in Windows
* each process is separate, but when a child process is spawned the parent is given a special token called _handle_
* _handle_ allows the parent to control the child, but the handle can be passed from the parent to another process
* In Unix, a process cannot "disinherit" its children


### Process state
* Each process is independent, but sometimes processes must communicate in some way
* A process blocks when it cannot continue its work
* A process might also be ready to run but the OS has stopped it in order to allow another process to use the CPU
* first case: suspension is inherent to the problem
* second case: simply a technical limitation
* Three states a process can be in:
    1. Running (currently using the CPU)
    2. Ready (waiting to use CPU but stopped so another process can run)
    3. Blocked (unable to run until something else happens)
* The first two states are similar: processes in either one are ready and willing to use CPU
* Third case is different, regardless of CPU availability the process cannot run
* As a result the CPU would be idle if all processes were in the third state
* Of the four possible transitions for process state, the first is caused by the OS when it recognizes a process cannot continue running at the moment
* second and third transistions are managed by the process scheduler in the OS
* Transition 2 would occur when the scheduler decides it is time for a process switch
* Transition 3 would occur for the next process in the queue depending on the scheduling algorithm in use
* final transtion occurs when the reason for the process to become blocked has been resolved
    * process enters the queue to use the CPU again


### Conceptual model of process syste
| 0 | 1 | ... | n - 2 | n - 1 |
|-----------------------------|
| Scheduler                   |

### Implementing processes
* operating system maintains a _process table_ containing _process control blocks_ (table entries)
    * Each entry contains information about the process:
    * Process state
    * Program counter
    * Stack pointer
    * Memory allocations
    * Open resources
* The table entry must contain all info necessary to restart a process when moving back to the _running_ state


### Process table entries
| **Process Management**    | **Memory management**          | **File management** |
|---------------------------|--------------------------------|---------------------|
| Registers                 | Pointer to text segment info   | Root Directory      |
| Program counter           | Pointer to data segment info   | Working Directory   |
| Program status word       | Pointer to stack segement info | File descriptors
    |
| Stack Pointer             |                                | User ID             |
| Process State             |                                | Group ID            |
| Priority                  |                                |                     |
| Scheduling parameters     |                                |                     |
| Process ID                |                                |                     |
| Parent process            |                                |                     |
| Process group             |                                |                     |
| Signals                   |                                |                     |
| Time when process started |                                |                     |
| CPU time used             |                                |                     |
| Children's CPU time       |                                |                     |
| Time of next alarm        |                                |                     |

### System interrupts
* I/O interrupt: handled by hardware and a specific memory area, _interrupt vector_
* memory location contains address of the _interrupt service procedure_
1. Hardware stacks program counter, etc.
2. Hardware loads new program counter from interrupt vector
3. Assembly-language procedure saves register
4. Assembly-language procedure sets up new stack
5. C interrupt service runs (typically reads and buffers input).
6. Scheduler decides which process is to run next
7. C procedure returns to the assembly code
8. Assembly-language procedure starts up new current process.

### Multiprogramming performance
* Most processes will spend time waiting for I/O to occur
* if a process spends a fraction _p_ of its time waiting for I/O and the system has _n_ processes in memory, the probability that all _n_ processes are waiting for I/O at the same time is _p^n_
* CPU utilization = 1 - p^n
* n: _degree of multiprogramming_


### Summary
* _process_: primary abstraction in OS
* corresponds to an instance of running program
* created in several ways, but stems from existing process calling a system call to create another
* terminate either voluntarily or involuntarily depending on success/error
* OS maintains a process table to keep track of processes
* OS has a scheduler that determines when to run each process
* scheduler shifts processes between three states: running, blocked, ready


10/05/2016

## Threads

### Threads
* OS tracks all processes in system
* Traditionally, each process have an address space and a single _thread of control_
* modern OS allow several threads of control to exist for a single process
    * each thread shares the same address space but will be performing different instructions
* _thread_: a process within a process
* allow software developers to write programs that require performing multiple simultaneous actions without needing to run separate programs
* more "lightweight" than processes, easier to create and destroy threads within a process than create new processes to handle parallel tasks
* can be 10-100x faster
* useful on modern computers that have multiple CPUs


### Multi-threaded software
* insert pictures


### Process model vs. thread model
* process model: based on execution and resource grouping
* thread allow us to separate these two things
* process: a way to group resources together
* thread of execution: has program counter, stack, and registers
* Traditionally process would be combination of these two things
* Now we allow a process (group of resources) to contain multiple threads of execution
* threads are what get scheduled on CPU


### Process model vs. thread model
| **Per-process items**       | **Per-thread items** |
|-----------------------------|----------------------|
| Adress Space                | Program counter      |
| Global variables            | Registers            |
| Open files                  | Stack                |
| Child processes             | State                |
| Pending alarms              |                      |
| Signals and signal handlers |                      |
| Accounting information      |                      |

### Multithreading
* Threads are sometimes called _lightweight processes_
* _multithreading_: ability to have multiple threads in a single process
* Modern CPU have hardware support for threads which allow thread switching at a much faster rate than if it had to b done entirely in software
* Programming languages and environments also support threads
    * java.lang.Thread class
* threads can be in one of several states: running, blocked, ready, terminated
* transitions between thread states are the same as for process states
* memory allocations for function calls are handled on stack and each thread is executing functions independently, every thread has its own stack
* Processes generally start with a single thread
    * this thread can create new threads by calling a function indicating what should be executed in the new thread
    * in some systems, threads form a thread hierarchy similar to a process hierarchy
    * even without a hierarchy, original thread typically receives some thread ID associated to the newly created thread
    * After finishing a thread can call a function to exit


### Complications of multithreading
* become more complicated than single-threaded programming
* normally have to do with how threads share resources in the process
* if no resources are shared, each thread is effectively its own process


### POSIX threads
* To create multithread programs that are portable, IEEE created standard for threads in 1003.1c
* _Pthreads_: multithread programs that are portable, supported by most Unix systems
* standard defines over 60 functions
* Each Pthread has an ID, set of registers, program counter, and attributes such as stack size, scheduling parameters, etc.


### POSIX threads functions
| **Thread call** | **Description**                           |
|----------------------|------------------------------------------------------|
| Pthread_create       | Create a new thread                                  |
| Pthread_exit         | Terminate the calling thread                         |
| Pthread_join         | Wait for a specific thread to exit                   |
| Pthread_yield        | Release the CPU to let another thread run            |
| Pthread_attr_init    | Create and initialize a thread's attribute structure |
| Pthread_attr_destroy | Remove a thread's attribute structure                |

### POSIX threads example

    #include <pthread.h>
    #include <stdio.h>
    #include <stdlib.h>

    #define NUMBER_OF_THREADS 10

    void *print_hello_world(void *tid)
    {
        /* This function prints the thread's identifier and then exits */
        print("Hello World. Greetings from thread %d\n", tid);
        pthread_exit(NULL);
        
    } 

    int main(int argc, char *argv[])
    {
        /*The main program creates 10 threads and then exits */
        pthread_t threads[NUMBER_OF_THREADS];
        int status i;
        
        for(i=0;i<NUMBER_OF_THREADS;i++) {
            print("Main here. Creating thread %d\n", i);
            status = pthread_create(&threads[i], NULL, print_hello_world(void*i));
            if (status!=0) {
                printf("Oops. pthread_create returned error code %d\n", status);
                exit(-1);
            }
        }
        exit(NULL);
    }


### User space threads
* threads can be implemented either in user space, kernel space, or a mix of the two
* threads are implemented entirely in user space, the kernel has no idea the threads exist
* kernel sees only single-threaded processes to schedule
* possible to implement threads on OS that does not directly support them
* each process has its own _thread table_
* table acts like a process table in kernel for tracking just the threads for one process
* table is managed by _run-time system_ which exists in each process
* when a thread would become blocked, instead of performing a system call to tell the kernel, it would call a run-time system procedure so process can choose a different thread to execute
* Because it is all done within the process, it can be much faster than going to the kernel to perform a thread switch
* each process can implement its own scheduler in the run-time system
* drawbacks are dealing with _blocking system calls_
* _blocking system calls_: a system call that causes the process to block until a result is given
    * cause the entire process to block because the kernel doesn't know about the threads, but another thread in the process could have continued executing
    * can also be caused by page faults
* another problem, in user space there are no clock interrupts, so a thread must voluntarily give up the CPU to allow another thread in the process to execute


### Kernel space threads
* no run-time system is required and each process will not have its own thread table
* kernel will maintain a thread table in addition to the process table
* when one thread wants to create another, a system call will be used just as we used a system call to create a process
* calls that would block a thread are all implemented as system calls allowing the kernel to schedule a new thread to execute either from the same process or from a different process


### Threads in Java
* when JVM is started, one non-daemon thread is created called _main thread_
    * this thread will begin executing the main method of the program
    * this thread can start other threads using java.lang.Thread class
* To create a thread programmatically, create an instance of java.lang.Thread
* For a thread to execute, must specify what code it should execute
    * pass a java.lang.Runnable to Thread's constructor
* after creating Thread object, calling its start() method will cause a new thread to begin executing the run() method of the Runnable


### java.lang.Runnable
* Runnable is a simple interface that specifies one method
    public abstract void run();
* you inherit Runnable any time you have something that should be executed by a thread
* Runnable encapsulates code to run into an object


### Thread synchronization
* Java synchronized key word allows you to mark either a method or block as _synchronized_ given a specific lock
* when multiple threads are executing, only one thread is allowed to execute synchroized code at a time
* when that thread enters the synchronized code, it obtains a lock that prevents other threads from entering that code
* Other threads will block waiting for a chance to enter the synchronzied code
* any object can act as a lock for synchonized code
* for non-static method, the object calling the method acts as the lock
* for static method, the class object acts as the lock


10/05/2016

## Interprocess Communication

### Interprocess Communication
* processes need to communicate with each other
* system needs a way to properly handle this communication including when some processes need to wait for others
* Interprocess Communication (IPC)


### IPC issues
* three primary issues:
1. _how_ one process can provide info to another process
2. ensuring multiple processes do not conflict with each other while communicating
3. dealing with sequences of dependencies

### IPC with threads
* two of these issues are also thread communication issues
* first issue is very simple for threads: threads share an address space they can communicate directly
* Both of the other issues are challenging for threads
* threads must also make sure they do not conlict with each other
* threads must make sure they handle dependencies properly


### Shared storage
* sometimes processes or threads will share some common storage that each can read and write
* storage might be in main memory or be a shared file
* _print spooler_: handles communication between processes that need to print and the printer actually printing documents


### Print spooling example
* when a process needs to print a file, it will record the file name in a special _spooler directory_
* separate process known as _printer daemon_ will periodically check for files to print from this directory
* printer daemon will print the files and remove their names from the directory


### Race condition
* _race condition_: multiple processes read/write shared data and final result depends on which process runs first or last
* can be extremely difficult to debug
* often no problems will occur, but then results will be incorrect at seemingly random intervals


### Danger of race conditions
* 


### Avoiding race conditions
* when performing interprocess communication we must write our software to avoid race conditions
* the result in shared memory should not change based on which process gets to execute first
* _mutual exclusion_: need to prohibit more than one process from reading/writing this shared memory at a time
    * when one process is using shared memory, others are excluded from also using it


### Critical region
* To solve, recognize that processes do not always need to use shared memory
* Most of the time, each process is working independently on their own tasks
* The code where they make use of the shared memory is only a small portion of the entire program
* this part of code is known as _critical region_ or _critical section_


### Proper data sharing
* four requirements must be met to ensure that programs do not have problems with race conditions:
1. No two processes may be simultaneously inside their critical regions
2. No assumptions may be made about speeds or number of CPUs
3. No process running outside its critical region may block any process
4. No process should have to wait forever to enter its critical region

### Potential Solutions
* Peterson's algorithm


### Disable interrupts
* allow user processes to block interrupts when they enter a critical region then re-enable interrupts when they finish
* unattracive because it is not wise to give user processes the ability to disable interrupts
* what if process never re-enabled interrupts? System would effectively stall
* solution breaks requirement 2 because it assumes a single processor system
* with multiple processors, even with interrupts disabled on one another process could be using the second processor and entering its own critical region


### Lock variables
* solution involves having a single lock variable that can be set to either 0 (unlocked) or 1 (locked)
* when a process needs to enter its critical region, it will first check if the lock is set to 0 or 1
* if it is 0, the process will wait and periodically check for the variable to be set back to 0
* doesn't work


### Strict alteration
* a variable named turn will indicate whose turn it is to enter their critical region
* it will start initially at 0
* when process 0 needs to enter its critical region it will check the value and see it is 0 so it will enter
* when process 1 needs to enter its critical region it will check the value and see it is 0 so it will wait in a loop periodically checking the value (busy waiting)
* when process 0 finishes it will set turn to 1 so process 1 can enter
* doesn't work


### Peterson's solution
* Both the lock variable and strict alternation solutions break at least on of the four requirements we have
* solves two process mutual exclusion problem but it can work for more than two processes


    int turn;
    int interested[2];

    void enter_region(int process) {
        int other = 1 - process;
        turn = process;
        while (turn == process && interested[other]); // wait
    }

    void leave_region(int process) {
        interested[process] = false;
    }


TSL
* uses hardware to assist
* Modern CPUs may come with any instructions specifically designed for handling these scenarios
* example instruction
    * TSL RX, LOCK
* TSL stands for _Test and Set Lock_
* read value in memory at position LOCK storing the result in register RX while also saving a non-zero value in LOCK
* create an _atomic instruction_ for both checking the lock value and setting it
* prevents the problem of a process being switched out after it checks the lock but before it can write back a new value
* For multi-processor systems, the instruction would lock the memory bus while executing to prevent another CPU from also accessing the shared memory

    enter_region:
        TSL REGISTER, LOCK | copy lock to register and set lock to 1
        CMP REGISTER, #0   | was lock zero?
        JNE enter_region   | if it was not zero, lock was set, so loop
        RET                | return to caller; critical region entered

    leave_region:
        MOVE LOCK,#0       | store a 0 in lock
        RET                | return to caller


10/12/2016

## Interprocess Communication

### Efficiency problems
* two correct solutions: Peterson's algorithm and TSL
* However, a problem they share is that they utilize _busy waiting_
* when a process needs to enter its critical region it will sit in a loop continually checking to see if it is able to continue
    * waste a lot of CPU time


### Priority inversion problem
* two processes _H_ and _L_
* _H_ is high priority and _L_ is low priority
* The OS is designed so it will always run _H_ over _L_ if _H_ is ready
* _L_ is currently in critical region and _H_ is given time to run
* _H_ busy waits because _L_ is in critical region, but CPU won't bring _L_ back to the CPU because it thinks _H_ is ready
* _priority inversion problem_


### Sleep and wakeup
* to avoid problems called by busy waiting
* sleep: causes current process to block
* wakeup: takes one parameter (the id of the process to wakeup) and will cause a sleeping process to become ready to run again


### Producer-consumer problem
* two processes share a common, typically fixed-size buffer
* One process acts as the _producer_ putting data into the buffer
* The other process acts as the _consumer_ taking data from the buffer
* problems:
1. what does the producer do if it is trying to add to the buffer but the buffer is full?
2. What does the consumer do if it is trying to remove from the buffer but it is empty?
* when one of these occurs, that process can go to sleep until it is able to utilize the buffer


### Race condition
1. Consumer reads count = 0
2. Consumer is interrupted and pulled off CPU
3. Producer inserts into buffer, increments count
4. Producer sees count = 1, so it wakes up Consumer
5. Consumer isn't asleep, already in ready state so wakeup is ignored
6. Producer interrupted and consumer returns to CPU
7. Consumer sees count = 0 from previous time on CPU and goes to sleep
8. Producer eventually fills up buffer and goes to sleep
* both processes are asleep forever


### Possible solution
* store _wakeup waiting bit_
    * can be set to 1 when a process is woken up when it's not sleeping
    * if that process later goes to sleep and the bit is set, it can instead wake up immediately
    * Unfortunately, a single bit isn't sufficient in some situations with more processes


### Semaphores
* count the number of wakeup signals that have been sent
* can have value 0 if no wakeups are saved
* can also have positive value to indicate the number of pending wakeups
* two operations that act as generalizations of sleep and wakeup that we call down and up
* down operation checks to see if value is greater than 0
    * if it is, decrements the value and continues
    * if it is 0, the process goes to sleep without completing the two operation
    * done in an _atomic operation_ (single step that can't be interrupted)
* up operation increments the value of the semaphore
    * if any processes are sleeping on the semaphore, the system chooses on to wakeup and finish its original down operation
* Utilizing semaphores, we can solve the indefinite sleep problem in our producer-consumer code by preventing the wakeup signal from being lost


### Producer-consumer with semaphores

    #define N 100
    typedef int semaphore
    semaphore mutex = 1;
    semaphore empty = N;
    semaphore full = 0;

    void producer(void)
    {
        int item;

        while(TRUE) {
            item = produce_item();
            down(&empty);
            down(&mutex);
            insert_item(item);
            up(&mutex);
            up(&full);
        }
    }

    void consumer(void)
    {
        int item
        
        while (TRUE) {
            down(&full);
            down(&mutex);
            item = remove_item();
            up(&mutex);
            up(&empty);
            consume_item(item);
        }
    }
* code utilizez three semaphores:
1. full counts the number of slots in the buffer that are full and starts at 0
2. empty counts the number of slots that are empty and starts at N
* mutex acts as a _binary semaphore_ (a semaphore that starts with value 1 and is used by processes to control access to a critical region)
* to do this, each process calls down on the semaphore before entering the critical region and up after leaving


### Mutexes
* mutex: simplified semaphore that can only have two values: _locked_ and _unlocked_
* can be used for managing mutual exclusion to a shared resource
* when a process needs to access its critical region, it calls mutex_lock
* if the mutex is unlocked, the call completes and the process enters the critical region
* if the mutex is already locked, the caller blocks until the other process finishes and calls mutex_unlock
* Mutexes and semaphores are usually implemented with TSL instructions


10/17/2016

## Process Scheduling

### Scheduling
* modern systems use _multiprogramming_ to allow many proceses to execute simultaneously by switchng them in as other processes block
* Additionally, some systems will switch out processes after a certain amount of time has expired to give other processes a chance on the CPU
* In order to decide which process gets to run next, the operating system must use a _scheduler_
* scheduler will employ one of many possible _scheduling algorithms_


### Process behavior
* Processes do not generally use CPU all the time
* will alternate "bursts" of computing along with I/O, usually from a disk or across a network
* program often runs for a short time then needs to read from a file, then can continue running for a short time, then write to a file, etc.
* _compute-bound/CPU-bound_: processes spend most of their time using the CPU and a small amount of time waiting for I/O
* _I/O-bound_: processes spend the majority of their time waiting for I/O and a small amount of time using the CPU
* over time as CPUs get better, the general trend has been that processes tend to become more I/O-bound than CPU-bound


### When to schedule
* 
