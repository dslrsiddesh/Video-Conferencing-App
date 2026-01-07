# Video Conferencing Application using Socket Programming

This project implements a basic video conferencing system using **TCP socket
programming in Python**. The primary focus of the project is on understanding
and applying **computer networking concepts** such as client–server communication,
reliable data transfer, and continuous streaming over persistent connections.

The graphical interface is intentionally kept minimal and is used only to
visualize the received video stream. The core contribution of the project lies
in the networking and communication design.

---

## Objective

The objective of this project is to design and implement a real-time video
communication system that demonstrates:

- Client–server architecture
- TCP-based reliable communication
- Application-layer framing over a byte-stream protocol
- Continuous data transmission using persistent sockets

This project was developed for academic learning and experimentation in the
domain of Computer Networks.

---

## Architecture Overview

The system follows a **centralized server-based architecture**.

A single server listens for incoming client connections on a specified IP
address and port. Multiple clients connect to the server and establish
persistent TCP connections. Video frames captured at the client side are sent
to the server, which then relays the received data to other connected clients.

All communication is handled using **TCP**, ensuring ordered and reliable
delivery of video data.

---

## Networking Design

### Client–Server Communication

The server creates a listening socket and waits for incoming client connections.
Each client initiates a connection using TCP and maintains a persistent socket
for continuous data exchange.

Once connected, clients begin transmitting video frames to the server without
closing the connection after each transmission. This models real-time streaming
over a long-lived TCP session.

---

### Data Serialization and Framing

Since TCP is a stream-oriented protocol and does not preserve message boundaries,
an application-layer framing mechanism is implemented.

Each video frame is:
- Serialized using `pickle`
- Preceded by its size encoded using the `struct` module
- Sent as a continuous byte stream over the socket

On the receiver side, the frame size is first read, followed by the complete
frame payload. This ensures correct reconstruction of video frames from the
TCP stream.

---

### Continuous Streaming

The application maintains continuous loops on both client and server sides for:
- Capturing video frames
- Sending serialized data
- Receiving and decoding incoming frames

This simulates real-time media streaming while relying entirely on TCP for
reliability and flow control.

---

### Reliability Considerations

TCP was chosen for this project to simplify the implementation by leveraging:
- Guaranteed delivery
- In-order packet arrival
- Built-in congestion and flow control

Unlike UDP-based streaming systems, no additional logic is required for packet
loss handling or reordering, making the project suitable for learning purposes.

---

## Module Description

The server module handles socket creation, connection management, and data
forwarding between connected clients.

The client module captures video frames from the local webcam, serializes them,
and sends them continuously to the server.

The communication module abstracts low-level socket send and receive operations,
ensuring reliable transmission of framed data.

The GUI client module is responsible only for displaying received video frames
and does not influence the networking logic.

---

## Execution

First, start the server process so it begins listening for client connections.
Then, run one or more client instances which connect to the server and start
streaming video data.

All participating machines must be reachable over the network and configured
with the correct server IP address and port.

---

## Concepts Demonstrated

- TCP socket programming
- Client–server architecture
- Stream-based communication
- Application-layer protocol design
- Real-time data transmission

---

## Limitations

This implementation does not include encryption, authentication, NAT traversal,
or bandwidth optimization. It is intended purely for academic exploration of
networking concepts and is not suitable for production use.

---

## License

This project is licensed under the GPL-3.0 License.

---

## Note

This project was developed to strengthen practical understanding of
**Computer Networks**, with emphasis on socket programming and data transmission
mechanisms rather than user interface design.
