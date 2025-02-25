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
