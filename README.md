<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we use Wireshark to examine the flow of network traffic between two Azure Virtual Machines and explore how Network Security Groups function. <br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDP, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Install Wireshark
- Start Wiresharks packet capture 
- Observe Traffic
- Setup Network Security Group/Add rule (Firewall)
- Observe Traffic after Firewall

<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
    Install Wireshark/Download Wireshark

-Go to Wireshark Download Page.

-Select the installer for your operating system (Windows, macOS, or Linux).

Run the Installer

-Launch the installer and follow the on-screen prompts.

-If prompted to install additional components (e.g., WinPcap or Npcap on Windows), accept them to allow Wireshark to capture traffic.

Verify Installation

-Open Wireshark from the Start Menu (Windows), Applications folder (macOS), or your system’s app menu (Linux).

(Wireshark should open without errors)
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
   Start Wireshark’s Packet Capture
  
Select a Network Interface

-Once Wireshark is open, you’ll see a list of available network interfaces (Ethernet, Wi-Fi, etc.).

-Choose the interface you want to monitor (usually the one with active traffic).

Begin Capture

-Click the Start Capturing button or double-click the interface.

-Wireshark will begin displaying live packets in the capture window.

Capture Duration

-Let the capture run for a short period (e.g., a few minutes) while you browse the internet or use other network-based applications.


(This ensures you collect enough packets for observation)
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
   Observe Traffic
  
Real-Time Packet List

-Notice the constant flow of packets in the main window. Each row represents a single packet with time, source/destination IP, protocol, and more.

Apply Basic Filters

-Use Wireshark’s display filter (e.g., ip.addr == <your IP> or tcp.port == 80) to focus on specific traffic.

(This helps you zoom in on interesting traffic such as HTTP, HTTPS, DNS, etc)

Analyze Packet Details

-Attempt to Ping you Linux VM

-Click on any packet to view its details (headers, payload, etc.) in the pane below.

(Observe how protocols like TCP, UDP, ICMP, or DNS appear)
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Set Up Network Security Group / Add Firewall Rule


Navigate to Your Cloud Firewall or NSG of the virtual machine you are attempting to ping

For Azure, open the Network Security Group in the Azure Portal ( Virtual Machine -->Network Settings--> Netowrk Security Groups).

-Create or Modify a Rule

(Example: Block inbound ICMP traffic to Linux VM.)

*Save your changes and wait a few seconds for the rule to take effect*.

Confirm the Configuration

-Ensure the new rule is active by reviewing your NSG or firewall settings.

(Make sure you understand whether the rule is inbound or outbound)
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Observe Traffic After Firewall
  
*Run Another Wireshark Capture*

-Start a new Wireshark capture so you can compare “before and after” results.

Use the same interface to maintain consistency.

Attempt Network Activity

-Try performing the same actions as before ( send pings, etc.) that should be affected by the firewall rule.

(If you blocked ICMP, attempt to ping that machine)

Look for Blocked or Dropped Packets

Depending on how your firewall/NSG is configured, you might see RST (reset) or no response for blocked connections.

(Filter Wireshark for the relevant IP, port, or protocol to see how traffic is being handled differently)
</p>
<br />
