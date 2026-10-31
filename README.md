<div align="center">

# 🔐 Cybersecurity Lab Environment Setup

**Building an isolated virtual lab for penetration testing and ethical hacking practice**
</div>


<p align="center">
  <img src="https://img.shields.io/badge/Cybersecurity-Ethical%20Hacking-C00000?style=flat-square" alt="Cybersecurity" />
  <img src="https://img.shields.io/badge/VirtualBox-7.2-0070C0?style=flat-square&logo=virtualbox&logoColor=white" alt="VirtualBox" />
  <img src="https://img.shields.io/badge/Kali%20Linux-2026.3-E87500?style=flat-square&logo=kalilinux&logoColor=white" alt="Kali Linux" />
  <img src="https://img.shields.io/badge/Network-10.0.0.0%2F24-238F89?style=flat-square" alt="Lab Network" />
  <img src="https://img.shields.io/badge/Platform-Virtual%20Machines-404040?style=flat-square" alt="Virtual Machines" />
  <img src="https://img.shields.io/badge/Documentation-GitHub-181717?style=flat-square&logo=github&logoColor=white" alt="GitHub Documentation" />
</p>


---

## 📌 Project Overview

This project focuses on setting up a **virtual cybersecurity and penetration-testing laboratory** using VirtualBox, Kali Linux and some other Operating Systems acting as targets.

The purpose of the lab is to create a controlled environment where cybersecurity tools, network scanning, reconnaissance, vulnerability assessment, and other security-testing activities can be performed safely and repeatedly.


---

## 📑 Table of Contents

