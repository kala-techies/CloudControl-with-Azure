# Module 3: Networking Essentials

🛠️ **Skills**: Build and understand virtual networks

---

## 6. IPv4 & Subnetting Basics

Understanding IP addressing is one of the **core and fundamental concepts of networking**. There are two main types of IP addresses: **IPv4 and IPv6**. In this module, we’ll deep dive into **IPv4**.

### IPv4 Public Classes (Before Private IPs Were Introduced)

- **Class A**: `1.0.0.0` to `126.255.255.255`
- **Class B**: `128.0.0.0` to `191.255.255.255`
- **Class C**: `192.0.0.0` to `223.255.255.255`
- **Class D**: `224.0.0.0` to `239.255.255.255` *(Reserved for Multicast)*
- **Class E**: `240.0.0.0` to `255.255.255.255` *(Experimental)*

IPv4 addresses consist of **4 octets (8 bits each)**. For example:

```

0.0.0.0 = 8 bits \* 4 = 32-bit address (/32)

````

Try running:
```bash
ping www.swiggy.com
````

This will resolve to either an **IPv4** or **IPv6** address. If it returns an IPv4 address, it will fall under **Class A to C**, since **Class D & E are reserved**.

---

## 🏡 Home Analogy: How Private IPs Work

As computer usage grew rapidly (especially after Windows became mainstream), the demand for IP addresses exploded. Networking engineers realized that public IPs would eventually **run out**.

So they introduced the concept of **Private IP addresses**.

Imagine this:

> You have 4–5 laptops at home. Each device has its own **private IP address**. But when they connect to your home **Wi-Fi/router**, they are **assigned a single public IP** by your Internet Provider (Jio, Airtel, BSNL, etc.). That’s the IP seen by the internet.

Despite multiple devices, all traffic **goes through one public IP** using **NAT (Network Address Translation)**.

```
[User Devices] --> [Router Gateway] --> [ISP (Jio, Airtel)] --> [Internet]
```

---

### 🖼️ SNAT Visual Representation

![Source NAT (SNAT)](https://github.com/kala-techies/CloudControl-with-Azure/blob/main/PHASE-1_Core-Foundations/Module-03_Networking-Essentials/images/01_SNAT.png)

---

## IPv4 Private IP Address Ranges

These are reserved for internal use within LANs or cloud networks:

* **Class A**: `10.0.0.0` to `10.255.255.255`
* **Class B**: `172.16.0.0` to `172.31.255.255`
* **Class C**: `192.168.0.0` to `192.168.255.255`

These ranges are **not routable on the public internet** — they’re used for internal communications only.

---

## 🧠 Subnetting Made Simple

CIDR Notation (e.g. `/8`, `/16`, `/24`) defines how many **usable IPs** you have in a subnet.

### Examples:

* `10.0.0.0/8` → **\~1 crore IPs**

  * Only `10` is fixed. Remaining 3 octets vary: `256 * 256 * 256 = ~16 million`

* `10.0.0.0/16` → **65,536 IPs**

  * `10.0` is fixed. Last 2 octets vary: `256 * 256 = 65K`

* `10.0.0.0/24` → **256 IPs**

  * `10.0.0` is fixed. Only last octet varies.

> 📌 For every bit you “fix” in the subnet mask, you reduce the number of IPs by half.

### Bit Binary Cheatsheet:

| Binary | Decimal |
| ------ | ------- |
| 000    | 1       |
| 001    | 2       |
| 010    | 4       |
| 100    | 16      |

---

## 7. Create Virtual Networks (VNets)

An **Azure VNet** is a **logical isolation of your cloud network**, just like a physical network in your on-premises datacenter.

* You define the IP range (CIDR block).
* Divide that range into **subnets**.
* Deploy **resources** like VMs, DBs, etc. inside these subnets.

💡 VNets can **connect** with each other via **VNet Peering** or with **on-premises networks** via **VPN** or **ExpressRoute**.

---

## 8. Public vs. Private Subnets

| Type        | Access                                            | Use Case                             |
| ----------- | ------------------------------------------------- | ------------------------------------ |
| **Public**  | Internet-accessible (via NAT Gateway / Public IP) | Frontend web servers, Load Balancers |
| **Private** | No direct internet access                         | Databases, Internal APIs             |

To control traffic:

* Use **NSGs (Network Security Groups)** for port-level filtering
* Use **Route Tables** to override default paths
* Use **NAT Gateways** for secure outbound traffic from private subnets