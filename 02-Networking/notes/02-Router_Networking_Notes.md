# Router - Networking Notes

## What is a Router?

A router is a Layer 3 device which deals with IP addresses, unlike a switch which is a Layer 2 device and deals with MAC addresses.

A router is used to connect different networks together.

If we already have a switch to connect devices, then why do we need a router?

A switch is mainly used to connect devices within the same network, but when we need to communicate with devices on another network, we need a router.

### Example

- Network A: 192.168.1.0/24
- Network B: 192.168.2.0/24

If a device from Network A wants to communicate with a device on Network B, the traffic must go through a router.

In simple words:

- Switch = Connects devices inside the same network.
- Router = Connects different networks together.

---

## How Does a Router Work?

When Device A wants to send data to Device B on another network, Device A first checks whether the destination is inside its own network.

If the destination is outside the network, Device A sends the packet to its default gateway, which is usually the router.

Before sending the packet, the device uses ARP (Address Resolution Protocol) to find the MAC address of the router.

Once it knows the router's MAC address, it sends the packet to the router.

The router then looks at the destination IP address and decides where to send the packet next until the packet reaches its destination.

---

## What is ARP?

ARP stands for Address Resolution Protocol.

ARP is used to find the MAC address of a device when we already know its IP address.

For example, if a computer wants to send data to its default gateway, it sends an ARP request asking:

"Who has this IP address?"

The device with that IP address replies with its MAC address.

After that, communication can begin.

In simple words, ARP helps devices find the correct MAC address before sending data.

---

## DNS Server

DNS stands for Domain Name System.

When we visit websites like youtube.com or google.com, our devices actually need an IP address to communicate with those servers.

Instead of remembering IP addresses, we simply type the website name.

The device sends a DNS request to a DNS server, and the DNS server responds with the correct IP address.

In simple words:

DNS converts human-readable names into IP addresses.

Example:

- youtube.com → IP Address
- google.com → IP Address

---

## Default Gateway

A default gateway is usually the IP address of the router on our local network.

Whenever a device wants to communicate with another device outside its own network, it sends the traffic to the default gateway.

The router then forwards the traffic to the correct destination network.

You can think of the default gateway as the exit door of your local network.

---

## Cisco CLI Commands

Enter privileged EXEC mode:

```bash
enable
```

Display the routing table:

```bash
show ip route
```

This command shows the routes known by the router and the networks it can reach.

---

## Key Takeaways

- Router works at Layer 3 and uses IP addresses.
- Switch works at Layer 2 and uses MAC addresses.
- Routers connect different networks.
- ARP finds MAC addresses using IP addresses.
- DNS converts domain names into IP addresses.
- Default gateway is usually the router's IP address.
- `show ip route` displays the routing table.
