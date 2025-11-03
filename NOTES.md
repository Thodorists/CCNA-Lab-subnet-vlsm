# CCNA Lab Notes – VLSM & Static Routing

## Lab Overview
- **Goal:** Implement a network using VLSM to optimize IP address usage and configure static routing between routers.
- **Topology:** 2 Routers (R1, R2) + multiple subnets for hosts and links.

---

## 1. IP Addressing Plan (VLSM)

| Subnet | Required Hosts | Network Address | Subnet Mask | First IP | Last IP | Broadcast |
|--------|----------------|----------------|-------------|----------|---------|-----------|
| Subnet A | 64 hosts | 192.168.5.0 | 255.255.255.128 (/25) | 192.168.5.1 | 192.168.5.126 | 192.168.5.127 |
| Subnet B | 45 hosts | 192.168.5.128 | 255.255.255.192 (/26) | 192.168.5.129 | 192.168.5.190 | 192.168.5.191 |
| Subnet C | 14 hosts | 192.168.5.192 | 255.255.255.240 (/28) | 192.168.5.193 | 192.168.5.206 | 192.168.5.207 |
| Subnet D | 9 hosts | 192.168.5.208 | 255.255.255.240 (/28) | 192.168.5.209 | 192.168.5.222 | 192.168.5.222 |
| Subnet D | 2 hosts | 192.168.5.224 | 255.255.255.252 (/30) | 192.168.5.225 | 192.168.5.226 | 192.168.5.227 | this is point to point connection

> Note: Adjust subnet addresses according to your topology.

---

## 2. Router Configurations

### R1
```bash
interface Gig0/0
 ip address 192.168.5.126 255.255.255.128
 no shutdown

interface Gig0/1
 ip address 192.168.5.190 255.255.255.192
 no shutdown

 interface Gig0/2
 ip address 192.168.5.225 255.255.255.252
 no shutdown

ip route 192.168.5.192 255.255.255.240 192.168.5.226
ip route 192.168.5.208 255.255.255.240 192.168.5.226

## R2

interface Gig0/0
 ip address 192.168.5.226 255.255.255.252
 no shutdown

interface Gig0/1
 ip address 192.168.5.206 255.255.255.240
 no shutdown

interface Gig0/2
 ip address 192.168.5.222 255.255.255.240
 no shutdown

ip route 192.168.5.0 255.255.255.128 192.168.5.225
ip route 192.168.5.129 255.255.255.192 192.168.5.225

Το vlsm επιτρέπει να σπας το υποδίκτυο σε μικρότερα μέρη για να είναι πιο αποδοτικό ανάλογα τις ανάγκες και για περισσότερη εξοικονόμιση ip 
Αλλά υπάρχουν και περιπτώσεις που το flsm είναι αυτό που χρειάζεται αν θέλει τον ίδιο αριθμό host σε κάθε subnet
