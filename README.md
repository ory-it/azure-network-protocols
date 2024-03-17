<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create our Resources
- Observe ICMP Traffic
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe DNS Traffic
- Observe RDP Traffic
- Lab Cleanup

<h2>Actions and Observations</h2>

![Screenshot 2024-03-17 at 10 58 35 AM](https://github.com/ory-it/azure-network-protocols/assets/67742620/edd4db2d-18c7-45a0-b8e1-c98521491edd)
<h3>Create our Resources</h3>

1. Create a Resource Group 
2. Create a Windows 10 Virtual Machine (VM)
  a. While creating the VM, select the previously created Resource Group
  b. While creating the VM, allow it to create a new Virtual Network (Vnet) and Subnet
3. Create a Linux (Ubuntu) VM
  a. While create the VM, select the previously created Resource Group and Vnet
4. Observe Your Virtual Network within Network Watcher


![Screenshot 2024-03-17 at 1 11 35 PM](https://github.com/ory-it/azure-network-protocols/assets/67742620/67d47ffe-c57b-4ca7-a0ab-1c99be36cb93)
<h3>Observe ICMP Traffic</h3>

5. Use Remote Desktop to connect to your Windows 10 Virtual Machine
6. Within your Windows 10 Virtual Machine, Install Wireshark
7. Open Wireshark and filter for ICMP traffic only
8. Retrieve the private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM
  a. Observe ping requests and replies within WireShark
9. From The Windows 10 VM, open command line or PowerShell and attempt to ping a public website (such as www.google.com) and observe the traffic in WireShark
10. Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM
  a. Open the Network Security Group your Ubuntu VM is using and disable   incoming (inbound) ICMP traffic
  b. Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity
  c. Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is using
  d. Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (should start working)
  e. Stop the ping activity


![Screenshot 2024-03-17 at 1 28 10 PM](https://github.com/ory-it/azure-network-protocols/assets/67742620/a37c014e-54af-44cd-8114-7bf5fe9d4b3f)
<h3>Observe SSH Traffic</h3>

11. Back in Wireshark, filter for SSH traffic only
12. From your Windows 10 VM, “SSH into” your Ubuntu Virtual Machine (via its private IP address)
  a. Type commands (username, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark
  b. Exit the SSH connection by typing ‘exit’ and pressing [Enter]


![Screenshot 2024-03-17 at 1 32 15 PM](https://github.com/ory-it/azure-network-protocols/assets/67742620/e7ef4210-a3bf-425c-a795-467649b6cf73)
<h3>Observe DHCP Traffic</h3>

13. Back in Wireshark, filter for DHCP traffic only
14. From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew)
  a. Observe the DHCP traffic appearing in WireShark



![Screenshot 2024-03-17 at 1 33 24 PM](https://github.com/ory-it/azure-network-protocols/assets/67742620/053e1b6d-975b-4a6c-bd78-e1dcaa4899c4)
<h3>Observe DNS Traffic</h3>

15. Back in Wireshark, filter for DNS traffic only
16. From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are
  a. Observe the DNS traffic being show in WireShark


![Screenshot 2024-03-17 at 1 35 44 PM](https://github.com/ory-it/azure-network-protocols/assets/67742620/d1968563-6139-4eb9-b5ee-78ba0b2d8c6a)
<h3>Observe RDP Traffic</h3>

17. Back in Wireshark, filter for RDP traffic only (tcp.port == 3389)
18. Oserve the immediate non-stop spam of traffic? Why do you think it’s non-stop spamming vs only showing traffic when you do an activity?
  a. Answer: because the RDP (protocol) is constantly showing you a live stream from one computer to another, therefor traffic is always being transmitted


![Screenshot 2024-03-17 at 1 36 49 PM](https://github.com/ory-it/azure-network-protocols/assets/67742620/ab8f261f-73d4-4330-9e3a-b03aebe41f6c)
<h3>Lab Cleanup</h3>

19. Close your Remote Desktop connection
20. Delete the Resource Group(s) created at the beginning of this lab
21. Verify Resource Group Deletion