- [📌 Project Overview](#-project-overview)
- [🎯 Objectives](#-objectives)
- [🛡 Purpose of the Lab](#-purpose-of-the-lab)
- [🏗 Lab Architecture](#-lab-architecture)
- [⚙ Lab Configuration](#-lab-configuration)
- [🪜 Lab Setup Procedure](#-lab-setup-procedure)
- [🧰 Lab Work: Wireshark](#-lab-work-wireshark)
- [📂 In Case of Other VMs or Target Machines](#-in-case-of-other-vms-or-target-machines)
- [🔎 Lab Verification](#-lab-verification)
- [🐞 Problems Encountered & Solutions](#-problems-encountered--solutions)
- [💡 What I Learned](#-what-i-learned)
- [🔐 Security & Ethical Use](#-security--ethical-use)
- [🔗 Tools & Resources](#-tools--resources)
- [👤 Author](#-author)


---

## 🎯 Objectives

The main objectives of this project are to:

- Install and configure VirtualBox.
- Install/import Kali Linux and other Operating Systems as virtual machines.
- Create a private **NAT Network** for the cybersecurity lab.
- Configure network connectivity for these Operating Systems.
- Assign a consistent IP address to each Operating System.
- Verify network connectivity.
- Take a clean VM snapshot for recovery.
- Document the complete setup process.

---

# 🛡 Purpose of the Lab

The lab provides an isolated and controlled environment for cybersecurity learning and authorized security testing.

It can be used for activities such as:

- Network reconnaissance
- Port scanning
- Vulnerability assessment
- Packet analysis
- Web security testing
- Exploitation practice
- Security-tool experimentation

⚠️ **Important:** This laboratory must only be used for systems that you own or have explicit permission to test. Do not use the lab or its tools to attack unauthorized systems.

---


# 🏗 Lab Architecture

The laboratory uses Oracle VirtualBox to run Kali Linux as the
security-testing machine alongside Windows and Android target VMs.
All machines are configured to use the same NAT Network for
internal connectivity and, where configured, outbound access.

![VirtualBox Lab Architecture](Vbox-Main.png)

### 🔑 Virtual Machine and IP Mapping

| Virtual Machine | Role | IP Address |
|---|---|---|
| Kali Linux | Security Testing | `10.0.0.2` |
| Windows 10 | Client Target | `10.0.0.3` |
| Windows 11 | Client Target | `10.0.0.4` |
| Windows 7 | Legacy Target | `10.0.0.5` |
| Android-x86 | Mobile Target | `10.0.0.6` |
| NAT Network Gateway | Default Gateway | `10.0.0.1` |

> **Note:** These are the intended addresses for the lab.
> Verify actual assignments and gateway settings against the
> VirtualBox configuration and guest operating systems.

---

# ⚙ Lab Configuration

| 🧩 Component       | ⚙️ Configuration   |
| ------------------ | ------------------  |
| 🖥️ Host OS         | Windows 11         |
| 🧠 Host RAM        | 8 GB               |
| ⚡ Processor       | Intel Core i7      |
| 🧰 Hypervisor      | VirtualBox 7.2  |
| 🐉 Security OS     | Kali Linux 2026.3  |
| 🧠 Kali RAM        | 1500 MB            |
| 🌐 Virtual Network | NAT Network        |
| 📡 Network Address | 10.0.0.0/24        |
| 🐧 Kali IP Address | 10.0.0.2/24        |
| 🚪 Default Gateway | 10.0.0.1           |
| 🌍 DNS Server      | 8.8.8.8            |
| 🔮 Remaining VM Range        | 10.0.0.3–10.0.0.99 |

---

# 🪜 Lab Setup Procedure


## Step 1. Install VirtualBox

VirtualBox was installed as the hypervisor. Remember to enable virtualization in your system's bios to make sure that no errors related to virtualization may occur.

---

## Step 2. Create the NAT Network

A dedicated NAT Network was created in VirtualBox.
```text
Configuration:
Network Name: NatNetwork
IPv4 Prefix:  10.0.0.0/24
DHCP:         Enabled
IPv6:         Disabled
```

![](Vbox-NetworkSettings.png)

A **NAT Network** was selected because multiple virtual machines connected to the same NAT Network can communicate with one another while also having outbound network connectivity.

This will allow future attacker and target VMs to communicate within the lab.


---

## Step 3. Import Kali Linux

The Kali Linux virtual machine was downloaded from the official Kali Linux website and imported into VirtualBox.

The VM network adapter was configured as follows:

![](1-KaliVM/Vbox-Kali-NetworkSettings.png)


The VM was allocated:

```text
RAM: 1500 MB
```
![](1-KaliVM/KaliSpecs.png)

A shared folder was also configured for transferring required files between the host operating system and the Kali VM.

![](1-KaliVM/Kali-SharedFolders.png)


---

## Step 4. Configure the Kali Linux Network

The Kali Linux network configuration was checked and configured with a consistent IPv4 address.

Example configuration:

```text
IP Address: 10.0.0.2
Subnet Mask: 255.255.255.0
Gateway: 10.0.0.1
DNS: 8.8.8.8
```
![](1-KaliVM/Kali-NetworkSettingsInternal.png)

A consistent IP address makes it easier to document the lab and reference the Kali machine in future exercises.


---

## Step 5. Create a Clean VM Snapshot

After completing the initial configuration, a VirtualBox snapshot was created.

Example snapshot name:

```text
Clean Kali - Network Setup
```
![](1-KaliVM/Kali-Snapshot.png)

The snapshot represents the clean baseline of the laboratory.

If a future exercise changes or damages the VM configuration, the machine can be restored to this baseline.


---

## 📂 In Case of Other VMs or Target Machines

> **Note:** Follow the equivalent VM setup, resource allocation,
> network configuration, and verification procedures used for Kali
> Linux. The screenshots and configuration evidence for each target
> are available in the corresponding directory. Some steps may vary
> depending on the operating system.

- 📁 [Windows 10 VM](2-Win10VM/) — Environment settings and security configuration.
- 📁 [Windows 11 VM](3-Win11VM/) — VirtualBox resources and installation evidence.
- 📁 [Windows 7 VM](4-Win7VM/) — Legacy VM deployment and resource settings.
- 📁 [Android VM](5-AndroidVM/) — Installation, architecture, and interface verification.
- 📁 [Connectivity Tests](6-Connectivity/) — Cross-VM ping tests and connectivity evidence.


---



## 🔎 Lab Verification

Run the following commands from Kali Linux to verify addressing
and connectivity. Actual results and screenshots are documented
in the `6-Connectivity/` directory.

| Test | Command | Expected Outcome |
|---|---|---|
| Check network interfaces | `ip a` | Intended IP address is assigned |
| Test gateway | `ping -c 4 10.0.0.1` | Replies if the gateway responds to ICMP |
| Test Windows 10 | `ping -c 4 10.0.0.3` | Replies if reachable and ICMP is allowed |
| Test Windows 11 | `ping -c 4 10.0.0.4` | Replies if reachable and ICMP is allowed |
| Test Windows 7 | `ping -c 4 10.0.0.5` | Replies if reachable and ICMP is allowed |
| Test Android | `ping -c 4 10.0.0.6` | Replies if reachable and ICMP is allowed |

![Kali to Windows 10 Connectivity Test](6-Connectivity/Kali-To-Win10.png)

*Figure: Example cross-VM connectivity test.*


---

# 🧰 Lab Work: Wireshark

I used **Wireshark** to capture live network traffic and analyze packet captures (PCAPs) for security issues. It was an extra module in this project. 

### Lab 1: Live Packet Capture
- **Activity:** Cleared laptop DNS cache (`ipconfig /flushdns`), started a live Wireshark capture on Wi-Fi, and went to `networkwalks.com`.
- **Findings:** Filtered with `dns.qry.name == "networkwalks.com"` to verify my laptop IP, DNS server IP, and the website's IP. Used `tls.handshake.type == 1` to check the TLS Client Hello and Server Name.

### Lab 2: Offline PCAP Analysis
- **Activity:** Opened `Wireshark_Lab2_Microsoft_DNS_v2.pcap` in Wireshark to practice offline analysis.
- **Findings:** Filtered with `dns.qry.name == "microsoft.com"` to find the target web IPs. Used the packet details and bytes panes to confirm the traffic uses secure port `443` and runs on `TLSv1.3`.

### Lab 3: SOC Analyst Port Scan Investigation
- **Activity:** Used the online Networkwalks lab environment to act as a SOC Analyst and investigate an unusual traffic alert sent to a web server (`192.168.10.20`).
- **Findings:** 
  - Used filter `tcp.flags.syn == 1` and found one IP address (`192.168.10.66`) blasting connection packets to many different ports in a fraction of a second. This confirmed a **Port Scan**.
  - Out of `309` total packets, `73` were SYN packets. The attacker scanned `40` unique ports from source port `52311`.
  - Filtered with `ip.addr == 192.168.10.66` to see server replies. Found that ports `22`, `80`, and `443` are **open** (`[SYN, ACK]`), while the other `37` ports are **closed** (`[RST, ACK]`).
  - #### 🏆 Lab Completion Proof
![Wireshark SOC Lab-3](PM4-Wireshark/PM4.d-Wireshark-SOC-LAB.png)

  **You can check out the official lab here: [Networkwalks Online SOC Lab-3](https://networkwalks.com/wireshark-lab3/).**

---

### 🔍 Quick Reference Filters Used

| Filter | Purpose |
| :--- | :--- |
| `ip.addr == 192.168.10.66` | Shows all traffic to or from the attacker IP. |
| `tcp.flags.syn == 1` | Isolates packets starting a TCP connection (SYN). |
| `dns.qry.name == "microsoft.com"` | Shows only DNS questions for this website. |
| `tls.handshake.type == 2` | Filters for Server Hello packets to check active TLS versions. |
| `Analyze > Follow > TCP Stream` | Rebuilds the whole conversation into clear text. |

---


# 🐞 Problems Encountered & Solutions

Documenting problems is an important part of the project.

## Problem 1. Internet Connectivity After Static IP Configuration

After manually configuring the IPv4 settings, Internet connectivity may fail depending on the Kali/NetworkManager configuration.

One workaround used during this lab was:

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
```

The network connection was then restarted/rebooted and connectivity was tested again.

> **Important:** Network interface and connection names may differ between systems. Students should first identify their actual connection name before running an `nmcli` command.

---

## Problem 2. Target Windows VMs Dropping Ping Requests (ICMP Blocked by Default)

During connectivity verification, the Kali Linux machine could not receive ping responses from the Windows target virtual machines (`10.0.0.3`, `10.0.0.4`, `10.0.0.5`), resulting in `100% packet loss`. 

### Cause
By default, the built-in Windows Defender Firewall blocks all inbound Internet Control Message Protocol (ICMP) Echo Requests. This prevents the target machines from responding to scanning or reconnaissance attempts from the attacker platform, even though they are active on the same `NatNetwork`.

### Solution
The issue was resolved by enabling the predefined inbound firewall rule on each Windows guest OS to explicitly allow ICMPv4 traffic:

1. Open the **Run** dialog box (`Win + R`), type `wf.msc`, and press **Enter** to open *Windows Defender Firewall with Advanced Security*.
2. Click on **Inbound Rules** in the left-hand pane.
3. Scroll down to locate the predefined rule: **File and Printer Sharing (Echo Request - ICMPv4-In)**.
4. Right-click the rule and select **Enable Rule** for the appropriate network profile (Private/Public).

Once enabled, cross-VM communications succeeded immediately, yielding successful ICMP replies on the Kali Linux terminal.

---

# 💡 What I Learned

Through this project, I learned how to create and configure a virtual environment for cybersecurity practice.

The most important concepts I learned include:

### 1. NAT vs NAT Network

A standard NAT configuration and a NAT Network serve different purposes.

A NAT Network allows multiple VMs connected to the same virtual network to communicate with one another while providing network address translation for external connectivity.

This makes it useful for building a multi-machine cybersecurity laboratory.

### 2. Virtual Machine Networking

I learned how VirtualBox virtual network adapters connect virtual machines to different types of networks and how network configuration affects communication between machines.

### 3. Static IP Configuration

I learned how to configure and verify IPv4 addressing, subnet masks, gateways, and DNS settings in Kali Linux.

### 4. VM Snapshots

I learned that a clean snapshot should be created **before performing risky or experimental activities**.

This provides a known-good recovery point for future cybersecurity exercises.

### 5. Documentation

I learned that documenting commands, configuration, screenshots, problems, and solutions is an important part of a professional cybersecurity project.

### 6. Packet Analysis with Wireshark
- I learned how to look inside individual network packets to find IP addresses, ports, and protocols instead of just testing basic connections.
- I learned how firewalls and servers reply differently to connection attempts when a port is open (`SYN, ACK`) versus when a port is closed (`RST, ACK`).

---

# 🔐 Security & Ethical Use

This laboratory is intended strictly for education purposes only.

---

# 🔗 Tools & Resources

- **VirtualBox:** https://virtualbox.org
- **Kali Linux:** https://kali.org
- **Wireshark official installers:** https://www.wireshark.org/download.html
- **Online SOC Lab environment:** https://networkwalks.com/wireshark


---

# 👤 Author

**Abdullah Tariq**\
Cybersecurity Professional B084

LinkedIn: [Abdullah Tariq](https://www.linkedin.com/in/abdullah-tariq-202301340485gb/)

---

## 📌 Project Information

**Program Name:** Cybersecurity at Networkwalks | **Week:** 01 | **Project:** Cybersecurity & Pentesting Lab Setup | **Repository:** GitHub
