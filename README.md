<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

## Environments and Technologies Used

- Microsoft Azure (Virtual Machines)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDP, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

## Operating Systems Used

- Windows 10 (21H2)
- Ubuntu Server 20.04

## Actions and Observations

Welcome to my tutorial on Network Security Groups and Inspecting Network Protocols. First, you need to create two VMs on Azure. One machine will be a Linux machine, and the other will be a Windows 10 machine. Both should have two CPUs and must be on the same VNET.

### Wireshark and ICMP Traffic

1. Download Wireshark on the Windows machine from [Wireshark Download](https://www.wireshark.org/download.html).
2. Open Wireshark and filter for ICMP traffic only. ICMP is a network layer protocol used for network connection diagnostics.
   
   ![ICMP Traffic](https://i.imgur.com/IIUShxp.png)

3. Visualize the packets and inspect the actual data in each ping.

   ![Packet Inspection](https://i.imgur.com/GLxSIG3.png)

4. Perpetually ping the Linux machine using the command `ping -t`. While pinging, block inbound ICMP traffic on the Linux machine by creating a new Network Security Group and set it to block ICMP.

   ![NSG Block ICMP](https://i.imgur.com/5vXO75R.png)
   
   ![NSG Allow ICMP](https://i.imgur.com/Asl80tN.png)

### SSH Traffic

5. Use the Windows machine to SSH into the Linux machine. Set Wireshark to capture SSH packets only.

   ![SSH Traffic](https://i.imgur.com/zteR41r.png)

### DHCP Traffic

6. Filter for DHCP traffic. Request a new IP address using the command `ipconfig /renew`.

   ![DHCP Traffic](https://i.imgur.com/vU8fpQf.png)

### DNS Traffic

7. Filter for DNS traffic. Initiate DNS traffic with the command `nslookup www.google.com`.

   ![DNS Traffic](https://i.imgur.com/VMcwmsO.png)

### RDP Traffic

8. Finally, filter for RDP traffic using the command `tcp.port==3389`. Observe the non-stop traffic as we use Remote Desktop Protocol to connect to our Virtual Machine.

   ![RDP Traffic](https://i.imgur.com/VxXGv6X.png)
