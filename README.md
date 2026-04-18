# 🐧 Kali VM Network Incident & Fix Report

![Kali Linux](https://img.shields.io/badge/Kali-Linux-557C94?style=for-the-badge&logo=kalilinux&logoColor=white)
![VirtualBox](https://img.shields.io/badge/VirtualBox-Network%20Fix-183A61?style=for-the-badge&logo=virtualbox)
![Status](https://img.shields.io/badge/Status-Resolved-success?style=for-the-badge)
![Networking](https://img.shields.io/badge/Networking-Troubleshooting-blue?style=for-the-badge)

---

## 🧾 Incident Summary

This project documents a real-world troubleshooting scenario involving **network connectivity failure in a Kali Linux virtual machine running on Oracle VM VirtualBox**.

The system initially experienced **partial connectivity (gateway reachable but no internet access)** due to misconfigured network adapters and routing conflicts.

---

## 🚨 Problem Statement

The Kali Linux VM exhibited the following issues:

- ❌ No internet access inside VM
- ❌ Packet loss on external requests
- ❌ Incorrect IP assignment (`192.168.x.x`)
- ❌ DNS resolution failure
- ❌ VPN (Cloudflare WARP) routing conflicts

---

## 🔍 Root Cause Analysis

The issue was caused by multiple misconfigurations:

- Bridged Adapter incorrectly set (Thunderbolt/Wi-Fi)
- NAT mode not properly applied
- VPN service interfering with routing tables
- DNS and gateway mismatch
- VirtualBox network misalignment

---

## 🛠️ Resolution Steps

### 1️⃣ Network Reset in Kali Linux
```bash
sudo systemctl restart NetworkManager
sudo dhclient -r eth0
sudo dhclient eth0
2️⃣ Disabled VPN Conflicts
sudo systemctl stop warp-svc
sudo systemctl disable warp-svc
3️⃣ Verified Network Interface
ip a
Expected correct NAT result:
10.0.2.x IP range
4️⃣ Fixed VirtualBox Configuration
Changed Adapter 1 → NAT Mode
Enabled Cable Connected
Restarted VM
5️⃣ Connectivity Validation
ping -c 4 8.8.8.8
ping -c 4 google.com
| Component        | Status     |
| ---------------- | ---------- |
| Internet Access  | ✅ Working  |
| DNS Resolution   | ✅ Fixed    |
| IP Configuration | ✅ Stable   |
| Routing          | ✅ Correct  |
| VM Network       | ✅ NAT Mode |
Host (macOS)
     │
     ▼
VirtualBox NAT Network
     │
     ▼
Kali Linux VM
     │
     ├── DNS (8.8.8.8 / 1.1.1.1)
     ├── Internet Access
     └── Network Interface (eth0)
     🎯 Key Learnings
NAT vs Bridged networking behavior in VirtualBox
Linux network troubleshooting commands
DNS and routing diagnostics
VPN interference impact on VM networking
Real-world VM debugging workflow
🚀 Tools Used
Kali Linux
Oracle VM VirtualBox
NetworkManager
Linux CLI tools (ip, dhclient, ping)
Systemd services
📌 Conclusion
The issue was successfully resolved by switching to NAT networking mode and removing VPN routing conflicts, restoring full internet connectivity in the virtualized Kali Linux environment.

---

# 🚀 If you want next level upgrade

I can also help you turn this into:

🔥 1. **:contentReference[oaicite:0]{index=0}**
🔥 2. **:contentReference[oaicite:1]{index=1}**
🔥 3. **:contentReference[oaicite:2]{index=2}**
🔥 4. **:contentReference[oaicite:3]{index=3}**

Just tell me 👍
