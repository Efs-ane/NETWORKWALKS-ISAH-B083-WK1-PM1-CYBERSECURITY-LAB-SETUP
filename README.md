<div align="center">
    
# Cybersecurity Lab Environnment Setup
    
**Isolated virtual lab built with virtualBox and Kali linux for cybersecurity testing and penetration testing practice**
</div>


## Project Overview: 

This project involves building an isolated cybersecurity testing environment with VirtualBox and kali linux. The lab is designed 
to support practical security exercises, including reconnaisance, network scanning, vulnerability analysis, and penetration testing, in a safe and repeatable manner. A private virtual network is used to facilitate the future integration of additional virtual machines, which can serve as targets for authorised security assessments.

---

## OBJECTIVES:

- Install and configure VirtualBox
- Install\import Kali Linux as a virtual machine.
- Create a private **NAT Network** for the cybersecurity lab
- Configure network connectivity for kali linux
- Assign an IP address to the kali VM 
- Verify network connectivity and DNS resolution
- Take a clean VM snapshot for recovery
- Document the complete setup process 
- Prepare the environment for future cybersecurity projects

---

## purpose of the Lab

The lap provides a controlled environment for cybersecurity learning and authorized security testing

Activities:

- Network reconnaissance
- Port Scanning
- Vulnerability assessment
- Packet analysis
- Web Security testing
- Exploitation practice
- Security-tool experimentation
---
## Lab Architecture

## lab Configuration
|   component          |    configuration     |
| -------------------- | ---------------------|
|  Host OS             |   Windows 11         |
|  Host RAM            |   20 GB              |
|  Processor           |   Intel Core i3      |    
|  Hypervisor          |   VirtualBox 7.2     |
|  Security OS         |   Kali Linux 2026.2  |
|  Kali RAM            |   2048 MB            |
|  Virtual Network     |   NAT Network        |
|  Network Address     |   10.0.0.0/24        |
|  Kali IP Address     |   10.0.0.2/24        |
|  Default Gateway     |   10.0.0.1           |
|  DNS Server          |   10.0.0.1           |
|  Future VM Range     |   10.0.0.3-10.0.0.99 |

---
#Lab Setup Procedure

## Step 1. Install 7-Zip
7-zip will be used to extract the kali linux virtual machine package, which may be distributed as a '.7z' archive.

**Tool:** 7-zip

---

## Step 2. Install virtualBox

VirtualBox was installed as the hypervisor.

---

## Step 3. Create the NAT Network

A dedicated NAT Network was created in VirtualBox

Configuration:
Network Name: NatNetwork
IPv4 Prefix : 10.0.0.0/24
DHCP        : Enabled
IPv6        : Disabled



A **Nat Network** was selected so that multiple virtual machines can connect to the same NAT Network and communicate with one another while also having outbound network connectivity.

This will allow future attacker and target VMs to communicate within the lab.

---
## Step 4. Import Kali Linux

The kali Linux virtual machine was downloaded from the official kali linux website and imported into VirtualBox

Below is the VM network adapter configuration:
'''text
Adapter 1
Attached to: NAT Network
Network    : NatNetwork
Adapter Type: Intel PRO/1000 MT Desktop
'''
VM was allocated:
'''text
RAM: 2048 MB
'''

A shared folder was also configured for transferring required files between the host operating system and the kali VM.




---

## Step 5. Kali Linux Network Configuration

The Kali Linux network configuration was checked and configured with a consistent IPv4 address.

Example configuration:

'''text
IP Address:   10.0.0.2
Subnet Mask:  255.255.255.0
Gateway:      10.0.0.1
DNS:          10.0.0.1
'''
A consistent IP address makes it easier to document the lab and reference the kali machine in future exercise



---

## Step 6. Create a Clean VM Snapshot

After completing the initial configuration, a VirtualBox snapshot was created.

Example snapshot name:

