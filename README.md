# Fortune Cloud Technologies – Day 1 Practical Examination

## Practical Examination: Day 1

This repository contains my practical work for **Fortune Cloud Technologies – Day 1**.

The practical covers:

1. Linux IP Investigation
2. IPv4 Address Analysis
3. Dynamic IP Investigation
4. Cloud Linux Server & IP
5. Cloud Network Troubleshooting

The practical was performed using a **Linux environment and AWS EC2**.

---

# Table of Contents

- [Task 1 – Linux IP Investigation](#task-1--linux-ip-investigation)
- [Task 2 – IPv4 Address Analysis](#task-2--ipv4-address-analysis)
- [Task 3 – Dynamic IP Investigation](#task-3--dynamic-ip-investigation)
- [Task 4 – Cloud Linux Server and IP](#task-4--cloud-linux-server-and-ip)
- [Task 5 – Cloud Network Troubleshooting](#task-5--cloud-network-troubleshooting)
- [Commands Used](#commands-used)
- [Practical Results](#practical-results)
- [Screenshots](#screenshots)
- [Learning Outcomes](#learning-outcomes)
- [Conclusion](#conclusion)

---

# Task 1 – Linux IP Investigation

## Objective

The objective of this task was to launch/access a Linux machine and investigate its network configuration.

The following information was checked:

- System IP address
- Network interface
- Default gateway
- DNS information
- Complete network configuration

---

## 1. Check IPv4 Address

Command used:

```bash
ip -4 addr
```

Another command used:

```bash
hostname -I
```

Example observed private IP on the AWS Linux machine:

```text
172.31.27.152
```

---

## 2. Identify the Network Interface

Command used:

```bash
ip link
```

The active network interface observed was:

```text
ens5
```

The interface state was:

```text
UP
```

---

## 3. Find the Default Gateway

Command used:

```bash
ip route
```

Observed route information included:

```text
default via 172.31.16.1 dev ens5
```

Therefore, the default gateway observed during the practical was:

```text
172.31.16.1
```

---

## 4. Find DNS Information

Command used:

```bash
cat /etc/resolv.conf
```

Observed DNS configuration:

```text
nameserver 172.31.0.2
search ec2.internal
```

The file also indicated that the resolver configuration is managed by `systemd-resolved`.

---

## 5. Complete Network Configuration

The following commands were used to investigate the complete network configuration:

```bash
ip addr
ip link
ip route
cat /etc/resolv.conf
hostname -I
```

---

## Task 1 Result

The Linux machine was successfully investigated.

### Summary

| Item | Result |
|---|---|
| Linux IP | 172.31.27.152 |
| Network Interface | ens5 |
| Interface State | UP |
| Default Gateway | 172.31.16.1 |
| DNS Server | 172.31.0.2 |
| Environment | AWS EC2 Linux |

---

# Task 2 – IPv4 Address Analysis

## Objective

The objective was to investigate an IPv4 address, separate it into four octets, identify the value of each octet, determine whether it is private or public, and investigate other accessible systems.

---

## 1. IPv4 Address

The public IPv4 address used for this analysis was:

```text
44.197.247.201
```

The address was obtained from the cloud environment / public IP information.

---

## 2. Separate IPv4 Address into Four Octets

IPv4 address:

```text
44.197.247.201
```

Separated into four octets:

```text
44 . 197 . 247 . 201
```

### Octet Table

| Octet | Value |
|---|---:|
| 1st Octet | 44 |
| 2nd Octet | 197 |
| 3rd Octet | 247 |
| 4th Octet | 201 |

Each octet is within the valid IPv4 range:

```text
0 – 255
```

---

## 3. Private or Public IP

The analyzed address was:

```text
44.197.247.201
```

This address does not fall within the private IPv4 ranges:

```text
10.0.0.0 – 10.255.255.255
172.16.0.0 – 172.31.255.255
192.168.0.0 – 192.168.255.255
```

Therefore:

```text
44.197.247.201 = Public IPv4 Address
```

---

## 4. Investigate Network and Host Information

The following commands were used:

```bash
ip -4 addr
```

```bash
hostname -I
```

```bash
hostname
```

```bash
ip route
```

```bash
cat /etc/resolv.conf
```

Example private address observed inside the AWS Linux instance:

```text
172.31.27.152
```

Hostname observed during the practical:

```text
abhipatil
```

---

## 5. Find Other Accessible Systems

The task requires identifying at least two other systems accessible from the environment.

Commands that can be used are:

```bash
ip neigh
```

and:

```bash
nslookup google.com
```

```bash
nslookup amazon.com
```

or:

```bash
dig google.com
```

```bash
dig amazon.com
```

The actual IP addresses returned by these commands should be recorded as observed during the practical.

### Example Documentation Format

| System / Host | IPv4 Address | Type |
|---|---|---|
| My Linux / EC2 public IP | 44.197.247.201 | Public |
| Google | `<actual output>` | Public |
| Amazon | `<actual output>` | Public |

> The Google and Amazon IP values should be replaced with the actual values returned by the commands during execution rather than using fixed example addresses.

---

## Task 2 Result

The investigated IPv4 address was:

```text
44.197.247.201
```

Its four octets were:

```text
44, 197, 247, 201
```

The IP was classified as a:

```text
Public IPv4 Address
```

Linux networking commands were also used to investigate the local host, interface, route, and DNS configuration.

---

# Task 3 – Dynamic IP Investigation

## Objective

The objective was to investigate the behavior of dynamic IP addressing by recording the IP before and after a reconnect test.

---

## 1. Record IP Before Disconnect

Command used:

```bash
hostname -I
```

Observed:

```text
172.31.27.152
```

A terminal record was created using:

```bash
echo "Before disconnect -> $(hostname -I)"
```

Observed:

```text
Before disconnect -> 172.31.27.152
```

---

## 2. Check Network Connection Status

The intended command was:

```bash
nmcli device status
```

However, during the practical the system returned:

```text
-bash: nmcli: command not found
```

This indicates that `nmcli` / NetworkManager command-line utilities were not installed or available in the current environment.

---

## 3. Reconnect Test

The environment was an AWS EC2 SSH session.

A network disconnect/reconnect operation was not performed through `nmcli`, because the command was unavailable and disconnecting an active EC2 network connection could terminate the SSH session.

The IP was checked again using:

```bash
hostname -I
```

Observed:

```text
172.31.27.152
```

---

## 4. Record IP After Reconnect Check

Command used:

```bash
echo "After reconnect -> $(hostname -I)"
```

Observed:

```text
After reconnect -> 172.31.27.152
```

### Comparison

```text
Before disconnect -> 172.31.27.152
After reconnect    -> 172.31.27.152
```

### Result

```text
IP Changed: No
```

> Note: Because the EC2 network was not actually disconnected, this comparison records the IP before and after the check rather than demonstrating a true DHCP disconnect/reconnect cycle.

---

# Task 4 – Cloud Linux Server and IP

## Objective

The objective was to create an AWS EC2 Linux instance, connect to it using SSH, identify its private and public IP addresses, and compare the information shown in AWS with the information available inside Linux.

---

## 1. AWS EC2 Instance

The AWS EC2 instance used during the practical was:

```text
Name: task1
Instance Type: t3.micro
Operating System: Amazon Linux 2023
Region: US East (N. Virginia)
```

---

## 2. SSH Connection

The EC2 instance was connected using SSH.

Command format:

```bash
ssh -i "key.pem" ec2-user@<PUBLIC-IP>
```

The actual instance was successfully accessed and the Amazon Linux 2023 login screen was displayed.

---

## 3. Find Private IP from Linux

Command used:

```bash
hostname -I
```

Observed:

```text
172.31.27.152
```

The private IPv4 address was also visible using:

```bash
ip -4 addr
```

Observed:

```text
inet 172.31.27.152/20
```

Network interface:

```text
ens5
```

---

## 4. Find Public IP

Command used:

```bash
curl http://checkip.amazonaws.com
```

Observed result:

```text
54.226.60.138
```

The public IP was also visible in the AWS EC2 console.

---

## 5. AWS Console and Linux Comparison

### AWS Console

```text
Public IPv4 Address: 54.226.60.138
Private IPv4 Address: 172.31.27.152
```

### Inside Linux

```bash
hostname -I
```

Result:

```text
172.31.27.152
```

Public IP command:

```bash
curl http://checkip.amazonaws.com
```

Result:

```text
54.226.60.138
```

### Comparison Table

| Information | AWS Console | Inside Linux |
|---|---|---|
| Private IPv4 | 172.31.27.152 | 172.31.27.152 |
| Public IPv4 | 54.226.60.138 | 54.226.60.138 |

---

## Task 4 Result

The AWS EC2 instance was successfully launched and accessed through SSH.

The private and public IP information matched between the AWS console and the Linux environment.

---

# Task 5 – Cloud Network Troubleshooting

## Objective

The objective was to troubleshoot a Linux cloud server systematically when a service could not be accessed.

The troubleshooting sequence included:

1. Check IP address
2. Check network interface
3. Check default route
4. Check network connectivity
5. Check running services
6. Check listening ports
7. Check firewall and AWS security rules
8. Fix the issue
9. Verify that the service works

---

# Troubleshooting Step 1 – Check IP Address

Command:

```bash
hostname -I
```

Observed:

```text
172.31.27.152
```

### Result

The server had a valid private IPv4 address.

---

# Troubleshooting Step 2 – Check Network Interface

Command:

```bash
ip link
```

The primary network interface was:

```text
ens5
```

The interface was in the:

```text
UP
```

state.

### Result

The network interface was operational.

---

# Troubleshooting Step 3 – Check Default Route

Command:

```bash
ip route
```

Observed default route:

```text
default via 172.31.16.1 dev ens5
```

### Result

A default route was available.

---

# Troubleshooting Step 4 – Check Network Connectivity

Command:

```bash
ping -c 4 8.8.8.8
```

Observed result:

```text
4 packets transmitted, 4 received, 0% packet loss
```

### Result

The server had external network connectivity.

---

# Troubleshooting Step 5 – Check Web Service

The Apache service was checked first.

Command:

```bash
sudo systemctl status httpd
```

Initially, the service was not available.

The installation was then performed using:

```bash
sudo yum install httpd
```

After installation, Apache was started:

```bash
sudo systemctl start httpd
```

Status was checked:

```bash
sudo systemctl status httpd
```

The service showed:

```text
Active: active (running)
```

and:

```text
Started, listening on port 80
```

---

# Troubleshooting Step 6 – Install and Configure Nginx

Nginx was also installed for web-server testing.

Command:

```bash
sudo yum install nginx
```

Apache was stopped before starting Nginx:

```bash
sudo systemctl stop httpd
```

Nginx was started:

```bash
sudo systemctl start nginx
```

Status:

```bash
sudo systemctl status nginx
```

Observed:

```text
Active: active (running)
```

---

# Troubleshooting Step 7 – Check Listening Ports

Command:

```bash
sudo ss -tulpn
```

The output showed web-server traffic listening on port:

```text
80
```

Example:

```text
0.0.0.0:80
```

Nginx was associated with the listening port.

---

# Troubleshooting Step 8 – Test Service Locally

Command:

```bash
curl http://localhost
```

The command returned the Nginx default welcome page.

The response included:

```text
Welcome to nginx!
```

### Result

The Nginx web server was working successfully from inside the EC2 instance.

---

# Troubleshooting Step 9 – AWS Security Group

The AWS EC2 Security Group was inspected.

The following inbound rules were present during the practical:

| Type | Protocol | Port | Source |
|---|---|---:|---|
| HTTP | TCP | 80 | 0.0.0.0/0 |
| Custom TCP | TCP | 90 | 0.0.0.0/0 |
| Custom TCP | TCP | 5000 | 0.0.0.0/0 |
| SSH | TCP | 22 | 0.0.0.0/0 |

### Important Security Note

For production systems, exposing ports to:

```text
0.0.0.0/0
```

should be avoided when possible.

Access should be restricted to trusted IP addresses or networks where appropriate.

---

# Task 5 – Troubleshooting Documentation

## Problem

The web service was not available initially because the required HTTP service was not installed/running.

## Commands Used

```bash
sudo systemctl status httpd
sudo yum install httpd
sudo systemctl start httpd
sudo systemctl status httpd
sudo yum install nginx
sudo systemctl stop httpd
sudo systemctl start nginx
sudo systemctl status nginx
sudo ss -tulpn
curl http://localhost
```

## Output

The final Nginx service was:

```text
Active: active (running)
```

The web server was listening on:

```text
Port 80
```

The local HTTP request returned the Nginx welcome page.

## Cause

The web service required for HTTP access was not running initially.

## Solution

The web server was installed and started.

Nginx was configured and started after stopping Apache to avoid both services competing for port 80.

## Final Result

The web service successfully responded to:

```bash
curl http://localhost
```

and returned the Nginx welcome page.

---

# Commands Used

## Linux Networking Commands

```bash
ip addr
```

```bash
ip -4 addr
```

```bash
ip link
```

```bash
ip route
```

```bash
hostname
```

```bash
hostname -I
```

```bash
cat /etc/resolv.conf
```

```bash
ip neigh
```

---

## Connectivity Commands

```bash
ping -c 4 8.8.8.8
```

```bash
curl http://checkip.amazonaws.com
```

```bash
curl http://localhost
```

---

## DNS Commands

```bash
nslookup google.com
```

```bash
nslookup amazon.com
```

```bash
dig google.com
```

```bash
dig amazon.com
```

---

## Service Commands

```bash
sudo systemctl status httpd
```

```bash
sudo systemctl start httpd
```

```bash
sudo systemctl stop httpd
```

```bash
sudo systemctl status nginx
```

```bash
sudo systemctl start nginx
```

---

## Package Installation Commands

```bash
sudo yum install httpd
```

```bash
sudo yum install nginx
```

---

## Port Investigation

```bash
sudo ss -tulpn
```

---

# Practical Results

## Task 1

Linux network configuration was successfully investigated.

```text
Private IP : 172.31.27.152
Interface  : ens5
Gateway    : 172.31.16.1
DNS        : 172.31.0.2
```

---

## Task 2

IPv4 address analyzed:

```text
44.197.247.201
```

Octets:

```text
44 . 197 . 247 . 201
```

Classification:

```text
Public IPv4 Address
```

---

## Task 3

Observed IP record:

```text
Before disconnect -> 172.31.27.152
After reconnect   -> 172.31.27.152
```

Observed result:

```text
IP Changed: No
```

The actual network disconnect/reconnect was not performed through `nmcli` because the command was unavailable in the environment.

---

## Task 4

AWS EC2:

```text
Instance Type: t3.micro
OS: Amazon Linux 2023
```

Public IP:

```text
54.226.60.138
```

Private IP:

```text
172.31.27.152
```

SSH access was successfully established.

---

## Task 5

The cloud server was successfully tested and troubleshot.

Final web service:

```text
Nginx
```

Listening port:

```text
80
```

Verification:

```bash
curl http://localhost
```

Result:

```text
Welcome to nginx!
```

---

# Screenshot Documentation

The practical submission contains screenshots for the major steps of each task.

Recommended screenshot organization:

```text
screenshots/
│
├── task1/
│   ├── ip-address.png
│   ├── network-interface.png
│   ├── route.png
│   └── dns.png
│
├── task2/
│   ├── ipv4-analysis.png
│   ├── hostname.png
│   ├── network-information.png
│   └── other-systems.png
│
├── task3/
│   ├── before-disconnect.png
│   ├── connection-status.png
│   └── after-reconnect.png
│
├── task4/
│   ├── ec2-console.png
│   ├── ssh-login.png
│   ├── private-ip.png
│   └── public-ip.png
│
└── task5/
    ├── connectivity.png
    ├── service-status.png
    ├── nginx-install.png
    ├── listening-ports.png
    ├── localhost-test.png
    └── security-group.png
```

---

# Technologies Used

- AWS EC2
- Amazon Linux 2023
- Linux
- IPv4
- SSH
- DNS
- Apache HTTP Server
- Nginx
- AWS Security Groups
- Linux Networking
- `ip`
- `ping`
- `curl`
- `ss`
- `systemctl`
- `yum`

---

# Learning Outcomes

Through this practical, I learned how to:

- Check Linux IP configuration
- Identify network interfaces
- Identify default gateways
- Check DNS configuration
- Analyze IPv4 addresses
- Separate an IPv4 address into octets
- Identify public and private IPv4 addresses
- Check Linux routing information
- Investigate network connectivity
- Understand dynamic IP behavior
- Launch an AWS EC2 Linux server
- Connect to EC2 using SSH
- Identify EC2 private and public IP addresses
- Install Apache and Nginx
- Start and stop Linux services
- Check listening network ports
- Test web services using `curl`
- Inspect AWS Security Group rules
- Troubleshoot cloud networking and web services

---

# Conclusion

The Day 1 practical provided hands-on experience with Linux networking and AWS cloud infrastructure.

I investigated Linux network configuration, analyzed IPv4 addressing, recorded dynamic IP behavior, created and accessed an AWS EC2 Linux server, compared public and private IP addresses, and performed systematic cloud network troubleshooting.

The final web-service test confirmed that the Nginx service was running and responding successfully on port 80.

---

# Author

**Abhishek Madge**

## Learning Focus

```text
AWS
Cloud Computing
Linux
DevOps
Networking
Web Servers
```

---

# Repository Purpose

This repository is created for practical learning, documentation, and demonstration of Linux networking and AWS cloud administration skills.
