# 🔍 Subnetting … but in Reverse – Detailed Notes
**Video 8 of NetworkChuck's Subnetting Mastery Series**

## 🎯 The Big Idea
Instead of “I have a network, how do I split it?” – reverse subnetting asks:  
**“I have an IP address and a subnet mask. What network is it part of?”**

This is a **troubleshooting superpower**. When you see a device’s IP config, you need to instantly know its network address, broadcast address, and usable range.

---

## 🔄 Reverse Subnetting – Step by Step

### Step 1 – Find the IP and subnet mask
On the device (or in a config file), get:
- IP address: e.g., `192.168.1.45`
- Subnet mask: e.g., `255.255.255.224`

### Step 2 – Convert to binary (only the interesting octet if possible)
For a `/27` mask (`255.255.255.224`), the 4th octet is the interesting one.

- IP last octet: `45` → binary `00101101`
- Mask last octet: `224` → binary `11100000`

### Step 3 – Perform the AND operation
- **Network bits** in the mask are `1` → they copy the IP’s bits.
- **Host bits** in the mask are `0` → they become `0` in the result.
