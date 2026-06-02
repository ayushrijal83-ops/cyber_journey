# Real-Life Example of TCP/IP and OSI Layers

## Introduction

In this lesson, I learned an overview of how data travels through a TCP/IP network. We did not go deep into every topic, but we learned the basic flow of data from one device to another and how different layers work together.

---

# Layers We Learned

1. Application Layer
2. Transport Layer
3. Network Layer
4. Data Link Layer
5. Physical Layer

---

# Application Layer

The Application Layer is where users interact with network services.

Protocols such as:

- HTTP
- HTTPS
- SMTP
- FTP
- DNS

operate at this layer.

When we visit a website or send an email, the communication starts here.

---

# Transport Layer

The Transport Layer is responsible for transporting data between devices.

It mainly uses:

- TCP (Transmission Control Protocol)
- UDP (User Datagram Protocol)

## TCP

TCP is a reliable protocol.

Before communication starts, TCP performs a process called the Three-Way Handshake.

Key Points:

- Reliable
- Connection-oriented
- Uses Three-Way Handshake
- Slightly slower than UDP

## UDP

UDP is faster than TCP.

Unlike TCP, UDP does not establish a connection before sending data.

Key Points:

- Fast
- Connectionless
- No handshake
- Less reliable than TCP

---

# Encapsulation

Encapsulation can be understood as placing data into a new envelope at every layer.

As data moves down the layers, each layer adds information called a Header.

The Data Link Layer also adds a Trailer.

This process is known as Encapsulation.

---

# Network Layer

The Network Layer deals with IP addresses.

It adds information such as:

- Source IP Address
- Destination IP Address

Routers use this information to forward packets to the correct destination.

---

# Data Link Layer

The Data Link Layer deals with MAC addresses.

Switches mainly operate at this layer.

This layer adds:

- Layer 2 Header
- Layer 2 Trailer

At this stage, the data is called a Frame.

---

# Physical Layer

The Physical Layer is responsible for transmitting bits across cables, fiber optics, or wireless signals.

This is where the actual transmission takes place.

---

# Data Flow Example

When you open a website:

1. Application Layer creates the request.
2. Transport Layer adds TCP or UDP information.
3. Network Layer adds IP address information.
4. Data Link Layer adds MAC address information.
5. Physical Layer sends the data.

The receiving device performs the reverse process.

---

# Key Takeaways

- Application Layer handles protocols such as HTTP and HTTPS.
- Transport Layer uses TCP and UDP.
- TCP is reliable and connection-oriented.
- UDP is faster but less reliable.
- Encapsulation adds headers and trailers.
- Network Layer works with IP addresses.
- Data Link Layer works with MAC addresses.
- Physical Layer sends bits across the network.

---

# Why This Matters for Cybersecurity

Understanding these layers is important because many cyber attacks target network communication.

Examples:

- TCP -> SYN Flood Attacks
- DNS -> DNS Spoofing
- ARP -> ARP Poisoning
- Network Traffic -> Packet Analysis with Wireshark

A strong networking foundation makes cybersecurity much easier to understand.
