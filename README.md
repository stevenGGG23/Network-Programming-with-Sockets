Lab 9 - Network Programming with Sockets
A simple client-server application built in C using the CSAPP library that demonstrates socket-based interprocess communication over a network.

Overview
This project implements a TCP client-server model where a client connects to a server, exchanges two messages, and receives a confirmation for each. It was built as part of CSCI 3240 to explore the fundamentals of network programming using the Unix socket API.

How It Works
Server
Starts and listens on a given port
Accepts an incoming client connection
Reads the client's first message and replies with "I got your message."
Reads the client's second message and replies with "I have received your second message."
Closes the connection and loops back to wait for the next client
Client
Connects to the server using a hostname and port
Prompts the user to enter a first message and sends it
Waits for and displays the server's response
Prompts the user to enter a second message and sends it
Waits for and displays the server's second response
Closes the connection and exits
Project Structure
lab9/
├── client.c       # Client-side socket logic
├── server.c       # Server-side socket logic
├── csapp.c        # CSAPP helper library (CS:APP3e)
├── csapp.h        # CSAPP header file
└── makefile       # Build configuration
Dependencies
GCC
POSIX Threads (-lpthread)
CSAPP Library (included)
Build & Run
Compile
bash
make
Start the Server
bash
./server <port>
Example:

bash
./server 3240
Run the Client (in a separate terminal)
bash
./client <host> <port>
Example:

bash
./client localhost 3240
Test Run
Server terminal:

Connected to (localhost, 36550)
server received 6 bytes message
Message from Client: Hello World

server received 3 bytes message
Message from Client: hi

(localhost, 36550) disconnected
Client terminal:

Please enter the message: Hello World
Message from Server: I got your message.
Enter another message: hi
Message from Server: I have received your second message.
Key Concepts
Sockets — endpoints for communication, treated like file descriptors in Unix
Port numbers — used to route traffic to the correct process on a machine
bind → listen → accept — the server-side connection setup (wrapped by Open_listenfd)
connect — the client-side connection setup (wrapped by Open_clientfd)
read/write — used to send and receive data over the socket, same as file I/O
Turn-based communication — server and client alternate reading and writing to avoid deadlock
Notes
The server runs indefinitely until killed with Ctrl+C
Fgets is used for user input instead of scanf to safely handle line-buffered input
The CSAPP wrapper functions handle error checking internally
