# Part A Guide: Diamond Topology, OSPF, Verification

This guide is a step-by-step checklist for completing Part A. It uses a diamond topology to verify alternate path usage (Task 4).

**Phase 1: Physical Topology & Planning (Task 1)**

**1. The Setup (Diamond Topology)**
1. Routers: Place 4 routers (e.g., 2911 or 4331). Label them `R1`, `R2`, `R3`, `R4`.
1. Switches: Place 2 switches. Connect one to `R1` and one to `R4`.
1. PCs: Connect `PC1` to `R1`'s switch. Connect `PC2` to `R4`'s switch.

**2. The Connections (Cabling)**
1. `R1` connects to `R2` (Path A).
1. `R1` connects to `R3` (Path B).
1. `R2` connects to `R4`.
1. `R3` connects to `R4`.

Note: You will need Serial (HWIC-2T) cards for these connections if using Packet Tracer.

**3. The IP Address Plan (Subnetting 10.100.0.0/24)**
1. LAN 1 (R1 Side): `10.100.0.1/26` (Network: `10.100.0.0`)
1. LAN 2 (R4 Side): `10.100.0.65/26` (Network: `10.100.0.64`)
1. WAN R1-R2: `10.100.0.129/30`
1. WAN R1-R3: `10.100.0.133/30`
1. WAN R2-R4: `10.100.0.137/30`
1. WAN R3-R4: `10.100.0.141/30`

**Phase 2: Configuration & IP Addressing (Task 1)**

Run these commands on each router.

**Router 1 (R1)**
```bash
enable
conf t
hostname R1
! LAN Interface
interface g0/0
 ip address 10.100.0.1 255.255.255.192
 no shutdown
! Connection to R2
interface s0/0/0
 ip address 10.100.0.129 255.255.255.252
 no shutdown
! Connection to R3
interface s0/0/1
 ip address 10.100.0.133 255.255.255.252
 no shutdown
exit
```

**Router 2 (R2)**
```bash
enable
conf t
hostname R2
! Connection to R1
interface s0/0/0
 ip address 10.100.0.130 255.255.255.252
 no shutdown
! Connection to R4
interface s0/0/1
 ip address 10.100.0.137 255.255.255.252
 no shutdown
exit
```

**Router 3 (R3)**
```bash
enable
conf t
hostname R3
! Connection to R1
interface s0/0/0
 ip address 10.100.0.134 255.255.255.252
 no shutdown
! Connection to R4
interface s0/0/1
 ip address 10.100.0.141 255.255.255.252
 no shutdown
exit
```

**Router 4 (R4)**
```bash
enable
conf t
hostname R4
! LAN Interface
interface g0/0
 ip address 10.100.0.65 255.255.255.192
 no shutdown
! Connection to R2
interface s0/0/0
 ip address 10.100.0.138 255.255.255.252
 no shutdown
! Connection to R3
interface s0/0/1
 ip address 10.100.0.142 255.255.255.252
 no shutdown
exit
```

**PC Configuration**
1. `PC1`: IP `10.100.0.10`, Mask `255.255.255.192`, Gateway `10.100.0.1`
1. `PC2`: IP `10.100.0.70`, Mask `255.255.255.192`, Gateway `10.100.0.65`

**Phase 3: Dynamic Routing - OSPF (Task 2)**

Run this on all routers (`R1`, `R2`, `R3`, `R4`).

```bash
router ospf 1
 network 10.0.0.0 0.255.255.255 area 0
 exit
```

Wait about 30 seconds. You should see neighbor adjacency messages on the console.

**Phase 4: Routing Table Analysis (Task 3)**

**1. Verify Dynamic Routes**
1. On `R1`, run `show ip route`.
1. Confirm you see `C` (Connected) routes for LAN and WAN links.
1. Confirm you see `O` (OSPF) routes, for example:

```text
O 10.100.0.64 [110/3] via 10.100.0.130
```

**2. Packet Forwarding Check**
1. On `PC1`, open Command Prompt.
1. Run `ping 10.100.0.70`.
1. Run `tracert 10.100.0.70`.

Expected: The path should be `R1 -> R2 -> R4 -> PC2` or `R1 -> R3 -> R4 -> PC2`.

**Phase 5: Routing Failure & Convergence (Task 4)**

**1. Check Current Path**
1. On `PC1`, run `tracert 10.100.0.70`.
1. Note the path (for example `R1 -> R2 -> R4`).

**2. Break the Link**
1. On `R2`, shut down the interface facing `R1`.

```bash
R2(config)# int s0/0/0
R2(config-if)# shutdown
```

**3. Verify Reconvergence**
1. Wait 5 to 10 seconds.
1. On `R1`, run `show ip route` and confirm the route to `10.100.0.64/26` still exists.
1. On `PC1`, run `tracert 10.100.0.70` again.

Expected: The path should switch to `R1 -> R3 -> R4`.

**Phase 6: Troubleshooting (Task 5)**

Scenario: `PC1` cannot ping `PC2`.

**1. Identify the Issue**
1. `ping 10.100.0.70` fails (Destination Unreachable).
1. On `R1`, `show ip route` shows the route to `10.100.0.64/26` is missing.
1. On `R1`, `show ip protocols` indicates the network is not being advertised.

**2. Common Fix**
If you forgot to advertise `R4`'s LAN, `R1` will never learn it.

Run on `R4`:
```bash
router ospf 1
 network 10.0.0.0 0.255.255.255 area 0
```

**3. Verify**
1. On `R1`, `show ip route` should display the `O` route again.
1. `ping 10.100.0.70` should succeed.
