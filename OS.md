# Module 1

**Module 1: Introduction to Operating Systems**

---

### **1. Introduction**
- **What is an Operating System (OS)?**
  - A program acting as an intermediary between a user and computer hardware.
  - Goals:
    - Execute user programs and simplify problem-solving.
    - Enhance convenience in using the computer system.
    - Ensure efficient hardware utilization.

---

### **2. Four Components of a Computer System**
The slide discusses the main components of a computer system, although specific details aren't provided in the extracted content.
![image](https://github.com/user-attachments/assets/a3534abf-05fc-46a9-99f7-4469cf2e56a2)

---

### **3. System Boot**
- **Booting:** The process of starting a computer by loading the kernel.
- **Bootstrap Program:**
  - Stored in ROM or EEPROM (firmware).
  - Locates and loads the kernel into memory, starting its execution.
  - Initializes system aspects.

---

**Computer System Organisation**:
![image](https://github.com/user-attachments/assets/c407f2a0-862e-4542-a49a-1febaaa5b7e1)

![image](https://github.com/user-attachments/assets/ca650027-65c1-494c-9cc0-ab28e7ec57f8)

### **4. OS Services**
Operating systems provide functionalities for both users and the system itself:
- **User-Focused Services:**
  - **User Interface (UI):** Can be CLI (Command Line Interface) or GUI (Graphical User Interface).
  - **Program Execution:** OS loads, executes, and manages program termination.
  - **I/O Operations:** Manages file or device-related input/output operations.
  - **File-System Manipulation:** Includes reading, writing, creating, deleting files, and managing permissions.
  - **Communications:** Enables process communication on the same/different systems (via shared memory or message passing).
  - **Error Detection:** Monitors errors in hardware, I/O devices, and user programs to ensure consistent computing.

- **System-Focused Services:**
  - **Resource Allocation:** Allocates resources like CPU cycles, memory, and I/O devices to concurrent users/jobs.
  - **Accounting:** Tracks resource usage.
  - **Protection and Security:**
    - Controls access to resources.
    - Implements user authentication and defends against unauthorized access or attacks.

---

### **5. Views of OS Services**
The slides provide a visual representation of how services are structured, likely depicting user interaction and system functions.
![image](https://github.com/user-attachments/assets/c4f5a196-3a88-44ed-9fec-c7275806524b)

---

### **6. OS Structuring Methods**
Different structures include:
- **Monolithic OS:** All functionalities in one layer (e.g., MS-DOS).
- ![image](https://github.com/user-attachments/assets/19e0ff9b-cd86-4a80-afd7-446a5a7c43b3)
![image](https://github.com/user-attachments/assets/5988e89a-5877-4ce9-acba-1dad013a0911)

- **Layered OS:** Organized into layers, where each layer depends only on lower layers.
- ![image](https://github.com/user-attachments/assets/23c67774-d7fb-452a-bfc9-fb451b2209c7)
- ![image](https://github.com/user-attachments/assets/90202fd0-dad1-4821-ac6a-2b31792c0f34)
- ![image](https://github.com/user-attachments/assets/1c225c58-afbf-4124-8f7c-fa45d14a67dc)



- **Microkernel OS:**
  - Minimal kernel, most functionalities in user space.
  - Communication via message passing.
  - Benefits: Easier to extend, port, and secure.
  - Drawback: Performance overhead.
 ![image](https://github.com/user-attachments/assets/2b0385aa-b608-4cfd-b09d-90b6914a9534)
![image](https://github.com/user-attachments/assets/9d5bfc57-c7dd-42db-8e7f-7194961aad44)

![image](https://github.com/user-attachments/assets/07077477-5432-4dc5-b600-ab70f19311fb)

  - 
- **Kernel Modular OS:** Combines layered and microkernel advantages using dynamically loadable modules (e.g., Linux, Solaris).

![image](https://github.com/user-attachments/assets/248a61a4-4f50-4425-a697-66aeb8a48456)

---

### **7. OS Design Issues**
Major design considerations include:
- Transparency, flexibility, reliability, performance, scalability, replication, synchronization, and security.

---

### **8. Abstraction in OS**
- Abstracts hardware complexity and provides a common API for application development.
- Simplifies device management, maintenance, and portability.
- Includes a **Command Interpreter (Shell)** for executing commands.

---

### **9. Program Execution Process**
- **Program (secondary memory) → Process (main memory).**
- OS creates a process with three segments:
  - **Code Segment (CS):** Instructions to execute.
  - **Data Segment (DS):** Required data.
  - **Stack Segment (SS):** For procedure calls.
- **Security with Segmentation:** Ensures privilege levels for memory access.

---

### **10. Protection and Security**
- **Protection:** Mechanisms for resource access control.
- **Security:** Defense against attacks like viruses, identity theft, etc.
- Uses user IDs and group IDs to control access.

---

### **11. Computing Environments**
- **Traditional Standalone Systems:** General-purpose machines, now often interconnected.
- **Distributed Systems:** Multiple networked systems (LAN, WAN, MAN) enabling communication.
- **Client-Server Model:** Servers provide services to client systems (e.g., file servers, compute servers).
- **Peer-to-Peer (P2P) Systems:** Nodes act as both clients and servers (e.g., Skype, Napster).
- **Mobile Computing:** Smartphones and tablets with extra OS features like GPS.
- **Virtualization:** Runs OSes within others (e.g., VMware).
- **Cloud Computing:** Offers computing/storage as a service (e.g., SaaS, PaaS, IaaS).
- **Real-Time Embedded Systems:** Special-purpose systems with fixed time constraints.
- **Open Source OS:** Freely available source code (e.g., Linux, BSD UNIX).

---

### **12. References**
The content references textbooks like *Operating System Concepts* by Silberschatz, Gagne, Galvin, and web resources for additional context.

---

The diagrams and visuals in the slides likely depict:
1. System architecture models (monolithic, layered, microkernel, etc.).
2. Communication pathways in distributed systems.
3. OS service interactions (e.g., UI to kernel modules).
4. Computing environments like client-server and cloud systems.
5. 


# Module 2

The PowerPoint presentation dives deep into **Module 2: System Calls** and covers related concepts like processes, threads, interrupts, and system call types. Here’s a comprehensive summary of its content:

---

### **1. Introduction to System Calls**
- **Definition:** Programming interface for accessing OS services, typically via APIs in high-level languages like C or C++.
- **Common APIs:**
  - Win32 API (Windows)
  - POSIX API (UNIX, Linux, Mac OS X)
  - Java API (Java Virtual Machine)
- **Example:** The `printf()` function in C indirectly invokes the `write()` system call.

---

### **2. System Call Implementation**
- Each system call has a unique number.
- **System-call Interface:** Maintains a table indexed by call numbers to invoke kernel functions.
- Details are abstracted via APIs and runtime libraries, hiding implementation complexity.

---

### **3. Parameter Passing**
- **Methods:**
  1. Passing parameters in registers (simple).
  2. Storing parameters in memory blocks and passing their address.
  3. Using the program stack to push parameters and pop them later.
- **Advantages:** The block and stack methods allow flexible parameter lengths.

---

### **4. Types of System Calls**
- **Process Control:**
  - Create, terminate, or manage processes.
  - Handle debugging and resource allocation.
- **File Management:**
  - Create, delete, read, write, and manipulate file attributes.
- **Device Management:**
  - Request or release devices, adjust attributes, and attach/detach devices.
- **Information Maintenance:**
  - Retrieve or set time, system data, and process attributes.
- **Communication:**
  - Enable inter-process communication (message passing or shared memory).
- **Protection:**
  - Control resource access, set permissions, and manage user authentication.

---

### **5. Protection and Modes**
- **Dual-Mode Operation:** Differentiates between **user mode** and **kernel mode** using a mode bit.
  - Privileged instructions are restricted to kernel mode.
  - System calls shift to kernel mode and revert after execution.
- **Timer Interrupts:** Prevent resource hogging or infinite loops by setting a timer to interrupt processes exceeding allotted time.

---

### **6. Interrupt Handling**
- Interrupts shift control to an **Interrupt Service Routine** (ISR) via an interrupt vector.
- **Types:**
  - **Hardware Interrupts:** Triggered by devices.
  - **Software Interrupts (Traps/Exceptions):** Triggered by errors or user requests.
- Interrupt architecture saves the interrupted instruction’s address and determines the appropriate action (polling or vectored systems).

---

### **7. Process Concept**
- **Definition:** A program in execution.
- **Components:**
  - **Text Section:** Code instructions.
  - **Current Activity:** Includes the program counter and registers.
  - **Stack:** Temporary data like function parameters and local variables.
  - **Data Section:** Global variables.
  - **Heap:** Dynamically allocated memory.

---

### **8. Process States**
- **New:** Creation phase.
- **Running:** Instructions are executed.
- **Waiting:** Awaiting an event.
- **Ready:** Awaiting CPU allocation.
- **Terminated:** Finished execution.

---

### **9. Process Control Block (PCB)**
- Contains process-specific data:
  - State, program counter, CPU registers, memory allocation, scheduling info, I/O details, and accounting info.

---

### **10. Process Operations**
- **Creation:** Parent processes spawn children, forming a process tree.
  - Example: `fork()` and `exec()` in UNIX.
- **Termination:** Parent processes can terminate children using the `abort()` call.
  - Cascading termination occurs when parents terminate, forcing all child processes to terminate.

---

### **11. Threads**
- **Single-threaded vs. Multithreaded:**
  - Threads allow multiple execution streams within the same process.
- **Benefits:**
  - Improved responsiveness, resource sharing, lower creation overhead, and scalability.
- **Thread Types:**
  - **User Threads:** Managed at the user level (e.g., POSIX, Windows, Java threads).
  - **Kernel Threads:** Supported by the OS kernel.

---

### **12. Multithreading Models**
- **Many-to-One:** Multiple threads mapped to one kernel thread.
- **One-to-One:** Each user thread corresponds to a kernel thread.
- **Many-to-Many:** Combines both approaches for flexibility.

---

### **13. Real-World Examples**
- **Chrome Browser Architecture:** A multiprocess architecture:
  - **Browser Process:** Manages UI, disk, and network I/O.
  - **Renderer Process:** Handles HTML and JavaScript (sandboxed for security).
  - **Plug-in Process:** Dedicated processes for specific plug-ins.

---

### **14. Thread Creation Example**
- The `pthread_create()` function in C is used to create threads.
  - Passes thread attributes, an entry point function, and arguments.

---

### **15. Interrupt and Process Examples**
- **Interrupts:** Enable event-driven programming by handling software and hardware triggers.
- **Processes:** Demonstrated with forking examples, showing how process hierarchies and outputs evolve.

---

The presentation references the textbook *Operating System Concepts* by Silberschatz, Gagne, and Galvin, emphasizing practical examples and implementations. Let me know if you'd like specific diagrams or points elaborated!


## Syllabus after CAT 2:

### Module 5 (continue):

The concepts you've outlined relate to **memory management** in operating systems, specifically how virtual memory is implemented using **paging**, and how the operating system keeps track of what memory belongs to which process. Here's an explanation of each major concept:

---

### 🔒 **Memory Protection**

To prevent a process from accessing memory that it shouldn't:
- **Protection bits** are associated with each frame in physical memory.
  - Common bits:
    - **Read-only / Read-write**: Can the page be written to?
    - **Execute-only**: Can this page be executed (used for code)?
- These bits ensure that processes can't overwrite others' memory or execute invalid memory regions.
- If a process violates these rules, the CPU **traps** to the kernel (causing a **segmentation fault**, for example).

---

### ✅ **Valid-Invalid Bit in Page Table**

Each **page table entry** has a **valid-invalid bit**:
- **Valid (V)**: The page is part of the process’s logical address space.
- **Invalid (I)**: The page doesn’t belong to this process.
- If a process tries to access an invalid page, the OS traps and handles the violation (e.g., page fault or error).

An alternative is the **Page Table Length Register (PTLR)** which stores how many entries in the page table are valid — any access beyond this is invalid.

---

### 🤝 **Shared vs Private Memory**

- **Shared Code**:
  - Commonly used for **read-only code** like compilers, text editors.
  - Stored once in memory and **shared** across multiple processes.
  - Saves memory and improves cache performance.
- **Private Code and Data**:
  - Each process has **its own copy** of code and data that it can modify.
  - These copies can be stored in any location of the process's logical address space.

---

### 🧠 **Memory Overhead in Paging**

Paging creates a page table to map logical addresses to physical addresses.

#### Example:
- Logical address space = 32 bits → 2³² bytes
- Page size = 4 KB = 2¹² bytes
- Number of pages = 2²⁰ = ~1 million pages
- Each page table entry = 4 bytes → needs 4 MB just for one page table!

Allocating that much memory *contiguously* for each process is inefficient — hence better structures are used:

---

### 🏗️ **Hierarchical Page Tables**

To avoid large single-level page tables:
- Use **multi-level page tables**.
- Break the logical address into parts:
  - Suppose 32-bit address and 4 KB page:
    - Offset = 12 bits (for 4 KB)
    - Remaining 20 bits for page table entries

#### Two-level paging:
- Divide 20 bits into:
  - Outer page table index (`p1`) = 10 bits
  - Inner page table index (`p2`) = 10 bits
- So, a 32-bit address is broken down as:
  ```
  | p1 (10 bits) | p2 (10 bits) | offset (12 bits) |
  ```

This structure is known as **forward-mapped** paging.

For even larger address spaces (like 64-bit), multiple outer levels may be required (e.g., three or four-level paging).

---

### 🔢 **Hashed Page Tables**

Used when address space is huge (like in 64-bit systems):
- Use a **hash function** on the virtual page number to find its entry.
- Handle collisions via **linked chains**.
  - Each entry contains:
    - Virtual page number
    - Frame number (physical location)
    - Pointer to next entry in the chain
- Faster lookup using **hashing**, but still more complex than direct indexing.

A **clustered page table** is a variation where each entry maps multiple pages together (reducing overhead).

---

### 🔄 **Inverted Page Tables**

Instead of one page table **per process**, this keeps **one global page table**:
- One entry for **each physical frame** in memory.
- Each entry stores:
  - Virtual page number
  - Process ID (to identify which process owns it)

Advantage:
- Saves memory (especially on systems with lots of processes).

Disadvantage:
- Slower lookup → must **search** for matching entry.

To solve this:
- Use **hash tables** to speed up the search.
- Combine with **TLB (Translation Lookaside Buffer)** for fast address translation.

#### ❓Shared memory in inverted page tables:
- Requires **special handling** since many virtual addresses (from different processes) may map to **one shared physical page**.
- Must allow **multiple mappings** in the inverted page table.

---

### Summary Table

| Concept | Purpose | Key Points |
|--------|---------|------------|
| **Protection Bits** | Prevent invalid access | Read/write/execute bits |
| **Valid-Invalid Bit** | Mark legal pages | "Invalid" pages cause a trap |
| **Shared Code** | Save memory | One copy for multiple processes |
| **Hierarchical Paging** | Reduce table size | Multi-level page tables |
| **Hashed Page Tables** | Handle large address spaces | Hash on virtual page number |
| **Inverted Page Tables** | Save space across processes | One table for all, search on access |

---

Here’s a **structured summary** of the key concepts you’ve shared on **Virtual Memory and Demand Paging** from Operating Systems:

---

### 🔹 **1. Virtual Memory Basics**
- **Definition**: Separation of **logical** and **physical memory**.
- **Only part of a program** needs to be in memory to execute.
- Enables programs larger than physical memory to run.
- Improves **CPU utilization**, **throughput**, and **multi-programming** without increasing response time.
- Reduces I/O overhead for loading/swapping.

---

### 🔹 **2. Virtual Address Space**
- Logical memory starts at **address 0**.
- Stack grows **downwards** from max address; heap grows **upwards**.
- **Hole**: unused space between heap and stack.
- Enables **sparse memory**, **shared libraries**, and **shared memory**.
- Memory Management Unit (MMU) maps logical addresses to physical.

---

### 🔹 **3. Demand Paging**
- Bring pages into memory **only when needed**.
- **Lazy swapper** brings in pages **on demand**, not in advance.
- Reduces memory use, improves response time, and increases user capacity.
- If a page is not in memory → **page fault** occurs.

---

### 🔹 **4. Page Fault Handling**
1. Trap to OS.
2. Check if it's a valid reference.
3. Find a free frame or use a **page replacement algorithm**.
4. Bring the page from disk to memory.
5. Restart the instruction.

---

### 🔹 **5. Hardware Requirements**
- **Valid-invalid bit** in the page table (v = valid, i = invalid).
- **Secondary memory** (disk, swap space).
- Support for **instruction restart**.

---

### 🔹 **6. Effective Access Time (EAT)**
- Formula:  
  **EAT = (1 – p) × memory access time + p × (page fault overhead + swap out + swap in)**  
- For 1 in 1000 page faults (p = 0.001), huge slowdown (~40x).
- To limit slowdown to <10%, p < 0.0000025 (i.e., <1 page fault per 400,000 accesses).

---

### 🔹 **7. Copy-on-Write (COW)**
- Parent and child initially **share pages**.
- Pages copied **only on write**.
- **vfork()** is a variation where child uses parent's address space until `exec()`.

---

### 🔹 **8. Page Replacement**
- When no free frames are available.
- **Dirty bit** optimization: only modified pages written to disk.
- Replaces unused or least useful pages.

---

### 🔹 **9. Page Replacement Algorithms**
| Algorithm | Description | Page Faults (on sample) |
|----------|-------------|--------------------------|
| **FIFO** | Oldest page replaced | Higher faults |
| **OPT**  | Replace page used farthest in future | Best, theoretical |
| **LRU**  | Replace least recently used page | Good, needs time tracking |
| **Second-Chance (Clock)** | FIFO + reference bit | Efficient, approximates LRU |
| **Enhanced Clock** | Uses (reference, modify) bits | Better decisions |

---

### 🔹 **10. Belady’s Anomaly**
- In some algorithms (like FIFO), **more frames can cause more page faults**.

---

Would you like a visual diagram of how **demand paging** or **page replacement algorithms** work?

## Module 6:

Thanks for the clarification, and I see your full presentation now. I'll now **explain everything in your PowerPoint slide-by-slide**, making sure to **not skip anything**. Since this is a large and comprehensive topic (covering virtualization, file systems, allocation methods, indexing, recovery, and distributed file systems), I’ll break it down **clearly, in parts** for easy understanding.

---

## 🧩 **Module 6: Virtualization – Full Explanation**

---

### ✅ **Chapter Objectives**
- Understand what **virtual machines (VMs)** are, their **history** and **benefits**.
- Explore **virtualization technologies** like hypervisors.
- Learn **how virtualization is implemented** at the OS and hardware level.
- See how **hardware support** helps virtualization (e.g., CPU features).

---

### 🔍 **Overview of Virtualization**
- Virtualization means creating **abstracted versions of physical hardware**, allowing multiple **execution environments** (like OSs) to run on the same machine.
- It’s like placing a fake layer over real hardware so multiple systems think they have full access.
- A **Virtual Machine (VM)** acts like a real computer, but it’s **simulated by software**.

---

### 🔧 **Key Components**
- **Host**: The real physical computer.
- **VMM / Hypervisor**: Software layer that creates and manages virtual machines.
  - It provides an **interface identical** to the hardware.
- **Guest**: The operating system or process running **inside the VM**.
- This allows one computer to run **multiple OSs simultaneously**, isolated from each other.

---

### 🖥️ **System Models**
- **Non-Virtual Machine Model**: Normal system with one OS controlling all hardware.
- **Virtual Machine Model**: Hardware is abstracted, and multiple VMs can run over a VMM.

---

### 🧱 **Implementation of VMMs**
- **Type 1 Hypervisor** (Bare Metal): Runs directly on the hardware, like an OS.
  - Examples: VMware ESXi, Microsoft Hyper-V.
- **Type 2 Hypervisor** (Hosted): Runs as a software **application** on top of a regular OS.
  - Examples: Oracle VirtualBox, VMware Workstation, Parallels.

---

### 🧩 **Virtualization and OS Components**
The OS must adapt traditional operations for virtualization:
- **CPU Scheduling**: Managing virtual CPUs fairly across VMs.
- **Memory Management**: Isolating memory between VMs.
- **I/O & Storage**: Redirecting disk and device I/O correctly to/from each VM.
- **VM Migration**: Moving a live VM between hosts (live migration).

---

### 📦 **Container Virtualization**
- Uses **OS-level virtualization**, not hardware emulation.
- A **container** runs with the same kernel as the host OS but is **isolated** (filesystem, process tree, etc.).
- Lighter and faster than full VMs.
- Example: Docker

---

### 💸 **Cost of Virtualization**
- Saves costs by:
  - Reducing physical hardware requirements.
  - Lowering space and power usage.
  - Needing fewer people to manage hardware.

---

## 📁 **File System Concepts**

---

### 📂 **File-System Interface**

---

#### **File Concept**
- A **file** is an abstract data type that stores data (text, binary, etc.).
- Types:
  - Text files, source code, executables
  - Binary files (audio, images, etc.)

---

#### **File Attributes**
- **Name**: Human-readable
- **Identifier**: Unique tag
- **Type**: e.g., .txt, .exe
- **Location**: Physical disk address
- **Size**: File length
- **Protection**: Access rights
- **Timestamps**: Creation, last access, last modified

All these are stored in the **directory structure** on disk.

---

#### **File Operations**
- **Create**: Allocate space and metadata
- **Write**: At the write pointer
- **Read**: At the read pointer
- **Seek**: Move pointers
- **Delete**, **Truncate**
- **Open**: Load file’s info into memory
- **Close**: Save changes back

---

#### **Open Files**
- **Open-file table**: Tracks currently open files.
- **File pointer**: Tracks current read/write location.
- **File-open count**: Tracks how many processes have it open.
- **Access rights**: Per process
- **Locking**: Shared or exclusive (like Reader-Writer locks)

---

#### **File Structure**
- Can be:
  - Sequence of bytes (no structure)
  - Fixed/Variable records
  - Complex formats (documents, executables)

---

#### **Access Methods**
- **Sequential**: Read/write in order
- **Direct**: Access specific block
- **Indexed**: Use an index to jump directly

---

## 📁 **Directory Structure**

---

### 📚 **What is a Directory?**
- A table that contains information about files (name, size, location, etc.).
- Stored **on disk**, used by OS to organize and retrieve files.

---

### **Directory Models**

| Type | Features | Problems |
|------|----------|----------|
| Single-Level | Simple, one flat directory | Name conflicts, no grouping |
| Two-Level | Separate directories for users | No grouping |
| Tree | Hierarchical, grouping possible | Needs path management |
| Acyclic Graph | Allows shared subdirectories/files | Needs back-pointers to avoid dangling refs |
| General Graph | Allows full flexibility | Needs cycle detection |

---

### 📌 **Mounting File Systems**
- Before access, a file system must be **mounted** at a **mount point**.
- Mounted volumes are then accessible through the existing directory tree.

---

### 👥 **File Sharing and Protection**
- Users can **share** files via permissions (read/write/execute).
- Use **User IDs** and **Group IDs**.
- Access Control Lists (ACLs) for fine-grained control (used in Windows).
:


---

1. Structure Layers in File System Implementation

These layers work together to ensure that when an application wants to read/write a file, it is handled correctly all the way from the user level to the hardware.

a. Application Calls OS

Applications use system calls like open(), read(), write() to interact with files.

These calls are sent to the Operating System, which passes them down through various layers of the file system.


b. Logical File System (LFS)

Manages metadata: file names, directory structure, permissions, ownership, timestamps, etc.

Provides an interface to manage files and directories without worrying about physical storage.

Responsible for protection and security (like access rights).


c. File Organization Module

Translates logical file blocks (e.g., block 5 of a file) into physical disk blocks.

Handles file allocation methods: contiguous, linked, indexed.

Keeps track of where file parts are on the disk.


d. Basic File System

Deals with I/O operations, manages buffers and caches.

Optimizes data transfer with techniques like read-ahead, write-behind, or caching.

Coordinates with I/O schedulers to minimize seek time and improve performance.


e. Device Drivers

Lowest level.

Interacts directly with the disk hardware (SSD/HDD).

Converts high-level commands (like read block 12) into hardware-specific instructions.



---

2. Important Data Structures on Disk

These are stored persistently on disk and are essential for file system operation.

a. Boot Control Block

Present in system disks (not always in all volumes).

Contains code to boot the system.

May include location of the OS kernel.


b. Volume Control Block (VCB)

Also called a superblock (especially in UNIX).

Contains info like:

Total number of blocks

Number of free blocks

Block size

Number of FCBs (file descriptors)



c. File Control Block (FCB)

Stores metadata for each file:

File size

Ownership

Permissions

Time stamps (creation, access, modification)

Pointers to file data blocks



d. Mount Table

Keeps track of all mounted file systems.

Helps the OS access files that are stored on other volumes/devices.



---

3. In-Memory Structures

Used by the OS to cache frequently used information for faster access (volatile, lost after reboot).

a. Open-File Table

Each process and the system maintain tables for files that are currently open.

Tracks:

File descriptor

Read/write pointer

Buffer location

Access mode



b. Mount Table (in-memory copy)

Contains details of mounted file systems, including pointers to the VCB, root directory, etc.


c. Buffers

Used for temporary storage during read/write.

Helps improve performance and reduce direct disk access.



---

4. Virtual File System (VFS)

Purpose:

Provides a unified interface to support multiple types of file systems (e.g., ext4, NTFS, FAT32).

Applications don't need to know what file system is being used.


How It Works:

VFS defines a standard set of functions like open(), read(), close() regardless of the underlying FS.

Internally, VFS uses objects like:

vnode (virtual node): abstract representation of files.

inode: holds metadata (Linux-specific).

dentry: directory entry.

superblock: describes a file system's overall structure.

file: represents an open file.




---

Analogy to Help You Visualize

Think of the file system like a post office:

Application: You (the sender) writing a letter.

Logical File System: The post office that checks if the address is valid.

File Organization Module: Sorts and routes your letter to the correct truck.

Basic File System: Manages the trucks, delivery routes, and schedules.

Device Driver: The driver who delivers the letter.

On-Disk Data Structures: The city maps and logs used by the post office.

VFS: Like a postal service that delivers both letters and packages, regardless of their origin (FedEx, DHL, etc.).



---

Would you like a diagram to visualize these layers and structures?


---

## 📦 **Directory Implementation**

---

### 📋 **Methods**
- **Linear List**: Simple, slow for large directories.
- **Hash Table**: Fast lookup, handles collisions.

---

## 💽 **Allocation Methods**

---

### 1. **Contiguous Allocation**
- Files stored in consecutive blocks.
- Fast access but causes **external fragmentation**.
- Need to know file size in advance.

### 2. **Extent-Based Allocation**
- Allocates extents (chunks of contiguous blocks).
- Improves flexibility while maintaining performance.

### 3. **Linked Allocation**
- Each block has a pointer to the next.
- No external fragmentation.
- **Slow** access; reliability issues.

### 4. **FAT (File Allocation Table)**
- Linked allocation with a table at the beginning.
- Speeds up access, easy to cache.

### 5. **Indexed Allocation**
- Each file has an index block.
- Allows **random access**, no external fragmentation.
- Needs overhead for index storage.

---

## 🔁 **Recovery & Journaling**

---

### 🧹 **Consistency Checking**
- Compare directory entries with data blocks.
- Try to fix errors.

### 📀 **Backups**
- Copy data to external media for recovery.

### 📓 **Log-Structured File Systems**
- Log metadata updates as transactions.
- Faster recovery after crashes.

### 🔧 **Soft Updates**
- Maintain metadata integrity by **tracking dependencies** between updates.

---

## 🌐 **Distributed File Systems (DFS)**

---

### 🕸️ **What is DFS?**
- A file system **spread across multiple machines**.
- Users access files as if they’re local.
- DFS manages **transparency**, **replication**, and **reliability**.

### 🧩 **Components**
- **Namespace**: Makes local/remote files appear unified.
- **Redundancy**: Replicates data for fault tolerance.

---

### ⭐ **DFS Features**
- User Mobility: Your files follow you.
- High Availability & Reliability.
- Security via access control.
- Scalability and simplicity.

---

Here’s a **comprehensive explanation** of everything in the presentation "Module-7: Disk Storage" without skipping **any** detail:

---

## 📘 **Module 7: Disk Storage (Chapter 10: Mass-Storage Systems)**

---

### 🧠 **Objectives**
- Explain the physical structure of secondary storage.
- Understand performance characteristics.
- Evaluate disk scheduling algorithms.
- Learn about OS support for storage, including RAID.

---

### 💾 **Overview of Mass Storage Structure**
- **Magnetic disks**: Backbone of secondary storage.
- **Drive rotation**: 60–250 rotations/sec.
- **Transfer rate**: Data transfer rate between drive & computer.
- **Positioning time** (a.k.a. **random access time**):  
  = **Seek time** (move arm to cylinder) + **Rotational latency** (wait for sector under head).
- **Head crash**: Physical contact with disk surface → catastrophic failure.
- **Disk Removability**: Some are removable.
- **Connections** via various buses:  
  EIDE, ATA, SATA, USB, Fibre Channel, SCSI, SAS, FireWire.
- **Host controller** talks to **disk controller** via I/O bus.

---

### 🔄 **Moving-Head Disk Mechanism**
- Mechanical movement over platters to read/write data.

---

### 🧱 **Hard Disks**
- **Sizes**: Historically 0.85” to 14”; common: 3.5", 2.5", 1.8".
- **Storage**: 30GB – 3TB per drive.
- **Performance**:
  - **Theoretical Transfer Rate**: 6 Gb/s.
  - **Effective Transfer Rate**: ~1 Gb/s.
  - **Seek Time**: 3–12 ms (avg. desktop = 9 ms).
- **Latency** (delay due to spinning):
  \[
  \text{Latency} = \frac{60}{\text{RPM}}, \quad \text{Avg latency} = \frac{\text{Latency}}{2}
  \]

---

### 🧮 **Hard Disk Performance Calculations**
- **Access Latency** = Seek Time + Avg Latency.
- Example:
  - Fast disk: 3 + 2 = 5 ms.
  - Slow disk: 9 + 5.56 = 14.56 ms.
- **Avg I/O Time** = Access time + transfer time + controller overhead.
- E.g., 4KB transfer on 7200 RPM disk:
  - Access = 5 ms
  - Controller overhead = 0.1 ms
  - Transfer time ≈ 0.031 ms  
  ⇒ **Total ≈ 9.301 ms**

---

### 🕰 **The First Commercial Disk Drive**
- **IBM Model 350 (1956)** in RAMDAC.
- 50 x 24” platters, 5M (7-bit) chars.
- Access time: < 1 sec.

---

### ⚡ **Solid-State Disks (SSDs)**
- **No moving parts**: Faster (no seek/latency).
- **Non-volatile** memory.
- **Drawbacks**: More expensive, less capacity, potential shorter lifespan.
- **Connection**: PCI (for speed) over traditional bus.

---

### 🧵 **Magnetic Tape**
- **Oldest secondary storage**.
- From open spools → cartridges.
- **Sequential access** (1000× slower than disk).
- **Used for**: backup, infrequent storage, system transfer.
- **Transfer rates**: ~140MB/s or more.
- **Capacity**: 200GB – 1.5TB.
- **Common formats**: LTO-{3,4,5}, T10000.

---

## 🧱 **Disk Structure**
- **Logical Blocks**: smallest transfer unit.
- **Low-level formatting**: creates logical blocks on physical media.
- **Mapping**:
  - Starts from sector 0 (first sector, first track, outermost cylinder).
  - Proceeds sequentially → inward.
- **Issues**:
  - Bad sectors disrupt mapping.
  - Constant Angular Velocity (non-uniform sector count per track).

---

## 🖇 **Disk Attachment**
- **Host-attached storage**: via I/O ports (SCSI, etc.).
- **SCSI**:
  - Bus with up to 16 devices.
  - Devices = **Initiators** and **Targets**.
  - Each target: up to 8 **Logical Units (LUNs)**.
- **Fibre Channel (FC)**:
  - Serial, high-speed.
  - 24-bit address space.
  - Enables **SANs** (Storage Area Networks).
  - I/O to Bus ID → Device ID → LUN.

---

## 🧰 **Storage Array**
- May include:
  - Controllers, memory (maybe NVRAM), software.
  - From few → thousands of disks.
  - Supports: RAID, hot spares, hot swap.
- **Advanced features**:
  - Snapshots, cloning, thin provisioning, replication, deduplication.

---

### 🧠 **Storage Area Network (SAN)**
- **SAN** = multiple arrays + hosts connected via Fibre Channel switches.
- **LUN Masking**: restrict storage access per host.
- **Benefits**:
  - Flexibility, scalability.
  - Low-latency communication.
- **Alternatives**: iSCSI, FCoE.

---

### 🌐 **Network-Attached Storage (NAS)**
- Storage accessible via **IP Network** instead of local bus.
- Common protocols:
  - **NFS**, **CIFS**.
  - Use **RPC** (Remote Procedure Calls) over TCP/UDP.
- **iSCSI**: SCSI protocol over IP for block-level storage.

---

## 🔁 **Disk Scheduling**
- Goal: Minimize access time and increase disk bandwidth.
- **Seek Time** ≈ Seek distance.
- **Disk Bandwidth**: total bytes transferred ÷ total request time.

---

### 🧾 **Sources of I/O Requests**
- OS, system processes, user processes.
- Each request: mode (read/write), disk addr, memory addr, sector count.
- Requests are queued per device.

---

### 📊 **Scheduling Algorithms**
1. **FCFS (First-Come, First-Served)**:
   - Simple, fair, poor performance.
   - Example: Total movement = **640 cylinders**.

2. **SSTF (Shortest Seek Time First)**:
   - Chooses nearest request → better performance.
   - May starve distant requests.
   - Movement: **236 cylinders**.

3. **SCAN (Elevator Algorithm)**:
   - Moves in one direction, services all requests, then reverses.
   - Avoids starvation.
   - Movement: **236 cylinders**.

4. **C-SCAN (Circular SCAN)**:
   - Goes one way servicing requests.
   - Immediately jumps to beginning without servicing on return.
   - Uniform wait time.

5. **C-LOOK**:
   - Like C-SCAN but reverses at last request instead of going to end.

---

### 🧮 **Disk Scheduling Example**
- Given disk requests:  
  `45, 21, 67, 90, 4, 50, 89, 52, 61, 87, 25`  
  - Head starts at: 50.
  - Use different algorithms to analyze performance.

---

## 🧠 **Selecting the Right Scheduling Algorithm**
- **SSTF**: common and intuitive.
- **SCAN / C-SCAN**: good under heavy load.
- Performance depends on request pattern, metadata layout, and allocation method.
- **Algorithm = separate OS module**: easy to swap.
- **Rotational latency**: hard for OS to calculate.
- **Queueing in hardware** can affect software-based ordering.

---

## 🔐 **OS – Security & Threats**

### 🔒 **Security**
Protects:
- CPU
- Memory
- Disk
- Software
- Data

If unauthorized users access the system → serious damage.

---

### 👤 **Authentication**
- Confirms user identity:
  - Username/password
  - Card/key
  - Biometric (fingerprint, retina)

---

### ⏱ **One-Time Passwords**
1. **Random number card**
2. **Hardware key**
3. **SMS/email-based codes**

---

### 🦠 **Program Threats**
Malicious user programs influencing system processes.

#### Types:
- **Trojan Horse**: Fake programs steal data.
- **Trap Door**: Hidden code performs malicious actions.
- **Logic Bomb**: Triggers malicious actions under certain conditions.
- **Virus**: Infects files/systems.

---

### 🌐 **System Threats**
- Misuse of system resources and network.

#### Types:
- **Worm**: Overuses resources.
- **Port Scanning**: Finds vulnerabilities.
- **DoS (Denial of Service)**: Blocks access (e.g., to browser/internet).

---

### 📏 **Policy vs Mechanism**
- **Policy**: *What* to enforce.
- **Mechanism**: *How* to enforce it.

---

### ✅ **Access vs Authentication**
- **Authentication**: Verify identity.
- **Access Control**: Restrict specific actions based on authentication.

---

### 🔐 **System Protection**
- Controls access to resources (CPU, files, memory).
- Allows safe multi-user environments.
- Helps detect errors and prevent unauthorized access.

---

### 🧮 **Access Matrix**
- Security model for defining access rights.

\[
\text{Matrix Rows} = Domains (Users/Processes)\\
\text{Columns} = Objects (Files/Resources)
\]

---

### 🔐 **Capability-based System**
- Capabilities (access rights) are securely passed between processes.

---

### 📱 **Future Direction in Mobile OS**
(No detail provided in slides, likely left for further discussion.)

---


