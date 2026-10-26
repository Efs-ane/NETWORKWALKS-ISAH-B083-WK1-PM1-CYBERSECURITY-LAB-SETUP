<div align="center">
    
# Cybersecurity Lab Environnment Setup
    
**Isolated virtual lab built with virtualBox and Kali linux for cybersecurity testing and penetration testing practice**
</div>
---

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



