- ### Course Info
	- Course Number: 404241
	- CW page: https://cw.sharif.edu/course/view.php?id=10984
	- Professor: [Hossein Asadi](http://sharif.edu/~asadi/)
	- Units: 3
	- Source book: ![Operating System Concepts](../assets/Abraham_Silberschatz_Peter_B_Galvin_Greg_Gagne_-_Operating_system_concepts-Wiley_(2012)_1669592582873_0.pdf)
- ## Introduction
	- Slides: ![Lecture1-intro.pdf](../assets/Lecture1-intro_1669592229275_0.pdf)
- ## OS Structure
	- Slides: ![Lecture2-os-structure.pdf](../assets/Lecture2-os-structure_1669592272306_0.pdf)
	- Chapter in book: ((6383f67f-f470-4181-9fb1-a0c88e89ce14))
- ## Process
	- Slides: ![Lecture3-process.pdf](../assets/Lecture3-process_1669592302014_0.pdf)
	- Chapter in book: ((6383f6f9-b367-4d7f-af48-f044aaf0aac1))
	- ### Process Concept
	  collapsed:: true
		- **Process**: a Program in Execution
		- Process execution **must** progress in **sequential**
		  fashion
		- System Processes:
			- **OS** processes executing **system code**
			- **User** processes executing **user code**
		- Multiple Parts:
			- Program code, also called **text section**
			- Current activity including **program counter** ,
			  processor registers
			- **Stack** containing temporary data
				- Function parameters, return addresses, local variables
			- **Data section** containing global variables
			- **Heap** containing memory dynamically allocated
			  during run time
		- **Program** is Passive Entity Stored on Disk
		  (executable file) but process is **active**
			- Program becomes process when executable file
			  loaded into memory
		- Execution of Program Starts via:
			- GUI mouse clicks
			- Command line entry of its name
		- **One Program** can be **Several Processes**
			- Consider multiple users executing same program
	- ### Process in Memory
	  collapsed:: true
		- ((6383fa12-2651-4fe7-b6d5-5055f8bf4a43))
	- ### Process States
		- ((6383fae3-f831-48a1-b792-30b5a3d6cc28))
		- **New**: Process is being created
		- **Running**: Instructions are being executed
		- **Waiting**: Process is waiting for some event to
		  occur
		- **Ready**: Process is waiting to be assigned to a
		  processor
		- **Terminated**: Process has finished execution
	- ### Process Control Block (PCB)
	  collapsed:: true
		- ((6383fc15-84e3-4bdd-b62a-9f559f606988))
		-
		- Info Associate with each Process:
			- Aka, task control block
		- Process State
			- Running, waiting, ready, new, & terminated.
		- Program Counter
			- Location of instruction to next execute
		- CPU Registers
			- Contents of all process-centric
			  registers:
				- GP registers
				- Stack register
		- CPU Scheduling Info
			- Priorities, scheduling queue pointers
		- Memory-Management Info
			- Memory allocated to process
			- Page or segment tables
		- Accounting Info
			- CPU used
			- Clock time elapsed since start
			- Time limits
		- I/O Status Info
			- I/O devices allocated to process
			- List of open files
	- ### Process Representation in Linux
	  collapsed:: true
		- **Doubly Linked List** of **Task_Struct**
			- Kernel Maintains a Pointer to Current Process
		- ((6383fc98-adac-46d6-b658-e3382a56b0f8))
	- ### Process Scheduling
		- #### Process Scheduler
			- Selects among available processes for next
			  execution on CPU
		- **Goals** of Process Scheduling:
			- Maximize CPU utilization
				- Quickly switch processes onto CPU for time sharing
			- Meet deadline of each process
				- In real-time applications
			- Meet fairness among processes
		- **Scheduling Queues**
			- **Job queue** – set of all processes in system
			- **Ready queue** – set of all processes residing in
			  main memory, ready, and waiting to execute
				- Pointers to the 1st and final PCB in the list
			- **Device queues**  – set of processes waiting for an
			  I/O device (one queue for each device)
		- Processes **Migrations** among Queues: **OS selects (schedules) processes in queues**
			- Job queue -> Ready queue
			- Device queue -> Ready queue
		- Representation:
			- Queuing Diagram represents queues,
			  resources, and flows
				- ((6383fe5b-daf1-462f-9c50-b54084d32c08))
	- ### Schedulers
		- **Short-Term (ST) Scheduler** (CPU Scheduler)
			- Selects which process should be executed next
			  and allocates CPU
			- Sometimes the **only** scheduler in a system
			- is invoked frequently (**milli-sec**) -> Must be fast
		- **Long-Term (LT) scheduler** (Job scheduler)
			- Selects which processes should be brought into
			  ready queue
			- is invoked infrequently (**sec~min**) -> May be slow
			- Controls degree of multiprogramming:
				- i.e., Determines number of processes in memory
			- **Steady-State**: long-term scheduler should be
			  invoked only a process leaves the system
				- Assuming degree of multiprogramming is stable
			- Processes:
				- **I/O-bound process** – spends more time
				  doing I/O than computations
				- **CPU-bound process** – spends more time
				  doing computations
			- Strives for Good **process mix**
				- All processes **I/O bound** -> **ready queue** will
				  almost always be **empty** -> **Short-Term (ST) Scheduler** idle
				- All processes **CPU bound** ->**I/O waiting queue** 
				  will almost always be **empty** -> **devices** idle
			- May be *Absent* or *Minimal* -> Can adversely affect performance -> users may quit and their processes are terminated
				- E.g., UNIX and Windows have no LT scheduler
				  and put every new process in memory
		- **Medium-Term Scheduler**
			- Used if Degree of Multi-Programming Needs to Decrease
			- **Swapping**: remove process from memory,
			  store on disk (***swapped out***), bring back in from
			  disk to continue execution (***swapped in***)
			- Used to improve **process mix**
			- ((638401e9-1fa3-4669-87dc-876dd2c646ab))
		-
			-
			-
	- ### Context Switch
		- Context of a Process Represented in PCB
		- When CPU Switches to another Process:
			- **System** must **save state** of old process -> **OS**, then, **loads** saved state for new process via a context switch
		- Context-Switch Time is Overhead:
			- System does **no useful** work while switching
			- **More complex** OS and PCB-> **longer** context
			  switch
			- **More** context **switching time** when using **VM**s
		- Time:
			- HW Support
				- Memory speed
				- Number of Registers in Register File
				- Special instruction to copy RF
					- Also, HW (micro-architecture) support
				- Some HW provides multiple sets of registers per
				  CPU -> multiple contexts loaded at once
					- Context switch: changing a pointer to a target RF
	- ### Operations on Processes
		- Process Identified and Managed via a **Process Identifier (pid)**
		- System must Provide Mechanisms for:
			- Process **Creation**
			  collapsed:: true
				- Parent Process Creates Children processes
					- What **Does** Child Process ***Inherits*** from Parent?
						- Privileges and scheduling attributes
						- Certain resources such as open files
					- What **Does not**  Child ***Inherits*** from Parent?
						- Parents memory locks
						- Parent’s timers
						- Semaphore’s adjustments and pending signals
				- **Resource Sharing** Options
					- Parent and children **share all resources**
					- Children **share subset of parent’s resources**
						- Prevents any process from overloading system by
						  creating too many sub-processes
					- Parent and child **share no resources**
				- **Execution Options**
					- Parent and children execute **concurrently**
					- Parent **waits** until **children terminate**
				- **Address Space**
					- Child duplicate of parent
					- Child has a new program loaded into it
				- UNIX Example:
					- ((638405f0-636e-4e41-b821-ab687cd70a83))
					- ``fork()`` ->  system call creates new process
						- Both processes continue execution at the
						  instruction after ``fork()``
						- Child gets unique process ID
						- Child’s PPID = parent’s PID
						- Reset child’s resource utilization and CPU time
						  counters
						-
					- ``exec()`` -> system call used after a ``fork()`` to
					  replace process’ memory space with a new
					  program
					-
					-
				-
			- Process **Termination**
				- Process Executes Last Statement -> asks OS to delete it (using ``exit()``) -> Returns status data from child to parent via ``wait()`` -> Process’ resources are de-allocated by OS
				- Parent may Terminate Execution of Children Processes Using ``abort()`` System Call (or ``TerminateProcess()`` in Win32)
				- Reasons to Terminate Child Processes:
					- Child has **exceeded** allocated resources
					- Task assigned to child is **no longer required**
					- **Parent is exiting** and **OS does not allow a child** to
					  continue if its parent terminates
					- etc
				- **Some** **OS**es do **not Allow** Child to Exists
					- if its parent has terminated -> If a process terminates, then all its children must
					  also be terminated called **Cascading termination** (All children, grandchildren, etc. are terminated)
					- Termination is initiated by OS
				- Parent process may **Wait** for **Termination of a Child** Process by Using ``wait()`` System Call
					- Returns Status Info and pid of Terminated Process
					- ((63840900-a844-456d-a254-b0688d0470ad))
					- Other Variations of Wait
						- ``waitid()``
						- ``waitpid()`` ->  Waits for specific child process
				- **Zombie** Process
					- If no **parent waiting** (did not invoke ``wait()``)
					- Process has completed execution but still has an entry in process table
					- Entry needed for possible reading of exit status by its parent
				- **Orphan** Process
					- **Parent terminated** without Invoking ``wait()``
					- In UNIX, any orphan process is immediately **adopted by “init” process**
					- A process can become orphan **intentionally** (to run a process indefinitely) or **unintentionally** (Process crash)
				- **Scenarios**:
					- Terminate **parent** process ->  **Reparenting**
					- Terminate **child** process -> **Zombie process**
			-
			-
	-
- ## Thread
	- Slides: ![Lecture4-thread.pdf](../assets/Lecture4-thread_1669592372464_0.pdf)
	- Chapter in book: ((6383f713-b0c4-42b7-b6bd-7e6ea46a9f9a))
- query-table:: true
  #+BEGIN_QUERY
  from A take B
  #+END_QUERY
-
-
-
-
-
- ## CPU Scheduling
  collapsed:: true
	- Slides: ![Lecture5-cpu-scheduling.pdf](../assets/Lecture5-cpu-scheduling_1669592386915_0.pdf)
	- Chapter in book: ((6383f725-0258-47e0-b227-1282c0343442))
	- ### Basic Concepts
		- Maximum CPU Utilization -> Obtained with Multiprogramming
		- #### CPU–I/O Burst Cycle
		  collapsed:: true
			- Process execution consists of a cycle of CPU execution and I/O wait.
			- CPU Burst followed by I/O Burst
			- Major Concerns
				- CPU burst Duration
				- CPU burst distribution
				- ((6398b5ed-7ce6-45e3-8b3f-1f91cbd1daac))
				-
	- ### CPU Scheduler
		- #### Short-Term Scheduler:
			- Selects from among processes in the ready queue, and allocates CPU to one of them.
				- Queue may be ordered in various ways -> Not necessarily a **FIFO**
		- #### CPU Scheduling Decisions When a Process:
			- 1. Switches from **running** to **waiting** state (for example, as the result of an I/O request or an invocation of wait() for the termination of a child process)
			- 2. Switches from **running** to **ready** state (for example, when an interrupt occurs)
			- 3. Switches from **waiting** to **ready** state ((for example, at completion of I/O)
			- 4. Terminates
		- #### Non-**Preemptive** Scheduling (aka, cooperating scheduling)
			- Scheduling only under case 1 and case 4
			- Used in Windows 3.x
			- Pros
				- Simple to implement
			- Cons
				- Low context switch flexibility
				- Process hogging very likely to happen
		- #### **Preemptive** Scheduling
			- Used in Win95/WinNT, Mac OS X
			- Pros
				- More flexibility in context switching
			- Cons
				- More complex to implement
				- More issues for implementation
					- access to shared data
					- preemption while in kernel mode
					- interrupts occurring during crucial OS activities
	- ### Dispatcher
		- The dispatcher is the module that gives control of the CPU to the process selected by the short-term scheduler. This function involves the following:
			- Switching context
			- Switching to user mode
			- Jumping to the proper location in the user program to restart that program
		- The dispatcher should be as fast as possible, since it is invoked during every process switch. The time it takes for the dispatcher to stop one process and start another running is known as the **dispatch latency**.
	- ### Scheduling Criteria
		- CPU utilization
		- Throughput
		- Turnaround time
		- Waiting time
		- Response time
	- ### Scheduling Algorithms
		- #### First-Come, First-Served Scheduling
			- With this scheme, the process that requests the CPU first is allocated the CPU first. The implementation of the FCFS policy is easily managed with a FIFO queue.
			- On the negative side, the average waiting time under the FCFS policy is
			  often quite long.
			- There is a **convoy effect** as all the other processes wait for the one big process to get off the CPU. This effect results in lower CPU and device utilization than might be possible if the shorter processes were allowed to go first.
		- #### Shortest-Job-First Scheduling
			- When the CPU is available, it is assigned to the process that has the smallest next CPU burst. If the next CPU bursts of two processes are the same, FCFS scheduling is used to break the tie.
			- is provably optimal in that it gives the minimum average waiting time for a given set of processes.
			- The real difficulty with the SJF algorithm is knowing the length of the next CPU request.
			- SJF scheduling is used frequently in long-term scheduling.
			- Although the SJF algorithm is optimal, it cannot be implemented at the level of short-term CPU scheduling. With short-term scheduling, there is no way to know the length of the next CPU burst.
				- The next CPU burst is generally predicted as an exponential average of the measured lengths of previous CPU bursts.
					- $$\tau_{n+1} =\ \alpha\ t_n\ \ +\ (1\ -\ \alpha)\ \tau_n$$
					- The value of $t_n$ contains our most recent information
					- while $\tau_n$ stores the past history.
		- #### Shortest-Remaining-Time-First
			- same as previous one but Preemptive.
		-
	-
-