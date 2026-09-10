# NETWORKWALKS-B083-WK1-CYBERSECURITY-KALI-LINUX-LAB-SETUP

# Cybersecurity Lab Environment Setup

Building an isolated virtual lab for penetration testing and ethical hacking practice.

![Cybersecurity](https://img.shields.io/badge/Skill-Cybersecurity-red)
![VirtualBox](https://img.shields.io/badge/Hypervisor-VirtualBox-blue)
![Kali Linux](https://img.shields.io/badge/OS-Kali%20Linux-orange)
![Networking](https://img.shields.io/badge/Network-NAT%20Network-teal)
![Networkwalks](https://img.shields.io/badge/Networkwalks-Internship-red)

---

## Project Overview

This project documents the setup of a virtual cybersecurity and penetration-testing laboratory using VirtualBox and Kali Linux. It was completed as part of the Cybersecurity & Ethical Hacking Internship at Networkwalks Technologies.

The purpose of this lab is to establish a controlled, isolated environment in which network scanning, reconnaissance, vulnerability assessment, and other security-testing activities can be carried out safely and repeatably. The lab is built on a private virtual network so that additional target machines can be added in future exercises.

---

## Objectives

- Install and configure VirtualBox as the hypervisor.
- Download and import Kali Linux as a virtual machine.
- Create a private NAT Network for the lab environment.
- Configure network connectivity for the Kali Linux VM.
- Assign a consistent, static IP address to the Kali VM.
- Enable shared folders and clipboard/file transfer between host and VM.
- Verify network connectivity and DNS resolution.
- Take a clean VM snapshot for recovery purposes.
- Document the complete setup process, including issues encountered and their resolutions.

---

## Machine Configuration

| Component           | Configuration            |
|---------------------|---------------------------|
| Host OS              | Windows 10                |
| Hypervisor            | VirtualBox (latest version) |
| Guest OS              | Kali Linux                |
| Virtual Network Type  | NAT Network                |
| Network Subnet        | 10.0.0.0/24                |
| Kali Linux IP Address | 10.0.0.2/24                |
| Default Gateway       | 10.0.0.1                   |
| DNS Server             | 8.8.8.8                    |
| Shared Folder          | /downloads (host to guest) |
| Clipboard & Drag/Drop  | Enabled                     |

---

## Lab Setup Procedure

### Phase 1

#### Step 1: Install 7-Zip

7-Zip is used to extract the Kali Linux virtual machine package, which is distributed as a compressed archive.

*If 7-Zip is already installed on your system, this step can be skipped.*

**Download link:** https://7-zip.org/download.html

![7-Zip image](<7-Zip .png>)

---

#### Step 2: Install VirtualBox

VirtualBox was installed as the hypervisor used to run and manage the virtual machines in this lab.

**Download link:** https://virtualbox.org/wiki/Downloads

![VirtualBox Download 1](./Virtual%20Box%20Download%201.png)

![VirtualBox Download 2](<Virtual Box Download 2.png>)

---

#### Step 3: Configure VirtualBox Network Settings

A dedicated NAT Network was created within VirtualBox to allow virtual machines to communicate with one another while retaining outbound internet access.

**Navigation:** File → Tools → Network

![Setup VirtualBox 1](<Setup Virtual Box 1.png>)

**NAT Network configuration:**

| Setting        | Value          |
|----------------|-----------------|
| Network Name    | NatNetwork      |
| IPv4 Prefix      | 10.0.0.0/24      |
| DHCP             | Enabled          |
| IPv6             | Disabled         |

![Setup VirtualBox 2](<setup Virtual Box 2.png>)
A NAT Network was selected over a standard NAT configuration because it allows multiple virtual machines attached to the same network to communicate with each other, in addition to providing outbound connectivity. This is essential for building a multi-machine lab in future projects.

---

#### Step 4: Download and Import Kali Linux Virtual Machine

The Kali Linux virtual machine was downloaded from the official Kali Linux website and imported into VirtualBox.

**Download link:** https://kali.org/get-kali

![Kali Linux Download 1](<Kali Linux Download 1.png>)

![Kali Linux Download 2](<Kali Linux Download 2.png>)

**VM import:**

![Import Kali Linux In VirtualBox 1](<Import kali Linux In Virtual Box 1.png>)

**Network adapter configuration:**

```text
Adapter 1
Attached to: NAT Network
Network: NatNetwork
```

![Import Kali Linux In VirtualBox 2](<Import kali Linux In Virtual Box 2.png>)

---

#### Step 5: Configure the Kali Linux Network

The Kali Linux network interface was manually configured with a static IP address to ensure consistency across the lab environment.

```text
IP Address: 10.0.0.2
Subnet Mask: 255.255.255.0 (/24)
Gateway: 10.0.0.1
DNS: 8.8.8.8
```

![Kali Linux Config](<Kali Linux Config.png>)

---

#### Step 6: Take a Clean VM Snapshot

Once the initial configuration was complete, a VirtualBox snapshot was created to preserve the clean baseline of the lab. This snapshot allows the environment to be restored if a future exercise alters or damages the VM configuration.

![Snap Shot](<Snap Shot.png>)

---

## Lab Verification

| Test                         | Command                       | Expected Result             |
|------------------------------|--------------------------------|-------------------------------|
| Check IP address               | `ip a`                          | Correct Kali IP displayed     |
| Test gateway                    | `ping 10.0.0.1`                 | Successful replies             |
| Test internet connectivity      | `ping 8.8.8.8`                  | Successful replies             |
| Test DNS resolution              | `nslookup networkwalks.com`     | Domain resolves                |
| Restore snapshot                 | Restore snapshot and run `ip a` | Baseline configuration restored |

---

## Problems Encountered & Solutions

### Problem 1: Internet Connectivity After Static IP Configuration

After manually configuring the IPv4 settings, internet connectivity failed due to a NetworkManager-related issue common in recent Kali Linux versions.

**Resolution:**

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
sudo nmcli connection down "Wired connection 1"
sudo nmcli connection up "Wired connection 1"
```

*Note: Connection names may differ between systems. Confirm the actual connection name before running these commands.*

---

## What I Learned

- **NAT vs. NAT Network:** A NAT Network allows multiple VMs on the same virtual network to communicate with one another while retaining outbound connectivity, making it well suited to a multi-machine lab.
- **Virtual Machine Networking:** Gained an understanding of how VirtualBox network adapters connect VMs to different network types and how this affects inter-VM communication.
- **Static IP Configuration:** Learned to configure and verify IPv4 addressing, subnet masks, gateways, and DNS settings within Kali Linux.
- **VM Snapshots:** A clean snapshot should always be taken before performing experimental or high-risk activities, providing a reliable recovery point.
- **Documentation:** Recording commands, configurations, screenshots, and troubleshooting steps is an essential part of professional cybersecurity work.

---

## Security & Ethical Use

This lab environment is intended strictly for educational purposes. All testing activities were carried out within the isolated virtual environment described above. This laboratory must only be used on systems that are owned by the user or for which explicit written permission has been granted.

---

## Tools & Resources

- **7-Zip:** https://7-zip.org/download.html
- **VirtualBox:** https://virtualbox.org/wiki/Downloads
- **Kali Linux:** https://kali.org/get-kali

---

## Author

**Syed Muhammad Ali Raza**
Cybersecurity & Ethical Hacking Intern, Networkwalks Technologies

---

## Project Information

**Program:** Cybersecurity & Ethical Hacking Internship — Networkwalks Technologies
**Week:** 01
**Project:** Cybersecurity & kali Linux Lab Setup
