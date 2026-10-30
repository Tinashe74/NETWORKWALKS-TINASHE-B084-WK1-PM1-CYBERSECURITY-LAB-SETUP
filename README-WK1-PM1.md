# WK1-PM1 – Week 1: Lab Setup with VirtualBox and Kali Linux

**Student:** Tinashe Victore Banda  
**Module:** Project Module 1 (PM1)  
**Week:** 1  
**Virtualisation software:** Oracle VM VirtualBox  
**Operating system:** Kali Linux  

## Introduction

This README documents my completion of the initial cybersecurity lab setup using Oracle VM VirtualBox and Kali Linux. The lab provides a virtual environment for practising basic Linux administration, network configuration and authorised cybersecurity testing.

The work documented here includes the VirtualBox NAT Network configuration, updating the Kali Linux package lists, and testing connectivity from Kali Linux to the virtual network gateway and an external IP address.

## Lab Environment

| Component | Configuration |
|---|---|
| Virtualisation platform | Oracle VM VirtualBox |
| Guest operating system | Kali Linux |
| NAT Network name | `NatNetwork` |
| IPv4 network prefix | `10.0.0.0/24` |
| DHCP | Enabled |
| Gateway tested | `10.0.0.1` |
| External IP tested | `8.8.8.8` |

## 1. Configure the NAT Network in VirtualBox

I created a NAT Network in Oracle VM VirtualBox named `NatNetwork` and configured its IPv4 prefix as `10.0.0.0/24`. The DHCP server option is enabled in the VirtualBox network settings.

The Kali Linux virtual machine should be connected to this NAT Network through its network adapter settings.

![VirtualBox NAT Network settings showing NatNetwork, 10.0.0.0/24 and DHCP enabled](screenshots/virtualbox-nat-network.png)

**Figure 1:** VirtualBox NAT Network configuration.

## 2. Update Kali Linux

After starting Kali Linux, I opened the terminal and ran the package-list update command:

```bash
sudo apt update
```

The system requested the Kali user password before continuing. The command then retrieved package information from the Kali Linux rolling repositories.

The terminal output reported that **77.6 MB** of data was fetched and that **2,343 packages can be upgraded**. This confirms that the package list update completed and that package upgrades were available.

![Kali Linux terminal showing sudo apt update and package repository results](screenshots/kali-apt-update.png)

**Figure 2:** Updating Kali Linux package lists.

*Note:* `sudo apt update` refreshes the package information; it does not install all available upgrades. To upgrade installed packages, a separate upgrade command would be required.

## 3. Test Network Connectivity

I used the `ping` command to check whether Kali Linux could communicate with the gateway and an external IP address.

### 3.1 Test the virtual network gateway

Command:

```bash
ping -c 3 10.0.0.1
```

The command sent three ICMP packets to `10.0.0.1`. All three packets were received, resulting in **0% packet loss**. The reported average round-trip time was approximately **1.551 ms**.

This result demonstrates that the Kali Linux machine could reach the tested gateway address.

### 3.2 Test external IP connectivity

Command:

```bash
ping -c 3 8.8.8.8
```

The command sent three ICMP packets to `8.8.8.8`. All three packets were received, resulting in **0% packet loss**. The reported average round-trip time was approximately **87.201 ms**.

This result demonstrates successful connectivity to the external IP address at the time of testing.

![Kali Linux terminal showing successful ping tests to 10.0.0.1 and 8.8.8.8](screenshots/kali-connectivity-tests.png)

**Figure 3:** Successful gateway and external IP connectivity tests.

### Connectivity results

| Destination | Test purpose | Packets received | Packet loss | Average time |
|---|---|---:|---:|---:|
| `10.0.0.1` | Gateway connectivity | 3 of 3 | 0% | 1.551 ms |
| `8.8.8.8` | External IP connectivity | 3 of 3 | 0% | 87.201 ms |

## 4. Summary

The evidence in this repository shows that I configured a VirtualBox NAT Network using the `10.0.0.0/24` IPv4 prefix with DHCP enabled, refreshed Kali Linux package information, and tested connectivity to both `10.0.0.1` and `8.8.8.8`. Both ping tests completed successfully with no packet loss.

These results establish a working starting point for the lab. They do not, on their own, confirm every possible setup requirement. Any additional items specified in the lab handout—such as a static Kali IP address, shared clipboard, drag-and-drop, shared folder or virtual machine snapshot—should be verified separately before marking the entire lab as complete.

## Responsible Use

This virtual environment is intended for learning and authorised cybersecurity practice. Any scanning, vulnerability assessment or penetration testing should be limited to systems that I own or have explicit permission to test.
