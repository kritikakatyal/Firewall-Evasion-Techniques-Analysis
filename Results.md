# Firewall Evasion Test Results  

This document contains the results of different **Nmap scanning techniques** against a firewall with basic filtering rules enabled.

---

## **Test Environment**
- **Target System:** Ubuntu 22.04 with `iptables` firewall enabled
- **Firewall Rules:**
  - Block **SYN scans** (port scanning detection enabled)
  - Allow only traffic on ports `22 (SSH)`, `80 (HTTP)`, `443 (HTTPS)`
  - Drop fragmented packets
  - Log unusual scan attempts

---

## **Scan Results**

| **Scan Type**           | **Firewall Response**                          | **Output** |
|-------------------------|-----------------------------------------------|------------|
| **TCP Connect Scan**    | ❌ **Detected & Blocked**                     | Nmap scan report for <target-ip>  
PORT   STATE    SERVICE  
22/tcp open     ssh  
80/tcp open     http  
443/tcp open    https  
Other ports: filtered |
| **SYN Scan**           | ❌ **Blocked (Detected by firewall logs)**    | Nmap scan report for <target-ip>  
All scanned ports on <target-ip> are filtered |
| **NULL Scan**          | ✅ **Bypassed (No response from firewall)**   | Nmap scan report for <target-ip>  
PORT   STATE    SERVICE  
22/tcp open     ssh  
80/tcp open     http  
443/tcp open    https |
| **FIN Scan**           | ✅ **Bypassed (No response from firewall)**   | Nmap scan report for <target-ip>  
All scanned ports on <target-ip> appear to be closed |
| **Xmas Scan**          | ❌ **Blocked (Detected by firewall logs)**    | Nmap scan report for <target-ip>  
All scanned ports on <target-ip> are filtered |
| **Fragmentation Scan** | ⚠️ **Partially Blocked (Some fragments dropped)** | Nmap scan report for <target-ip>  
Some fragmented packets were dropped by firewall. |
| **Decoy Scan**         | ⚠️ **Some decoys detected in firewall logs**  | Nmap scan report for <target-ip>  
Firewall logs show multiple source IPs, but scan was detected |
| **Idle Scan**          | ✅ **Completely Undetected**                  | Nmap scan report for <target-ip>  
Appears as if no scan occurred (no logs detected) |

---

## **Key Findings**
- **SYN and Xmas scans** were **detected and blocked** by the firewall.
- **NULL and FIN scans** successfully bypassed detection but returned limited results.
- **Fragmentation scans** had **mixed success**, as the firewall **dropped some packets**.
- **Idle Scan was the most stealthy** and left **no trace in firewall logs**.
- **Decoy Scan added noise**, but the firewall still detected scanning attempts.

---

## **Next Steps:**
- Improve stealth techniques by **tweaking packet timing (`--scan-delay`)**.
- Experiment with **tunneling methods (e.g., HTTP, DNS tunneling)**.
- Test against **different firewall brands (pfSense, Cisco ASA, etc.)**.

Check **[Scanning.md](SCANS.md)** for more details! 🚀
