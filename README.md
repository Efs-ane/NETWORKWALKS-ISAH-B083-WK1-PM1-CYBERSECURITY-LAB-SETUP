<div align="center">
    
# Cybersecurity Lab Environnment Setup
    
**Isolated virtual lab built with virtualBox and Kali linux for cybersecurity testing and penetration testing practice**
</div>


## Project Overview: 

This project involves building an isolated cybersecurity testing environment with VirtualBox and kali linux. The lab is designed 
to support practical security exercises, including reconnaisance, network scanning, vulnerability analysis, and penetration testing, in a safe and repeatable manner. A private virtual network is used to facilitate the future integration of additional virtual machines, which can serve as targets for authorised security assessments.

---

## OBJECTIVES;

- Install and configure VirtualBox
- Install\import Kali Linux as a virtual machine.
- Create a private NAT Network for the cybersecurity lab
- Configure network connectivity for kali linux
- Assign an IP address to the kali VM 
- Verify network connectivity and DNS resolution
- Take a clean VM snapshot for recovery
- Document the complete setup process 
- Prepare the environment for future cybersecurity projects

---
## purpose of the Lab
The lap provides an isolated and controlled environment for cybersecurity learning and authorized security testing

Activities:

- Network reconnaissance
- Port Scanning
- Vulnerability assessment
- Packet analysis
- Web Security testing
- Exploitation practice
- Security-tool experimentatione
---

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


