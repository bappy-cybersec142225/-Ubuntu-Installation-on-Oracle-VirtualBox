<img width="1536" height="1024" alt="ChatGPT Image Jun 26, 2026, 07_36_01 PM" src="https://github.com/user-attachments/assets/70660600-25c5-4536-9dfa-c8e6ac30d565" />

# 🐧 Ubuntu 24.04 LTS Installation on Oracle VirtualBox (Windows 11)

### Complete Step-by-Step Guide with Commands for Cybersecurity, SOC, and IT Audit Labs

![Ubuntu](https://img.shields.io/badge/Ubuntu-24.04_LTS-E95420?style=for-the-badge\&logo=ubuntu\&logoColor=white)
![VirtualBox](https://img.shields.io/badge/Oracle-VirtualBox-183A61?style=for-the-badge\&logo=virtualbox\&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-Beginner-green?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)

---

# 📖 Introduction

Ubuntu is one of the most popular Linux distributions and is widely used by SOC analysts, cybersecurity professionals, penetration testers, cloud engineers, and IT auditors. Running Ubuntu inside Oracle VirtualBox allows you to safely create an isolated environment for learning, testing, and building professional security labs without modifying your Windows installation.

---

# 🎯 Project Objectives

* Install Oracle VirtualBox
* Create an Ubuntu virtual machine
* Install Ubuntu 24.04 LTS
* Configure networking
* Install VirtualBox Guest Additions
* Update the operating system
* Install common administration tools
* Prepare the VM for Wazuh, Splunk, Docker, Elastic, Suricata, and other cybersecurity tools

---

# 💻 Lab Environment

| Component  | Value                    |
| ---------- | ------------------------ |
| Host OS    | Windows 11 (64-bit)      |
| Hypervisor | Oracle VirtualBox        |
| Guest OS   | Ubuntu Desktop 24.04 LTS |
| CPU        | 4 vCPUs                  |
| RAM        | 8 GB                     |
| Disk       | 100 GB (Dynamic VDI)     |
| Network    | NAT                      |

---

# Step 1 – Enable Hardware Virtualization

Restart your computer and enter the BIOS/UEFI settings.

Enable one of the following:

* Intel VT-x
* Intel VT-d (optional)
* AMD-V / SVM Mode

Save the settings and reboot.

---

# Step 2 – Install Oracle VirtualBox

1. Install VirtualBox.
2. Install the VirtualBox Extension Pack.
3. Restart Windows if prompted.

---

# Step 3 – Download Ubuntu ISO

Download **Ubuntu Desktop 24.04 LTS (64-bit)** and save the ISO file.

---

# Step 4 – Create a Virtual Machine

Create a new VM with these settings:

| Setting   | Value                 |
| --------- | --------------------- |
| Name      | Ubuntu-24             |
| Type      | Linux                 |
| Version   | Ubuntu (64-bit)       |
| RAM       | 8192 MB               |
| CPU       | 4                     |
| Disk Type | VDI                   |
| Storage   | Dynamically Allocated |
| Disk Size | 100 GB                |

---

# Step 5 – Configure Virtual Machine

### System

* Disable Floppy
* Enable EFI (optional)
* Enable PAE/NX

### Display

* Video Memory: 128 MB
* Enable 3D Acceleration

### Network

* Adapter 1: NAT

### Shared Clipboard

Bidirectional

### Drag & Drop

Bidirectional

---

# Step 6 – Mount Ubuntu ISO

Storage → Empty Optical Drive → Choose the Ubuntu ISO.

Click **Start**.

---

# Step 7 – Install Ubuntu

Choose **Install Ubuntu** and follow the installer.

Recommended options:

* Language: English
* Keyboard: English (US)
* Install third-party software: Yes
* Download updates while installing: Yes (optional)
* Installation type: Erase disk and install Ubuntu (this only affects the virtual disk)

Create your user account and complete the installation.

---

# Step 8 – Update Ubuntu

Open Terminal (`Ctrl + Alt + T`) and run:

```bash
sudo apt update
```

Upgrade installed packages:

```bash
sudo apt upgrade -y
```

Remove unnecessary packages:

```bash
sudo apt autoremove -y
```

Clean cached package files:

```bash
sudo apt clean
```

Check Ubuntu version:

```bash
lsb_release -a
```

Check kernel version:

```bash
uname -r
```

Display system information:

```bash
hostnamectl
```

---

# Step 9 – Install Essential Packages

```bash
sudo apt install -y \
curl \
wget \
git \
vim \
nano \
htop \
net-tools \
tree \
zip \
unzip \
software-properties-common \
apt-transport-https \
ca-certificates \
gnupg \
build-essential
```

Verify installations:

```bash
git --version
curl --version
wget --version
htop --version
```

---

# Step 10 – Install VirtualBox Guest Additions

Install required build tools:

```bash
sudo apt update
```

```bash
sudo apt install -y build-essential dkms linux-headers-$(uname -r)
```

In the VirtualBox menu:

```
Devices
→ Insert Guest Additions CD Image
```

Mount the CD (if not mounted automatically):

```bash
sudo mkdir -p /media/cdrom
```

```bash
sudo mount /dev/cdrom /media/cdrom
```

Run the installer:

```bash
cd /media/cdrom
```

```bash
sudo ./VBoxLinuxAdditions.run
```

Restart Ubuntu:

```bash
sudo reboot
```

---

# Step 11 – Verify Network Connectivity

Show IP addresses:

```bash
ip a
```

Show routing table:

```bash
ip route
```

Check DNS resolution:

```bash
ping -c 4 google.com
```

Test internet connectivity:

```bash
curl https://example.com
```

---

# Step 12 – System Health Checks

CPU information:

```bash
lscpu
```

Memory usage:

```bash
free -h
```

Disk usage:

```bash
df -h
```

Mounted disks:

```bash
lsblk
```

Operating system details:

```bash
cat /etc/os-release
```

---

# Step 13 – Enable Firewall

Install UFW (if needed):

```bash
sudo apt install -y ufw
```

Allow SSH (only if you plan to use it):

```bash
sudo ufw allow OpenSSH
```

Enable the firewall:

```bash
sudo ufw enable
```

Check status:

```bash
sudo ufw status verbose
```

---

# Step 14 – Recommended Folder Structure

```text
~/Lab
├── Downloads
├── Projects
├── Scripts
├── Wazuh
├── Splunk
├── Elastic
├── Docker
└── Notes
```

Create it with:

```bash
mkdir -p ~/Lab/{Downloads,Projects,Scripts,Wazuh,Splunk,Elastic,Docker,Notes}
```

---

# Step 15 – Snapshot

Before installing security tools:

1. Power off the VM.
2. In VirtualBox, select the VM.
3. Open **Snapshots**.
4. Create a snapshot named:

```
Fresh-Ubuntu-24.04
```

This allows you to quickly restore the VM if something goes wrong.


---

# Author

**Bappy Sharma**
IT Audit & Cybersecurity Enthusiast
