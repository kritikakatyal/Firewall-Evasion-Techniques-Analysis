# Firewall Evasion Techniques Analysis

## Project Overview
This project analyzes how a firewall reacts to different **Nmap scanning techniques**. By performing various scans, we assess the effectiveness of firewall rules and explore ways to bypass or evade detection.

## Objectives
- Understand firewall behavior against different scan types.
- Learn how firewalls block or detect scans.
- Document the findings and provide insights.

## 🛠️ Tools & Requirements
- **Operating System**: Linux (Recommended: Kali Linux, ParrotOS)
- **Tools**: 
  - [Nmap](https://nmap.org/download.html)
  - Wireshark (Optional, for deeper packet analysis)
- **Target**: A test machine with an active firewall (Can use a VM with UFW, iptables, or pfSense)

## Steps to Complete the Project

### 1️⃣ Setup Environment
- Install **Nmap**: `sudo apt install nmap`
- Set up a **target VM** with a firewall (e.g., Ubuntu with UFW)
- Configure firewall rules to block different types of scans

### 2️⃣ Perform Nmap Scans & Analyze Firewall Reaction
Perform the following scans and observe firewall responses:

- **TCP Connect Scan**: `nmap -sT <target>`
- **SYN Scan** (Stealth scan): `nmap -sS <target>`
- **Null Scan**: `nmap -sN <target>`
- **FIN Scan**: `nmap -sF <target>`
- **Xmas Scan**: `nmap -sX <target>`
- **Fragmented Packets Scan**: `nmap -f <target>`
- **Decoy Scan**: `nmap -D RND:5 <target>`
- **IP Spoofing Scan**: `nmap -S <spoofed-IP> <target>`
- **Custom Packet Scan**: `nmap --scanflags URGACKPSH <target>`

### 3️⃣ Capture and Analyze Traffic
- Use **Wireshark** or `tcpdump` to monitor packets
- Compare results with different firewall configurations
- Document how the firewall reacts to each scan type

### 4️⃣ Document Findings & Insights
- Create a **report** summarizing scan results
- Suggest possible firewall improvements

## 📂 Project Structure
```
📁 Firewall-Evasion-Analysis
 ├── 📜 README.md  # Project documentation
 ├── 📜 installation.md # installation process and steps
 ├── 📜 scans.sh   # Bash script to automate scans
 ├── 📜 results.md    # Findings & analysis
 ├── 📁 reports    # Logs, screenshots, Wireshark captures
```

## How to Run
1. Clone this repository:  
   ```bash
   git clone https://github.com/yourusername/Firewall-Evasion-Analysis.git
   ```
2. Navigate to the project folder:  
   ```bash
   cd Firewall-Evasion-Analysis
   ```
3. Run the scan script (modify as needed):  
   ```bash
   chmod +x scans.sh
   ./scans.sh
   ```

## Contribution
Feel free to **fork** this repo, open **issues**, or submit **pull requests**. 

## ⚠️ Disclaimer
This project is for **educational purposes only**. Do not perform unauthorized scans. Always obtain permission before testing on any network.
