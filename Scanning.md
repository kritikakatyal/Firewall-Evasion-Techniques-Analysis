# Firewall Evasion Scan Execution Guide

This document provides a **detailed and technical** step-by-step guide on how to execute the **Firewall Evasion Techniques Analysis** project. Follow these instructions carefully to ensure the correct execution of scans from the cloned GitHub repository.

---
## Prerequisites
Before running scans, ensure that:
- **Nmap** is installed (Refer to `installation.md`).
- You have a **test target machine** with a firewall (e.g., a VM running **UFW, iptables, pfSense, or Windows Defender Firewall**).
- You have permission to scan the target machine to avoid legal issues.
- A network monitoring tool such as **Wireshark** or **tcpdump** is installed.

---
## Steps to Execute the Project

### 1️⃣ Clone the GitHub Repository
```bash
git clone https://github.com/yourusername/Firewall-Evasion-Analysis.git
cd Firewall-Evasion-Analysis
```
This repository contains the necessary scripts and documentation for executing firewall evasion tests.

### 2️⃣ Set Up the Target Machine
A **target machine** is required for testing firewall evasion techniques. 

#### Linux (Ubuntu/Kali) Firewall Setup (UFW)
1. **Enable UFW:**
   ```bash
   sudo ufw enable
   ```
2. **Set basic firewall rules:**
   ```bash
   sudo ufw default deny incoming
   sudo ufw default allow outgoing
   sudo ufw allow 80/tcp   # Allow HTTP traffic
   sudo ufw allow 22/tcp   # Allow SSH for remote access
   sudo ufw deny 443/tcp   # Block HTTPS traffic (Example rule)
   ```
3. **Check firewall status:**
   ```bash
   sudo ufw status verbose
   ```

#### Windows Firewall Setup (Windows Defender Firewall)
1. Open **Windows Defender Firewall with Advanced Security**.
2. Create a **new inbound rule** to block a specific port (e.g., block port 3389 for RDP):
   - Select **New Rule** > **Port** > **TCP 3389** > **Block the connection** > **Apply**.
3. Verify the rule by running:
   ```powershell
   Get-NetFirewallRule | Where-Object { $_.DisplayName -like '*3389*' }
   ```

### 3️⃣ Execute Nmap Scans
Use the following Nmap scans to analyze firewall behavior. 

#### ✅ **Basic TCP Connect Scan** (Detect open ports with a full TCP handshake)
```bash
nmap -sT <target-ip>
```
- Expected result: Open ports will respond with a **SYN-ACK**, and closed ports will reply with **RST**.

#### ✅ **SYN Scan (Stealth Scan)** (Avoid logging in certain firewalls)
```bash
nmap -sS <target-ip>
```
- Expected result: If allowed, the target will respond with a **SYN-ACK**, but the connection won’t complete.

#### ✅ **Null Scan** (Bypass poorly configured firewalls by sending no flags)
```bash
nmap -sN <target-ip>
```
- Expected result: Firewalls without proper stateful tracking may not log this.

#### ✅ **FIN Scan** (Bypass some firewalls by sending a FIN flag alone)
```bash
nmap -sF <target-ip>
```
- Expected result: Open ports **ignore** FIN packets, while closed ports send **RST**.

#### ✅ **Xmas Scan** (Evasion technique using FIN, URG, and PSH flags)
```bash
nmap -sX <target-ip>
```
- Expected result: Can detect firewalls that block normal SYN scans.

#### ✅ **Fragmented Packets Scan** (Bypass packet inspection firewalls)
```bash
nmap -f <target-ip>
```
- Expected result: Some firewalls will fail to reassemble fragmented packets.

#### ✅ **Decoy Scan** (Conceal your identity by spoofing decoy IPs)
```bash
nmap -D RND:5 <target-ip>
```
- Expected result: Firewall logs multiple IPs instead of a single attacker IP.

#### ✅ **IP Spoofing Scan** (Spoof your source IP address)
```bash
nmap -S <spoofed-ip> <target-ip>
```
- Expected result: If successful, firewall logs show the **spoofed** IP instead of the attacker's real IP.

#### ✅ **Custom Packet Scan** (Define specific TCP flags to evade detection)
```bash
nmap --scanflags URGACKPSH <target-ip>
```
- Expected result: If configured incorrectly, firewalls may fail to block these packets.

### 4️⃣ Capture & Analyze Traffic

To analyze firewall responses, use **Wireshark** or **tcpdump**:

#### **Wireshark**
1. Open Wireshark.
2. Select the network interface (e.g., `eth0` for wired connections).
3. Start capturing packets and apply filters:
   ```
   tcp.port == 80
   ```
   or
   ```
   ip.addr == <target-ip>
   ```
4. Observe responses and analyze logs.

#### **tcpdump** (For command-line packet analysis)
```bash
sudo tcpdump -i eth0 port 80 -nn
```
- This captures TCP traffic on port 80 for analysis.

### 5️⃣ Document Findings
- Record which scan techniques were **successful** in bypassing the firewall.
- Note how firewall logs record the scans.
- Suggest potential firewall **improvements** based on the results.

---
## Conclusion
By performing these scans and analyzing firewall responses, we can identify weaknesses in firewall configurations and enhance security measures.

**Next Steps:**
- Adjust firewall rules to improve detection and blocking.
- Run advanced tests using **intrusion detection systems (IDS)**.
- Document results for future security hardening efforts.

⚠️ **Legal Notice:** Always obtain permission before scanning any network! Unauthorized scanning can result in legal consequences.
