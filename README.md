<div align="center">

# 🔐 Cybersecurity Lab Environment Setup

### VirtualBox + Kali Linux | Ethical Hacking & Penetration Testing

Building a virtual cybersecurity laboratory for network configuration, security testing, and hands-on ethical hacking practice.

![Cybersecurity](https://img.shields.io/badge/Domain-Cybersecurity-C00000?style=for-the-badge)
![Kali Linux](https://img.shields.io/badge/OS-Kali%20Linux%202026.1-557C94?style=for-the-badge&logo=kalilinux&logoColor=white)
![VirtualBox](https://img.shields.io/badge/Hypervisor-VirtualBox%207.2-0070C0?style=for-the-badge&logo=virtualbox&logoColor=white)
![Networking](https://img.shields.io/badge/Network-10.0.0.0%2F24-238F89?style=for-the-badge)
![Ethical Hacking](https://img.shields.io/badge/Purpose-Ethical%20Hacking-E87500?style=for-the-badge)

</div>

---

## 📌 Project Overview

This project documents the setup and configuration of a virtual cybersecurity laboratory using Oracle VirtualBox and Kali Linux.

The laboratory provides an environment for learning Linux administration, virtual networking, network reconnaissance, vulnerability assessment, and penetration-testing fundamentals.

A dedicated VirtualBox NAT Network was configured to provide a common virtual network for Kali Linux and potential future target virtual machines.

The environment is designed to support repeatable cybersecurity exercises while keeping testing activities within systems that are owned by the user or explicitly authorized for testing.

This project also documents the configuration process, system resources, network settings, and initial verification of the Kali Linux network interface.

## 🎯 Project Objectives

The main objectives of this project are:

- Install and configure Oracle VirtualBox.
- Set up Kali Linux as a virtual machine.
- Create a dedicated NAT Network.
- Configure static IPv4 addressing in Kali Linux.
- Configure the intended gateway and DNS server.
- Verify the Kali Linux network interface.
- Understand virtual networking and IP addressing.
- Prepare the environment for future penetration-testing exercises.
- Document the setup using screenshots and configuration details.
- Establish a foundation for future cybersecurity laboratory projects.

---

## 🛡️ Purpose of the Lab

The laboratory is intended for cybersecurity education and authorized security testing.

Potential applications include:

- Network reconnaissance.
- Port scanning.
- Vulnerability assessment.
- Packet analysis.
- Web application security testing.
- Linux security administration.
- Penetration-testing fundamentals.
- Security-tool experimentation.
- Testing intentionally vulnerable virtual machines.

**Important:** These are intended uses of the environment. The installation of a tool or configuration of the lab does not mean that every activity has already been performed.

All testing must be limited to systems that you own or have explicit permission to assess.

---

## 🏗️ Lab Architecture

The current environment consists of a Windows host running VirtualBox and a Kali Linux virtual machine connected to a NAT Network.

```text
                    HOST COMPUTER
                     Windows OS
                          |
                          |
                  Oracle VirtualBox
                          |
                          |
                   NAT NETWORK
                    NatNetwork
                    10.0.0.0/24
                          |
                          |
                   KALI LINUX VM
                    Kali Linux 2026.1
                          |
                  Ethernet: eth0
                          |
                     10.0.0.2/24
                          |
                Cybersecurity Exercises
                          |
                Future Authorized Targets
```

### Network Design

The network uses the `10.0.0.0/24` IPv4 prefix.

The intended configuration includes:

- Kali Linux static IPv4 address: `10.0.0.2`.
- Default gateway: `10.0.0.1`.
- DNS server: `8.8.8.8`.
- VirtualBox network name: `NatNetwork`.

Additional virtual machines can be connected to the same NAT Network for authorized laboratory exercises.

**Network isolation note:** A NAT Network supports communication between connected virtual machines and can provide outbound connectivity. It should not be treated as a completely isolated network.

---

## ⚙️ System Configuration

The following table documents the configuration visible in the provided screenshots.

| Component | Configuration |
|---|---|
| Host operating system | Windows |
| Hypervisor | Oracle VirtualBox |
| Virtual machine | Kali Linux |
| Kali Linux version | 2026.1 |
| VM memory | 2048 MB (2 GB) |
| Allocated processors | 2 CPUs |
| Virtual disk | Approximately 80 GB |
| Network adapter | Intel PRO/1000 MT Desktop |
| Network attachment | NAT Network |
| Virtual network name | `NatNetwork` |
| IPv4 network prefix | `10.0.0.0/24` |
| Kali network interface | `eth0` |
| Kali IPv4 address | `10.0.0.2` |
| Subnet mask | `255.255.255.0` |
| Broadcast address | `10.0.0.255` |
| Default gateway | `10.0.0.1` |
| DNS server | `8.8.8.8` |
| DHCP | Enabled on the VirtualBox NAT Network |
| IPv6 | Disabled for the NAT Network |

**Configuration note:** The static IPv4 address, gateway, and DNS settings are visible in the Kali network settings screenshot. The `ifconfig` screenshot confirms the IP address and active interface. Internet connectivity and DNS resolution have not been independently verified in the screenshots.

---

# 🪜 Lab Setup Procedure

## Step 1: Install 7-Zip

7-Zip can be used to extract compressed virtual-machine packages when necessary.

Official website: https://www.7-zip.org/download.html

## Step 2: Install Oracle VirtualBox

Oracle VirtualBox was used to create and manage the virtual machines.

The VirtualBox Manager screenshot shows the Kali Linux virtual machine and its configuration.

The environment also contains entries for Parrot OS and Windows 7. Their presence in the manager does not establish that they have been configured as targets for this project.

Official website: https://www.virtualbox.org/wiki/Downloads

## Step 3: Configure the VirtualBox NAT Network

A dedicated NAT Network named `NatNetwork` was configured.

The network settings shown in the screenshot are:

```text
Network Name: NatNetwork
IPv4 Prefix:  10.0.0.0/24
DHCP:         Enabled
IPv6:         Disabled
```

### Why use a NAT Network?

A NAT Network is useful for a multi-machine virtual laboratory because virtual machines connected to the same network can communicate with each other while using network address translation for outbound connectivity.

This configuration provides a foundation for future security exercises involving an attacker VM and authorized target VMs.

### DHCP consideration

DHCP is enabled on the VirtualBox NAT Network, while Kali Linux is configured with a manually assigned IPv4 address.

This arrangement can work, provided the static IP does not conflict with an address assigned through DHCP.

For a more reliable setup, ensure `10.0.0.2` is outside the DHCP allocation range or is appropriately reserved.

**Screenshot:** `screenshots/04-nat-network-settings.png`

## Step 4: Configure the Kali Linux Virtual Machine

The Kali Linux VM is configured with the following resources:

```text
Operating System: Kali Linux 2026.1
Memory:           2048 MB
Processors:       2
Virtual Disk:     Approximately 80 GB
```

The network adapter is configured as follows:

```text
Adapter 1
Attached to: NAT Network
Network:     NatNetwork
Adapter Type: Intel PRO/1000 MT Desktop
```

This connects the Kali virtual machine to the configured NAT Network.

**Screenshot:** `screenshots/02-virtualbox-manager.png`

## Step 5: Configure a Static IPv4 Address

The Kali Linux network settings show the connection name `Wired connection 1`.

The IPv4 configuration is:

```text
Method:       Manual
IP Address:   10.0.0.2
Netmask:      24
Gateway:      10.0.0.1
DNS Server:   8.8.8.8
```

The `/24` prefix corresponds to the subnet mask `255.255.255.0`.

A static IP address makes it easier to reference the Kali VM consistently during future laboratory exercises.

**Screenshot:** `screenshots/01-kali-ipv4-settings.png`

## Step 6: Verify the Kali Network Interface

The Kali Linux terminal screenshot shows the output of:

```bash
ifconfig
```

The output includes:

```text
Interface:  eth0
IPv4:       10.0.0.2
Netmask:    255.255.255.0
Broadcast:  10.0.0.255
State:      UP, RUNNING
```

This confirms that the `eth0` interface is active and has the intended IPv4 address.

The screenshot also shows the loopback interface, `lo`, with the address `127.0.0.1`.

**Screenshot:** `screenshots/05-kali-ifconfig.png`

## Step 7: Capture the Kali Linux Desktop

The Kali Linux desktop screenshot documents the graphical environment used for laboratory configuration.

This serves as visual evidence that the Kali Linux desktop is available.

**Screenshot:** `screenshots/03-kali-desktop.png`

---

# 🔎 Initial Verification

The following table distinguishes between configuration evidence already available and checks that have not been documented.

| Verification item | Evidence or command | Status |
|---|---|---|
| Kali Linux desktop | Desktop screenshot | Confirmed |
| VirtualBox VM configuration | VirtualBox Manager screenshot | Confirmed |
| NAT Network prefix | VirtualBox Network Manager screenshot | Confirmed |
| Static IPv4 address | Kali network settings and `ifconfig` | Confirmed |
| Subnet mask | `ifconfig` output | Confirmed |
| Network interface status | `ifconfig` output | Confirmed |
| Default gateway configuration | Kali IPv4 settings | Configured |
| DNS server configuration | Kali IPv4 settings | Configured |
| Gateway connectivity | `ping -c 4 10.0.0.1` | Not documented |
| Internet connectivity | `ping -c 4 8.8.8.8` | Not documented |
| DNS resolution | `getent hosts networkwalks.com` | Not documented |
| Shared-folder access | Mount or file-access test | Not documented |
| VM snapshot recovery | Restore test | Not documented |

### Useful verification commands

The following commands can be used during future testing.

Check IP addressing:

```bash
ip a
```

Check routing:

```bash
ip route
```

Test the configured gateway:

```bash
ping -c 4 10.0.0.1
```

Test outbound IP connectivity:

```bash
ping -c 4 8.8.8.8
```

Check DNS resolution:

```bash
getent hosts networkwalks.com
```

Check Nmap installation:

```bash
nmap --version
```

These commands are included as verification steps. Their successful execution and results have not been established by the screenshots provided.

---

# 🐞 Troubleshooting and Configuration Notes

## 1. Internet Connectivity After Static IP Configuration

Manually configuring an IP address can cause connectivity problems if the address, gateway, subnet, or DNS settings do not match the virtual network.

Recommended troubleshooting steps:

1. Verify the active network interface.
2. Check the assigned IPv4 address.
3. Inspect the routing table.
4. Confirm the gateway address.
5. Check the configured DNS server.
6. Test gateway connectivity separately from Internet connectivity.
7. Inspect the VirtualBox NAT Network configuration.

Useful commands:

```bash
ip a
ip route
cat /etc/resolv.conf
nmcli connection show
```

The actual NetworkManager connection name should be identified before modifying settings.

## 2. VirtualBox Hardware Virtualization

If a VM fails to start because hardware virtualization is unavailable, check the host computer's BIOS/UEFI configuration.

Depending on the processor, the relevant setting may be Intel VT-x or another hardware-virtualization option.

After enabling virtualization, save the firmware settings, restart the computer, and try starting the VM again.

This is a general troubleshooting procedure; the current screenshots do not establish that this error occurred during this particular setup.

## 3. DHCP and Static IP Address Conflicts

The NAT Network screenshot shows DHCP enabled.

Because Kali uses the static address `10.0.0.2`, ensure the DHCP allocation does not assign the same address to another VM.

An address conflict can result in intermittent connectivity or unexpected network behavior.

---

# 💡 What I Learned

### 1. Virtualization Fundamentals

Learned how Oracle VirtualBox can run a separate Linux operating system inside a host computer.

### 2. Virtual Network Configuration

Learned how a NAT Network can connect multiple virtual machines while providing outbound connectivity.

### 3. IPv4 Addressing

Practiced configuring a static IPv4 address, subnet mask, gateway, and DNS server in Kali Linux.

### 4. Linux Network Interfaces

Learned how to inspect interface information and confirm the assigned IPv4 address using `ifconfig`.

### 5. Network Planning

Understood why a consistent IP-addressing scheme is useful for documenting and maintaining a virtual cybersecurity laboratory.

### 6. Technical Documentation

Learned the importance of documenting configuration settings, commands, screenshots, and verification status in a reproducible format.

---

# 🔐 Security and Ethical Use

This laboratory is intended for educational purposes and authorized security testing.

- Only test systems you own or have explicit permission to assess.
- Use intentionally vulnerable virtual machines only in an appropriately controlled environment.
- Check network boundaries before performing scanning or exploitation exercises.
- Avoid exposing vulnerable target machines to untrusted networks.
- Keep sensitive credentials and private keys out of shared folders.
- Create recovery points before making potentially disruptive changes.
- Document security exercises and their outcomes accurately.

---

# 🔗 Tools and Resources

| Tool | Purpose | Official website |
|---|---|---|
| 7-Zip | Archive extraction | https://www.7-zip.org/download.html |
| Oracle VirtualBox | Virtualization | https://www.virtualbox.org/wiki/Downloads |
| Kali Linux | Security testing distribution | https://www.kali.org/get-kali/ |
| Nmap | Network discovery and security auditing | https://nmap.org/ |
| Wireshark | Network protocol analysis | https://www.wireshark.org/ |

---

# 📸 Project Screenshots

The screenshots used in this documentation should be stored in a `screenshots` directory in the GitHub repository.

Recommended directory structure:

```text
cybersecurity-lab-setup/
│
├── README.md
│
└── screenshots/
    ├── 01-kali-ipv4-settings.png
    ├── 02-virtualbox-manager.png
    ├── 03-kali-desktop.png
    ├── 04-nat-network-settings.png
    └── 05-kali-ifconfig.png
```

### Embedding screenshots in the README

GitHub can display images stored in the repository using relative paths.

For example:

```markdown
![Kali IPv4 Configuration](screenshots/01-kali-ipv4-settings.png)
```

Use the same naming convention for all screenshots so the README remains organized.

*The directory structure above is a recommended organization. The files must be uploaded to GitHub using these names, or the Markdown paths must be updated to match their actual filenames.*

---

# 👤 Author

**Prashant Dubey**

Cybersecurity | Ethical Hacking | Digital Forensics

Interested in cybersecurity, network security, digital forensics, and practical security experimentation.

GitHub: Add your GitHub profile URL here.

---

# 📌 Project Information

| Field | Details |
|---|---|
| Project name | Cybersecurity Lab Environment Setup |
| Program | Cybersecurity at NetworkWalks |
| Week | 01 |
| Focus | Virtualization and network configuration |
| Hypervisor | Oracle VirtualBox |
| Security distribution | Kali Linux 2026.1 |
| Virtual network | `NatNetwork` |
| Network prefix | `10.0.0.0/24` |
| Kali IPv4 address | `10.0.0.2/24` |
| Default gateway | `10.0.0.1` |

---

<div align="center">

**Building a foundation for hands-on cybersecurity learning.**

</div>
