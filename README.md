[readme (1).md](https://github.com/user-attachments/files/26223103/readme.1.md)
# Lab 9 — Network Programming with Sockets

> A TCP client-server application in C demonstrating socket-based interprocess communication using the CSAPP library.

---

## Overview

This project implements a **TCP client-server model** where a client connects to a server, exchanges two messages, and receives a confirmation for each. Built as part of **CSCI 3240** to explore the fundamentals of network programming using the Unix socket API.

---

## How It Works

### Server
1. Starts and listens on a given port
2. Accepts an incoming client connection
3. Reads the client's first message and replies with `"I got your message."`
4. Reads the client's second message and replies with `"I have received your second message."`
5. Closes the connection and loops back to wait for the next client

### Client
1. Connects to the server using a hostname and port
2. Prompts the user to enter a first message and sends it
3. Waits for and displays the server's response
4. Prompts the user to enter a second message and sends it
5. Waits for and displays the server's second response
6. Closes the connection and exits

---

## Project Structure

```
lab9/
├── client.c       # Client-side socket logic
├── server.c       # Server-side socket logic
├── csapp.c        # CSAPP helper library (CS:APP3e)
├── csapp.h        # CSAPP header file
└── makefile       # Build configuration
```

---

## Build & Run

**Compile**
```bash
make
```

**Start the Server**
```bash
./server 3240
```

**Run the Client** *(open a second terminal)*
```bash
./client localhost 3240
```

---

## Test Run

**Server terminal:**
```
Connected to (localhost, 36550)
server received 6 bytes message
Message from Client: Hello World

server received 3 bytes message
Message from Client: hi

(localhost, 36550) disconnected
```

**Client terminal:**
```
Please enter the message: Hello World
Message from Server: I got your message.
Enter another message: hi
Message from Server: I have received your second message.
```

---

## Key Concepts

| Concept | Description |
|---|---|
| **Sockets** | Endpoints for communication, treated like file descriptors in Unix |
| **Port Numbers** | Used to route traffic to the correct process on a machine |
| **bind → listen → accept** | Server-side connection setup, wrapped by `Open_listenfd` |
| **connect** | Client-side connection setup, wrapped by `Open_clientfd` |
| **read / write** | Send and receive data over the socket, same as regular file I/O |
| **Turn-based communication** | Server and client alternate reading and writing to avoid deadlock |

---

## Notes

- The server runs indefinitely until killed with `Ctrl+C`
- `Fgets` is used for input instead of `scanf` for safe line-buffered reading
- CSAPP wrapper functions handle error checking internally