'''text
Clean Kali - Network Setup

The snapshot represents the clean baseline of the laboratory.
If a future exercise changes or damages the VM configuration, the machine can be restored to this baseline.

---

# Lab Verification
|    Test                                |        Command                     |    Expected result               |
| -------------------------------------- | ---------------------------------- | -------------------------------- |
|    check IP address                    |    'ip a'                          | correct kali IP displayed        |
|    Test gateway                        |    'ping 10.0.0.1'                 | Successful replies               |
|    Test Internet Connectivity          |    'ping 10.0.0.1||'               | Successful replies               |
|    Test DNS resolution                 |    'nslookup networkwalks.com'     | Domain resolves                  |
|    Verify Nmap                         |    'nmap --version'                | Nmap version displayed           |
|    Verify snapshot                     |     Restore snapshot and run 'ip a'| Baseline configuration restored  |

### Example Results

'''text
IP Address:
10.0.0.2/24

Gateway:
10.0.0.1

DNS:
10.0.0.1

---

# Problems Encountered & solutions

## Problem 1. Kali had working internet in plain NAT mode but not in NAT Network mode. The guide we were following used a static configuration: IP 10.0.0.2/24, gateway 10.0.0.1, DNS 8.8.8.8

what i assumed was wrong(in order)
1. Mode mismatch. Plain NAT work automatically, while NAT Network must be created and configured. This was correct, but only part of the story
2. Address range mismatch. VirtualBox defaults to 10.0.2.0/24, while the guide's addresses sit in 10.0.0.0/24. The fix was to create a NAT Network with the prefix 10.0.0.0/24. This was also correct
3. No IP on eth0. The ip a output showed the link was up but had no inet line, so the static settings had never been applied.
4. Failed ping to the gateway. I first assumed this meant a wrong prefix. VirtualBox's gateway doesn't answer pings, so this was normal. The successful ping to 8.8.8.8 showed routing was fine
5. DNS failure. ping google.com failed with temporary failure in name resolution", SO there was no working nameserver. I assumed NetworkManager settings to make it stick
6. "IP configuration could not be reserved" error. I first assumed the profile was still on DHCP. That didn't fix it, i then recreated a clean profile(kali-static) bound to eth0, and the error persisted
7. The actual cause(most likely)
10.0.0.2 is reserved by VirtualBox inside a NETNetwork(it acts as the host loopback address) NetworkManager's duplicate-address check saw it as taken and refused to activate the connection. I should have detect this as soon as i saw the guide address
## what fixed it?
- Created a NAT Network with prefix 10.0.0.0/24
- Attached the VM's adapter to it
- Created a static NetworkManager profile bound to eth0(gateway 10.0.0.1, DNS 8.8.8.8)
- Cleared leftover addresses with ip addr flush dev eth0
- Disabled the duplicate-address check(ipv4.dad-timeout 0)
- Fallback: using a different address such as 10.0.0.10
## Lessons
- A failed ping to the VirtualBox gateway doesn't necessarily mean the network is broken
- Test in layers: IP, then gateway/routing(ping 8.8.8.8), then DNS(ping google.com).
- If the guide hardcores 10.0.0.2, check wether it clashes with VirtualBox's reserved addresses before debugging further
- Wherever the guide mentions 10.0.0.2 later, use whichever address you end up with
- 

---

# What I Learned
Through this project, I learned how to create and configure a virtual environment for cybersecurity practice

The most important concepts I learned include:

### 1. NAT vs NAT Network
A standard NAT configuration and a NAT Network serve different purpose.
A NAT Network allows multiple VMs connected to the same virtual network to communicate with one another while providing network address translation for external connectivity.
This makes it useful for building a multi-machine cybersecurity laboratory.

### 2. Virtual Machine Networking
I learned how VirtualBox virtual network adapters connect virtual machines to different types of networks and how network configuration affects communication between machines

### 3. Static IP Configuration
I learned how to configure and verify ipv4 addressing, subnet masks, gateways, and DNS settings in kali linux
### 4. VM Snapshots
I learned that a clean snapshot should be created **before performing risky or experimental activities**
this provides a known-good recovery point for future cybersecurity exercises

### 5. Documentation
I learned that documenting commands, configuration, screenshots, problems, and solutions is an important part of a professional cybersecurity project.
---

# Security & Ethical Use
This laboratory is intended strictly for educational purposes only.
---
# Tools & Resources
- **7-zip:**
- **VirtualBox:**
- **Kali Linux:**

---

# Author
**Isah Suleiman**\

LinkedIn:

---

## Project Information
**Program Name:** Cybersecurity at Networkwalks | **week:** 01 | **Project:** Cybersecurity & Pentesting Lab Setup | **Repository:** GitHub


