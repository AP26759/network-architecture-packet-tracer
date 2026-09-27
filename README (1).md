# Network Architecture & Security — Cisco Packet Tracer

## Overview

A secure enterprise network designed and implemented in Cisco Packet Tracer for a fictional organisation, Tech Zolutions Inc.

The project focuses on network architecture, subnetting, routing, network services, traffic analysis, and layered security controls. The network is divided into **Inside, DMZ, Conference, and Internet** zones, with departmental segmentation within the Inside zone.

> **Educational project:** This repository is provided as a portfolio demonstration of networking and cybersecurity concepts.

## Network Architecture

The network is divided into four security zones:

- **Inside Zone** — Sales & Marketing, Development, and IT departments
- **DMZ Zone** — Web, DHCP, and Email services
- **Conference Zone** — isolated network for conference/visitor systems
- **Internet Zone** — treated as an untrusted external network

Each internal department is assigned its own subnet to support network management and access-control policies.

## Network Design & Configuration

### Subnetting

The network uses subnetting based on departmental host requirements. The implementation includes separate subnets for:

- Sales & Marketing
- Development
- IT
- Conference
- DMZ/services
- Internet/WAN connectivity

### Routing — OSPF

OSPF is configured between the routers to advertise the connected networks through **area 0**.

This provides dynamic routing between the network segments rather than relying entirely on static routes.

### DHCP

A central DHCP server is configured in the DMZ.

DHCP pools are created for the relevant internal subnets, while router interfaces use DHCP relay/IP helper addresses to forward client requests to the server.

### Web Services

An HTTP/HTTPS server is deployed in the DMZ using a static IP address.

Connectivity is tested from hosts in the different network zones.

### Email Services

SMTP and POP3 are configured on the email server.

Email access is controlled according to departmental requirements, with Sales & Marketing and IT receiving email functionality while Development is restricted.

### SSH

SSH is configured on the network routers for remote administration.

The configuration uses local authentication and restricts remote VTY access to SSH rather than Telnet.

## Security Controls

### Network Segmentation

The network is separated into security zones to reduce unnecessary communication between trusted and untrusted systems.

The Conference Zone is isolated from the Inside Zone because it is intended for external visitors.

### Zone-Based Policy Firewall

Cisco Zone-Based Policy Firewall (ZPF) policies are used to control traffic between:

- Inside ↔ DMZ
- Inside ↔ Internet
- Inside ↔ Conference
- DMZ ↔ Internet
- DMZ ↔ Conference
- Conference ↔ Internet

Policies use stateful inspection to control permitted protocols between zones.

### Access Control Lists

Extended ACLs provide more granular access control within the Inside Zone.

Examples include:

- Sales & Marketing — HTTP/HTTPS and email access
- Development — HTTP/HTTPS access
- IT — broader administrative access including SSH, FTP, web and email services
- Sales & Marketing and Development — blocked from directly accessing the IT subnet
- Unmatched traffic — denied by the ACL policy

### Device Security

Network devices are configured with:

- Console authentication
- Privileged access protection
- Encrypted password configuration
- Login banners
- SSH remote administration

## Traffic Analysis

The project also analyses network traffic at multiple layers.

Examples include:

- ICMP Echo Request/Reply
- ARP and Ethernet II frames
- DHCP Discover, Offer, Request and ACK
- TCP connection establishment
- HTTP traffic
- SMTP email traffic

The analysis demonstrates how packets move between hosts, routers and services and how addressing and encapsulation change across network layers.

## Security Testing

The completed network was tested against the intended access-control policies.

Examples include:

- Development cannot directly access IT
- Sales & Marketing cannot directly access IT
- Conference systems can obtain addresses through DHCP
- Internet systems cannot obtain DHCP service from the internal DHCP server
- Development cannot use the restricted email service
- Sales & Marketing can use the permitted email service
- Hosts can access the permitted web services
- IT can remotely administer routers using SSH
- Development and Sales & Marketing cannot remotely administer network devices through SSH

These tests were used to verify that the implemented ACL and zone policies matched the intended network-security requirements.

## Technologies & Concepts

- Cisco Packet Tracer
- IPv4 addressing
- Subnetting
- OSPF
- DHCP
- DHCP relay / IP helper
- HTTP / HTTPS
- SMTP / POP3
- SSH
- Access Control Lists (ACLs)
- Zone-Based Policy Firewall (ZPF)
- ICMP
- ARP
- TCP/IP
- Network segmentation
- Traffic analysis

## Project Structure

```text
network-architecture-packet-tracer/
├── Packet-Tracer-Project.pkt
├── README.md
└── .gitignore
```

Screenshots can be added later under a `screenshots/` directory to provide visual documentation of the topology and security configuration.

## Security & Repository Notes

The original coursework report is **not included** in this repository.

Do not commit:

- Coursework reports containing credentials
- Real passwords
- Personal/student information
- Unnecessary generated files

Before making the Packet Tracer file public, verify that any credentials stored inside the `.pkt` file are non-sensitive and suitable for public release. If the original coursework credentials are still present, replace them with dummy portfolio credentials before publishing.

## Future Improvements

Possible extensions include:

- VLAN-based segmentation
- More granular inter-VLAN ACL policies
- Additional firewall policies
- Centralised logging and monitoring
- DNS infrastructure
- Network intrusion detection
- Redundant routing paths
- More extensive automated connectivity/security testing

## Author

**Arronveer Patter**

Cyber Security BSc — University of Warwick

GitHub: [@AP26759](https://github.com/AP26759)
