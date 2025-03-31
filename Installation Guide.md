# 🛠️ Installation Guide

This guide provides step-by-step instructions to install the required tools for the **Firewall Evasion Techniques Analysis** project on **Windows, Kali Linux, and macOS**.

## Tools Required
- **Nmap** – Network scanning tool
- **Wireshark** (optional) – Packet analysis tool
- **Virtual Machine (Optional)** – For testing with different firewall configurations

---
## 🔹 Windows Installation

### 1️⃣ Install Nmap
1. Download the latest Nmap installer from [Nmap official site](https://nmap.org/download.html).
2. Run the installer and follow the setup wizard.
3. Open **Command Prompt (cmd)** and verify the installation:
   ```cmd
   nmap --version
   ```

### 2️⃣ Install Wireshark (Optional)
1. Download **Wireshark** from [Wireshark official site](https://www.wireshark.org/download.html).
2. Run the installer and select "Install WinPcap" and "Npcap" during setup.
3. Open Wireshark and check if it captures network traffic.

---
## 🔹 Kali Linux Installation

### 1️⃣ Install Nmap
Nmap is pre-installed on Kali Linux. If missing, install it using:
```bash
sudo apt update && sudo apt install nmap -y
```
Verify installation:
```bash
nmap --version
```

### 2️⃣ Install Wireshark (Optional)
```bash
sudo apt install wireshark -y
```
Run Wireshark:
```bash
wireshark
```

---
## 🔹 macOS Installation

### 1️⃣ Install Nmap
1. Install **Homebrew** (if not installed):
   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```
2. Install Nmap:
   ```bash
   brew install nmap
   ```
3. Verify installation:
   ```bash
   nmap --version
   ```

### 2️⃣ Install Wireshark (Optional)
```bash
brew install --cask wireshark
```
Open Wireshark:
```bash
open /Applications/Wireshark.app
```

---
## Next Steps
- Ensure all tools are installed and functional.
- Set up a **test machine** with a firewall for scanning.
- Proceed with running **Nmap scans** as described in the project README.
