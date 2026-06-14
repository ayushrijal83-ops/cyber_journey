# ☕ Subnetting My Coffee Shop – Detailed Notes
**Video 7 of NetworkChuck's Subnetting Mastery Series**

## 🎯 The Big Idea
Most subnetting examples focus on *how many subnets* you need. But real life asks a different question: **How many hosts do I need per subnet?**  
This video walks through a real-world café scenario: subnetting a single `/24` network to serve three coffee shops, each with ~30 devices.

---

## 🏪 The Scenario
You have one `10.1.1.0/24` network (256 total IPs, 254 usable). You need to split it for **three coffee shops**.

### Each shop’s devices:
| Device Type          | Count |
|----------------------|-------|
| Employees (wired)    | 5     |
| Server               | 1     |
| Raspberry Pi         | 2     |
| Wireless Access Point| 2     |
| Guest Wi-Fi devices  | 20    |
| **Total per shop**   | **30** |

> **Growth buffer**: You add 10 extra IPs per shop → target **40 hosts per subnet**.

---

## 🧮 The Method – Subnetting by Host Count

### Step 1 – Use the formula
Usable hosts in a subnet = `2ⁿ – 2`  
where `n` = number of **host bits**.

### Step 2 – Find the smallest n that meets your need
- `n = 5` → `2⁵ – 2 = 30` hosts → ❌ too small for 40.
- `n = 6` → `2⁶ – 2 = 62` hosts → ✅ perfect (room for growth).

### Step 3 – Derive the subnet mask
- IPv4 address has 32 bits total.
- If `n = 6` host bits, then network bits = `32 – 6 = 26`.
- New CIDR: **/26**  
- Subnet mask: **255.255.255.192**  
  (Binary: `11111111.11111111.11111111.11000000`)

### Step 4 – Find the magic number (increment)
- The interesting octet is the 4th octet.
- Value of the last network bit = `2⁶ = 64` (or `256 – 192 = 64`).
- Subnets increment by **64** in the last octet.

---

## 📊 Subnet Allocation Table

| Coffee Shop | Network ID    | Usable IP Range                 | Broadcast      |
|-------------|---------------|---------------------------------|----------------|
| Shop 1      | 10.1.1.0/26   | 10.1.1.1   – 10.1.1.62          | 10.1.1.63      |
| Shop 2      | 10.1.1.64/26  | 10.1.1.65  – 10.1.1.126         | 10.1.1.127     |
| Shop 3      | 10.1.1.128/26 | 10.1.1.129 – 10.1.1.190         | 10.1.1.191     |
| Unused      | 10.1.1.192/26 | 10.1.1.193 – 10.1.1.254         | 10.1.1.255     |

> ✅ Each subnet provides **62 usable IPs** – plenty for 40 devices.

---

## 💡 Key Takeaways
- When you need to design subnets for a given number of **hosts**, work backwards:  
  `required hosts ≤ 2ⁿ – 2` → choose smallest `n`.
- The **magic number** (increment) = `256 – subnet mask value in the interesting octet`.
- Always leave room for growth – never design for exactly today’s count.
- This is the foundation of **VLSM** (Variable Length Subnet Masks), covered in the final test video.

> 🔥 **Pro tip**: This exact method is what you’ll use when setting up a real office, school, or small business network.