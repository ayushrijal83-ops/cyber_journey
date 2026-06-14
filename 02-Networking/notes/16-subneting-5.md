
So the **network address** is `192.168.1.32`.

### Step 4 – Find the rest of the subnet details
- **Subnet size** = `2ⁿ` where `n` = number of host bits (mask has 5 host bits here) → `2⁵ = 32` IPs per subnet.
- **Network ID** = `192.168.1.32`
- **First usable** = Network ID + 1 → `192.168.1.33`
- **Last usable** = Broadcast – 1
- **Broadcast address** = Network ID + (subnet size – 1) = `32 + 31 = 63` → `192.168.1.63`

### Step 5 – Verify the original IP fits
`192.168.1.45` is between `.33` and `.62` → ✅ correct.

---

## 🧠 Why Reverse Subnetting Matters

| Scenario                          | What you do with reverse subnetting                           |
|-----------------------------------|---------------------------------------------------------------|
| You see a laptop with IP .45/27   | You instantly know the subnet is .32 – .63, broadcast .63     |
| Two devices can’t ping            | Check if they’re in the same subnet (compare network IDs)     |
| You’re given a random IP          | You can find its network without drawing the whole scheme     |

> **Real world**: `ipconfig` (Windows) or `ifconfig` / `ip a` (Linux) gives you the mask. Reverse subnetting tells you everything else.

---

## 📐 Quick Reference – Common Masks & Increments

| CIDR | Mask           | Host bits | Subnet size | Magic number |
|------|----------------|-----------|-------------|---------------|
| /24  | 255.255.255.0  | 8         | 256         | 1             |
| /25  | 255.255.255.128| 7         | 128         | 128           |
| /26  | 255.255.255.192| 6         | 64          | 64            |
| /27  | 255.255.255.224| 5         | 32          | 32            |
| /28  | 255.255.255.240| 4         | 16          | 16            |
| /29  | 255.255.255.248| 3         | 8           | 8             |
| /30  | 255.255.255.252| 2         | 4           | 4             |

> **Using the table**: If you see mask `.224`, increment = 32. So subnets are 0, 32, 64, 96, etc. Network ID is the multiple of 32 just below the IP’s last octet.

---

## 💡 Practice Example (Reverse)
**Problem**: IP = `10.20.30.150`, mask = `255.255.255.192`  
- Interesting octet: 4th – value 150.  
- Magic number = `256 – 192 = 64`.  
- Network IDs: 0, 64, 128, 192.  
- 150 lies between 128 and 192 → network ID = `10.20.30.128`.  
- Broadcast = `.128 + 63 = .191`.  
- Range = `.129 – .190`. ✅

> 🔥 **Pro tip**: You don’t always need binary. Use the magic number method for speed – but binary is your safety net.