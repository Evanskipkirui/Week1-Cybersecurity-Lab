# Week1-Cybersecurity-Lab

🔐 Cybersecurity Lab Environment Setup

Building an isolated virtual lab for penetration testing and ethical hacking practice

📌 Project Overview

This project focuses on setting up a virtual cybersecurity and penetration-testing laboratory using VirtualBox and Kali Linux.

The purpose of the lab is to create a controlled environment where cybersecurity tools, network scanning, reconnaissance, vulnerability assessment, and other security-testing activities can be performed safely and repeatedly. The lab is configured on a private virtual network so that additional machines can be added later and used as targets for authorized security testing.

🎯 Objectives

The main objectives of this project are to:

Install and configure VirtualBox.

Install/import Kali Linux as a virtual machine.

Create a private NAT Network for the cybersecurity lab.

Configure network connectivity for Kali Linux.

Assign a consistent IP address to the Kali VM.

Verify network connectivity and DNS resolution.

Take a clean VM snapshot for recovery.

Document the complete setup process.

Prepare the environment for future cybersecurity projects.

🛡️ Purpose of the Lab
The lab provides an isolated and controlled environment for cybersecurity learning and authorized security testing.

It can be used for activities such as:

Network reconnaissance

Port scanning

Vulnerability assessment

Packet analysis

Web security testing

Exploitation practice

Security-tool experimentation

⚠️ Important: This laboratory must only be used for systems that you own or have explicit permission to test. Do not use the lab or its tools to attack unauthorized systems.

🏗️ Lab Architecture

The lab is built on an isolated VirtualBox NAT Network (`10.0.0.0/24`). 

**[ Ubuntu Host Machine ]**

  └── **VirtualBox Hypervisor**
  
        └── **NAT Network (10.0.0.0/24)**
        
              └── **[ Kali Linux VM ]** (IP: 10.0.0.2/24)
              
                    ├── Gateway: 10.0.0.1
                    
                    └── DNS: 8.8.8.8

*Future target machines (Windows/Android) can be added to this same NAT Network (e.g., 10.0.0.10, 10.0.0.11).*

The lab consists of a Host OS running VirtualBox, which hosts a Kali Linux Virtual Machine connected to a private NAT Network (10.0.0.0/24). Additional target machines (Windows/Android) can be added to the same virtual network in future projects.

⚙️ Lab Configuration

🧩 Component	⚙️ Configuration

🖥️ Host OS	Ubuntu Linux (Noble 24.04)

🧠 Host RAM	16 GB

🧰 Hypervisor	VirtualBox 7.1

🐉 Security OS	Kali Linux 2026.3

🧠 Kali RAM	2048 MB

🌐 Virtual Network	NAT Network

📡 Network Address	10.0.0.0/24

🐧 Kali IP Address	10.0.0.2/24

🚪 Default Gateway	10.0.0.1

🌍 DNS Server	8.8.8.8

🔮 Future VM Range	10.0.0.3–10.0.0.99

🪜 Lab Setup Procedure

VirtualBox Installation: Installed VirtualBox via the official Oracle repository using the Ubuntu terminal.

NAT Network Creation: Created a dedicated NAT Network named NatNetwork with the IPv4 Prefix set to 10.0.0.0/24 and DHCP enabled.

Kali Linux Import: Downloaded the official Kali Linux VirtualBox image (.7z), extracted it using p7zip, and imported the .vbox file into VirtualBox.

VM Configuration: Configured the VM to use the NAT Network, allocated Base Memory, and enabled bi-directional Clipboard and Drag-and-Drop.

Shared Folders: Added a shared folder named downloads pointing to the Ubuntu /home/evans/Downloads directory with Auto-mount enabled.

Network Configuration: Configured the static IP 10.0.0.2/24 inside Kali using the nmcli command-line tool.

Snapshot: Created a clean snapshot named Phase 1 - Complete to serve as a baseline recovery point.

🔎 Lab Verification

✅ Test	🧾 Command	🎯 Expected Result

🌐 Check IP address	ip a	inet 10.0.0.2/24 displayed on eth0

📡 Test gateway	ping 10.0.0.1	Successful replies

🌍 Test Internet connectivity	ping -c 4 google.com	4 packets transmitted, 0% packet loss

📁 Verify Shared Folders	GUI Check	sf_Downloads accessible on Kali desktop

🐞 Problems Encountered & Solutions

Problem 1: Network Connection Failed (IP configuration could not be reserved)

Cause: When trying to bring the network interface up after setting the static IP, Kali's Duplicate Address Detection (DAD) blocked the activation, likely conflicting with VirtualBox's internal NAT engine.

Solution: Disabled DAD by running the following command (as advised on Page 7 of the lab PDF):

sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0

Then restarted the connection using sudo nmcli connection up "Wired connection 1".

Problem 2: VirtualBox GUI Freeze During Snapshot

Cause: Attempted to take a "live" snapshot while the VM was running with limited CPU allocation. The VirtualBox GUI hung at 99%, causing Ubuntu to display a "Not Responding" error.

Solution: Force-quit the frozen VirtualBox GUI. Rebooted Kali, shut the VM down cleanly from the OS, and took the snapshot while the machine was in a "Powered Off" state. This completed successfully without freezing.

💡 What I Learned

Through this project, I learned how to create and configure a virtual environment for cybersecurity practice. The most important concepts I learned include:

NAT vs NAT Network: Understanding how a NAT Network allows multiple VMs to communicate with each other while sharing the host's internet connection.

Virtual Machine Networking: How VirtualBox virtual network adapters connect VMs to different types of networks.

Static IP Configuration: How to configure and verify IPv4 addressing, subnet masks, gateways, and DNS settings in Kali Linux.

VM Snapshots: The importance of creating a clean snapshot before performing risky operations to provide a known-good recovery point.

Documentation: The importance of documenting commands, configuration, and troubleshooting steps for professional projects.

🔗 Tools & Resources

7-Zip: https://7-zip.org/download.html

VirtualBox: https://virtualbox.org/wiki/Downloads

Kali Linux: https://kali.org/get-kali

👤 Author

[Evans Rono]

Cybersecurity Intern

Program Name: Cybersecurity at Networkwalks | Week: 01 | Project: Cybersecurity & Pentesting Lab Setup

NAT Network

<img width="1836" height="1011" alt="Screenshot from 2026-10-27 14-08-17" src="https://github.com/user-attachments/assets/bd50edd1-851b-4f1c-ad2e-6a5d6770297d" />

Shared Folders

<img width="1836" height="1011" alt="Screenshot from 2026-10-27 14-15-20" src="https://github.com/user-attachments/assets/149eaf6b-69b8-4389-b0ec-a064cebed56b" />

IP Address

<img width="1854" height="965" alt="Screenshot_2026-10-27_07_18_07" src="https://github.com/user-attachments/assets/adfa2fbf-79ee-464c-8d30-5c4361367852" />

Ping Test

<img width="1854" height="965" alt="Screenshot_2026-10-27_07_18_25" src="https://github.com/user-attachments/assets/d0997844-b1fa-4de2-9f10-4cb7876eeb75" />



