# README.md

## Simple Client-Server TCP Communication in C

This project demonstrates basic TCP socket communication between a server and a client in C using the POSIX socket API. The server listens for incoming connections, accepts a client connection, and receives a message. The client connects to the server and sends a message.

---

### Server Program

#### **Line by Line Explanation**

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/socket.h>
#include <arpa/inet.h>
#include <unistd.h>
```
- **Includes necessary libraries**:
  - `stdio.h` and `stdlib.h`: For standard I/O and memory management.
  - `string.h`: For string manipulation functions.
  - `sys/socket.h` and `arpa/inet.h`: For socket-related functions and structures.
  - `unistd.h`: For close() and other Unix system calls.

```c
#define QUEUE_LIMIT 5
```
- **Defines a limit** for the number of connections waiting to be accepted in the server's queue.

```c
int main() {
    int sockid = socket(AF_INET, SOCK_STREAM, 0);
```
- **Creates a TCP socket** (`SOCK_STREAM` denotes TCP). The `socket()` function returns a socket descriptor or -1 if the creation fails.

```c
    if (sockid == -1) {
        perror("Socket creation failed");
        return EXIT_FAILURE;
    }
    printf("Socket creation successful\n");
```
- **Checks if the socket was created successfully**. If not, it prints an error message using `perror()` and exits the program.

```c
    struct sockaddr_in addrport;
    addrport.sin_family = AF_INET;
    addrport.sin_addr.s_addr = inet_addr("127.0.0.1");
    addrport.sin_port = htons(8000);
```
- **Configures the server address** (`struct sockaddr_in`) for IPv4 communication.
  - `AF_INET`: IPv4 family.
  - `inet_addr("127.0.0.1")`: Sets the IP address to `localhost` (127.0.0.1).
  - `htons(8000)`: Converts port number 8000 to network byte order using `htons()`.

```c
    int status = bind(sockid, (struct sockaddr*)&addrport, sizeof(addrport));
```
- **Binds the socket** to the specified address and port, making it ready to accept connections on port 8000.

```c
    if (status == -1) {
        perror("Binding failed");
        close(sockid);
        return EXIT_FAILURE;
    }
    printf("Binding successful\n");
```
- **Checks if binding was successful**. If not, it prints an error and exits the program.

```c
    status = listen(sockid, QUEUE_LIMIT);
```
- **Listens for incoming connections**. The `listen()` function marks the socket as a passive socket, and the server can accept connections with a queue limit of `QUEUE_LIMIT` (5).

```c
    if (status == -1) {
        perror("Listen failed");
        close(sockid);
        return EXIT_FAILURE;
    }
    printf("Listening for connections...\n");
```
- **Checks if the server is listening successfully**. If not, prints an error message and exits.

```c
    struct sockaddr_in client_addr;
    socklen_t addrlen = sizeof(client_addr);
```
- **Creates a structure to store client details** once the connection is accepted.

```c
    int client_sock = accept(sockid, (struct sockaddr*)&client_addr, &addrlen);
```
- **Accepts a client connection**. This function blocks the server until a client connects. It returns a new socket descriptor to communicate with the client.

```c
    if (client_sock == -1) {
        perror("Accept failed");
        close(sockid);
        return EXIT_FAILURE;
    }
    printf("Client connected\n");
```
- **Checks if the client connection was successful**. If not, prints an error and exits.

```c
    char buffer[1024];
    ssize_t recv_size = recv(client_sock, buffer, sizeof(buffer) - 1, 0);
```
- **Receives a message from the client**. The `recv()` function reads data from the client's socket into the buffer.

```c
    if (recv_size > 0) {
        buffer[recv_size] = '\0';
        printf("Received message: %s\n", buffer);
```
- **Prints the message** received from the client after null-terminating the string.

```c
    } else {
        perror("Receive failed");
    }
```
- **Handles the case** where the message was not received successfully.

```c
    close(client_sock);
    close(sockid);
```
- **Closes the client and server sockets** once communication is finished.

```c
    return EXIT_SUCCESS;
}
```
- **Exits the server program** with a success status.

---

### Client Program

#### **Line by Line Explanation**

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/socket.h>
#include <arpa/inet.h>
#include <unistd.h>
```
- **Includes necessary libraries** similar to the server program for socket functions and standard operations.

```c
int main() {
    int sockid = socket(AF_INET, SOCK_STREAM, 0);
```
- **Creates a TCP socket** similar to the server.

```c
    if (sockid == -1) {
        perror("Socket creation failed");
        return EXIT_FAILURE;
    }
    printf("Socket creation successful\n");
```
- **Checks if the socket was created successfully**. If not, it prints an error.

```c
    struct sockaddr_in server_addr;
    server_addr.sin_family = AF_INET;
    server_addr.sin_addr.s_addr = inet_addr("127.0.0.1");
    server_addr.sin_port = htons(8000);
```
- **Configures the server address** to which the client will connect.
  - `inet_addr("127.0.0.1")`: Connects to the localhost.
  - `htons(8000)`: Specifies the port 8000.

```c
    int status = connect(sockid, (struct sockaddr*)&server_addr, sizeof(server_addr));
```
- **Attempts to connect** to the server using the specified address and port.

```c
    if (status == -1) {
        perror("Connect failed");
        close(sockid);
        return EXIT_FAILURE;
    }
    printf("Connected to server\n");
```
- **Checks if the connection was successful**. If not, prints an error message.

```c
    const char *message = "Hello from the client!";
    ssize_t sent_size = send(sockid, message, strlen(message), 0);
```
- **Sends a message to the server**. The `send()` function writes the message to the server's socket.

```c
    if (sent_size == -1) {
        perror("Send failed");
        close(sockid);
        return EXIT_FAILURE;
    }
    printf("Message sent: %s\n", message);
```
- **Checks if the message was sent successfully**. If not, prints an error.

```c
    close(sockid);
```
- **Closes the client's socket** once the message is sent.

```c
    return EXIT_SUCCESS;
}
```
- **Exits the client program** with a success status.

---

### How to Run the Programs

1. **Compile the server program**:
    ```bash
    gcc server.c -o server
    ```

2. **Run the server program**:
    ```bash
    ./server
    ```

3. **In a separate terminal window, compile the client program**:
    ```bash
    gcc client.c -o client
    ```

4. **Run the client program**:
    ```bash
    ./client
    ```

---

### Expected Output

#### Server Side:
```bash
Socket creation successful
Binding successful
Listening for connections...
Client connected
Received message: Hello from the client!
```

#### Client Side:
```bash
Socket creation successful
Connected to server
Message sent: Hello from the client!
```
