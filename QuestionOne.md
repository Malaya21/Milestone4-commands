# Coding Question 1 – Complete Commands

**Topology:**
```
PC0 — Switch0 — R1 —(WAN)— R2 — Switch1 — PC1
```

---

## 🔹 BASIC SETUP (DO ON BOTH ROUTERS)

### R1
```
enable
configure terminal
hostname R1
no ip domain-lookup
```

### R2
```
enable
configure terminal
hostname R2
no ip domain-lookup
```

---

## 🔹 TASK 1: LAN IP ADDRESSING

### ▶️ R1 – LAN-A (192.168.100.0/25)
```
interface g0/0
 ip address 192.168.100.1 255.255.255.128
 no shutdown
```

### ▶️ R2 – LAN-B (192.168.100.128/25)
```
interface g0/0
 ip address 192.168.100.129 255.255.255.128
 no shutdown
```

---

## 🔹 TASK 3: WAN CONFIGURATION (PPP + CHAP)

### ▶️ WAN IPs (/30)

**R1**
```
interface s0/0/0
 ip address 10.0.0.1 255.255.255.252
 encapsulation ppp
 no shutdown
```

**R2**
```
interface s0/0/0
 ip address 10.0.0.2 255.255.255.252
 encapsulation ppp
 no shutdown
```

### ▶️ CHAP AUTHENTICATION

**R1**
```
username R2 password cisco
interface s0/0/0
 ppp authentication chap
```

**R2**
```
username R1 password cisco
interface s0/0/0
 ppp authentication chap
```

### ▶️ VERIFY PPP
```
show interfaces s0/0/0
```

**Must show:**
- Encapsulation PPP
- LCP Open

---

## 🔹 TASK 2: STATIC ROUTING + FLOATING ROUTE

### ▶️ R1
```
ip route 192.168.100.128 255.255.255.128 10.0.0.2
ip route 192.168.100.128 255.255.255.128 10.0.0.2 200
```

### ▶️ R2
```
ip route 192.168.100.0 255.255.255.128 10.0.0.1
ip route 192.168.100.0 255.255.255.128 10.0.0.1 200
```

### ▶️ VERIFY ROUTING
```
show ip route
```

---

## 🔹 TASK 4: DHCP + NAT (ONLY ON R1)

### ▶️ DHCP CONFIGURATION
```
ip dhcp excluded-address 192.168.100.1 192.168.100.10

ip dhcp pool LAN-A
 network 192.168.100.0 255.255.255.128
 default-router 192.168.100.1
 dns-server 8.8.8.8
```

### ▶️ NAT CONFIGURATION
```
access-list 1 permit 192.168.100.0 0.0.0.127

interface g0/0
 ip nat inside

interface s0/0/0
 ip nat outside

ip nat inside source list 1 interface s0/0/0 overload
```

### ▶️ VERIFY DHCP & NAT
```
show ip dhcp binding
show ip nat translations
```

---

## 🔹 PC CONFIGURATION

### ▶️ PC0 (LAN-A)
```
IP configuration → DHCP
```

### ▶️ PC1 (LAN-B)
```
IP address: 192.168.100.130
Subnet: 255.255.255.128
Gateway: 192.168.100.129
```

### ▶️ CONNECTIVITY TEST

**From PC0:**
```
ping 192.168.100.130
```

**From PC1:**
```
ping 192.168.100.1
```

---

## 🔹 TASK 5: HSRP (ONLY IF ASKED – SAME LAN REQUIRED)

⚠️ Requires both routers on same switch (you already practiced this)

### R1
```
interface g0/0
 standby 1 ip 192.168.100.254
 standby 1 priority 110
 standby 1 preempt
```

### R2
```
interface g0/0
 standby 1 ip 192.168.100.254
 standby 1 priority 100
 standby 1 preempt
```

### Verify:
```
show standby
```

---

## ✅ FINAL VERIFICATION COMMANDS (SUBMISSION)

```
show ip route
show interfaces
show ip nat translations
show ip dhcp binding
```

---

## 🧠 EXAM TIP (VERY IMPORTANT)

If something fails:

```
show ip interface brief
```

Check:
1. IP
2. Routing
3. NAT / DHCP
