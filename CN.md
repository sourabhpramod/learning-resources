The OSI (Open Systems Interconnection) model is a conceptual framework that standardizes the functions of a telecommunication or networking system into seven distinct layers. Each layer serves specific functions and interacts with the layers directly above and below it. Here’s a breakdown of the seven layers and their functions:

### 1. **Physical Layer (Layer 1)**
   - **Function**: The physical layer is responsible for the transmission of raw data (bits) over a physical medium, such as cables, radio frequencies, or fiber optics. It defines the hardware elements, such as cables, switches, voltage levels, and physical data rates.
   - **Example**: Ethernet cables, hubs, Bluetooth, Wi-Fi.

### 2. **Data Link Layer (Layer 2)**
   - **Function**: This layer is responsible for node-to-node data transfer and error detection/correction. It also manages access to the physical medium (i.e., how devices share the communication channel). It divides data into frames for easier transmission.
   - **Sub-Layers**:
     - **MAC (Media Access Control)**: Controls access to the physical medium and handles addressing.
     - **LLC (Logical Link Control)**: Manages communication between devices and provides error checking.
   - **Example**: Ethernet, MAC addresses, switches.

### 3. **Network Layer (Layer 3)**
   - **Function**: The network layer is responsible for data routing, switching, and addressing so that data can travel across different networks. It decides the best physical path for the data to take.
   - **Example**: IP (Internet Protocol), routers.

### 4. **Transport Layer (Layer 4)**
   - **Function**: This layer ensures reliable data transfer between host systems, providing error recovery and flow control. It divides data into segments, ensures they are sent in sequence, and reassembles them at the destination.
   - **Protocols**:
     - **TCP (Transmission Control Protocol)**: Provides reliable data transmission with acknowledgment.
     - **UDP (User Datagram Protocol)**: Provides faster, connectionless, but less reliable data transmission.
   - **Example**: TCP, UDP, port numbers.

### 5. **Session Layer (Layer 5)**
   - **Function**: The session layer manages and controls the connection between two systems, ensuring that sessions are established, maintained, and terminated in an orderly way. It also handles dialogue control, synchronization, and session recovery.
   - **Example**: Network sessions, authentication, session establishment.

### 6. **Presentation Layer (Layer 6)**
   - **Function**: The presentation layer translates data between the application layer and the rest of the OSI model. It handles data encryption, compression, and format conversion, ensuring that data from the application layer is readable by the receiving system.
   - **Example**: Data encryption (TLS), data compression, character encoding (ASCII, JPEG, MP4).

### 7. **Application Layer (Layer 7)**
   - **Function**: This is the layer where user interaction happens. It provides services directly to end users and applications, such as email, file transfer, and web browsing. It supports network services like file access, file sharing, and database management.
   - **Example**: HTTP, FTP, SMTP, DNS.

In summary, the OSI model ensures that communication between systems is standardized, with each layer serving specific roles to ensure smooth data transmission and reception.