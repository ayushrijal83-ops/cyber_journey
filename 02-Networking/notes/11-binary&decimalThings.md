# Binary ↔ Decimal Conversion & Subnetting Basics
## *Completing the Notes from SUBNETING1.pdf*

---

## 📌 Why Binary?

Computers don’t understand decimal numbers directly – they work with **binary** (0s and 1s).  
In networking, **IP addresses** and **subnet masks** are ultimately processed as binary strings.  
Understanding binary ↔ decimal conversion is the **first step** to mastering subnetting.

> 💡 **Binary = ON (1) / OFF (0)** – the language of every digital device.

---

## 🔁 The 8‑Bit Table (Positional Values)

Each octet of an IPv4 address is **8 bits**.  
We use this table to convert:

| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
|-----|----|----|----|---|---|---|---|

> Note: these are powers of 2 (2⁷ down to 2⁰).

---

## 🧮 Decimal → Binary (Subtraction Method)

Let’s correctly convert the first octet `192` from the IP `192.168.1.0`.

### Step‑by‑step for 192

| Bit value | Subtract? | Remainder | Binary bit |
|-----------|-----------|-----------|-------------|
| 128       | 192 ≥ 128 → 192 - 128 = 64 | 64 | 1 |
| 64        | 64 ≥ 64 → 64 - 64 = 0 | 0 | 1 |
| 32        | 0 ≥ 32? ❌ | 0 | 0 |
| 16        | 0 ≥ 16? ❌ | 0 | 0 |
| 8         | 0 ≥ 8? ❌  | 0 | 0 |
| 4         | 0 ≥ 4? ❌  | 0 | 0 |
| 2         | 0 ≥ 2? ❌  | 0 | 0 |
| 1         | 0 ≥ 1? ❌  | 0 | 0 |

✅ **192 in binary = `11000000`**

> **Correction from original notes:**  
> After subtracting 128 and 64, the remainder becomes **0**. There is *no* need to subtract 32, 16, etc. The earlier mention of “16 divisible by 32” was a typo – we always compare the *current remainder* with the next bit value.

---

## 🔢 Binary → Decimal (Using the Table)

To convert binary `11000000` back to decimal:  
- `1 × 128 = 128`  
- `1 × 64 = 64`  
- All other bits are 0.  

**128 + 64 = 192** ✅

---

## 🌐 Complete Example: IP 192.168.1.0

Now convert **all four octets** to binary.

| Octet | Decimal | Binary (8 bits) |
|-------|---------|------------------|
| 1     | 192     | `11000000`       |
| 2     | 168     | `10101000`       |
| 3     | 1       | `00000001`       |
| 4     | 0       | `00000000`       |

So the full binary representation is:

> `11000000.10101000.00000001.00000000`

### 🔁 Verify 168 → Binary

| Bit | Compare | Remainder | Bit |
|-----|---------|-----------|-----|
| 128 | 168 ≥ 128 → 168-128=40 | 40 | 1 |
| 64  | 40 ≥ 64? ❌ | 40 | 0 |
| 32  | 40 ≥ 32 → 40-32=8 | 8 | 1 |
| 16  | 8 ≥ 16? ❌ | 8 | 0 |
| 8   | 8 ≥ 8 → 8-8=0 | 0 | 1 |
| 4   | 0 ≥ 4? ❌ | 0 | 0 |
| 2   | 0 ≥ 2? ❌ | 0 | 0 |
| 1   | 0 ≥ 1? ❌ | 0 | 0 |

Binary: `10101000` ✅

---

## 🧠 Why This Matters for Subnetting

A **subnet mask** (e.g., `255.255.255.0`) is also a 32‑bit binary number.  
Routers perform a **bitwise AND** between IP address and mask to find the **network address**.

### Example with /24 mask (`255.255.255.0`)

| Item | Decimal | Binary |
|------|---------|--------|
| IP       | 192.168.1.0   | `11000000.10101000.00000001.00000000` |
| Mask     | 255.255.255.0 | `11111111.11111111.11111111.00000000` |
| AND → Network | 192.168.1.0 | `11000000.10101000.00000001.00000000` |

- **Network address**: `192.168.1.0`  
- **Usable hosts**: 2⁸ – 2 = 254 (from `.1` to `.254`)  
- **Broadcast address**: `192.168.1.255`

> ⚠️ The first and last addresses in any subnet are reserved (network & broadcast).

---

## 📘 Quick Reference: Common IP Ranges in Binary

| Decimal | Binary       |
|---------|--------------|
| 255     | `11111111`   |
| 254     | `11111110`   |
| 192     | `11000000`   |
| 168     | `10101000`   |
| 128     | `10000000`   |
| 1       | `00000001`   |
| 0       | `00000000`   |

---

## ✍️ Practice Yourself

Convert the following to binary (check your answers later):

1. **10.0.0.1**  
2. **172.16.5.33**  
3. **255.255.248.0** (subnet mask)

<details>
<summary>✅ Answers (click to reveal)</summary>

1. `00001010.00000000.00000000.00000001`  
2. `10101100.00010000.00000101.00100001`  
3. `11111111.11111111.11111000.00000000`

</details>

---

## 🚀 Next Steps

Now that you’ve mastered binary ↔ decimal conversion, you can move on to:

- **CIDR notation** (e.g., `/24`)  
- **Subnetting** (borrowing bits, creating smaller networks)  
- **VLSM** (Variable Length Subnet Masks)

> 📂 This document completes the notes from `SUBNETING1.pdf`.  
> Keep practicing – binary will soon become second nature!

---

*Happy subnetting! 🧩*