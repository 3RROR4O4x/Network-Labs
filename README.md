# Network-Labs
Networking experiments, configs and lab notes  
Hands on networking labs: subnetting, routing, DNS, and wireshark captures 
### Currently: Week1 (Networking Foundations :Ethernet, ARP, IP, ICMP, TCP handshake)
## 🎯 **Objectives**

*Understand how your machine connects to the network.

*Learn how to identify your network interface and MAC address.

*Capture and analyze Ethernet frames, ARP requests/replies, and ICMP (ping) traffic.

*Observe a TCP 3-way handshake in action.

*Perform basic network scans and traffic inspection.

### 🔧 Step 1 — Identify Your Active Interface

# Check all network interfaces and pick the one carrying your Internet traffic.

# ip addr show
# ip route show

#Look for an interface like eth0, ens33, enp0s3, or wlan0 with an IP (e.g. 192.168.1.x).

Confirm with ip route show → the line default via ... dev <iface> tells you which one is used.

#Example:
default via 192.168.1.1 dev eth0
#Here, the interface is eth0.

###📡** Step 2 — Capture ARP & ICMP Traffic**

#Start capturing with tcpdump:

#sudo tcpdump -i eth0 -nn -w day1_eth.pcap


Trigger some traffic:

#ping -c 4 8.8.8.8         # ICMP to Google DNS
ping -c 3 <your_gateway>  # ARP + ICMP to your router


#Stop capture (Ctrl+C). Inspect:

#tshark -r day1_eth.pcap -q -z io,phs
#wireshark day1_eth.pcap &


#What to look for:

#ARP Request → “Who has X.X.X.X? Tell Y.Y.Y.Y” (broadcast).

#ARP Reply → “X.X.X.X is at aa:bb:cc:dd:ee:ff” (unicast).

#ICMP Echo (ping) → Request/Reply between your IP and target.

###🌐 **Step 3 — Explore Your ARP Cache**
#ip neigh show

#Shows MAC addresses your system has learned.

###🔗** Step 4 — Observe a TCP Handshake**

#Capture HTTP traffic:

#sudo tcpdump -i eth0 -nn tcp and host example.com -w day1_tcp.pcap
curl -I http://example.com


#Open day1_tcp.pcap in Wireshark.
#Filter: tcp.flags.syn==1 (SYN packets).

#Look for:

*SYN → client → server

*SYN-ACK → server → client

*ACK → client → server

*This is the 3-way handshake that establishes a TCP connection.

###🔍** Step 5 — Scan Your Local Network**

#Find your subnet:

*ip -4 addr show dev eth0


#Run a ping sweep:

*sudo nmap -sn 192.168.1.0/24


#Output: list of devices alive on your LAN (with MAC + vendor).

#⚠️ Only scan networks you own or have permission to test.

###💬 **Step 6 — Simple Netcat Test**

#Start a TCP listener:

nc -lvp 54321


#Connect (same machine or another device):

*nc <your_ip> 54321


#Type messages and see them travel through the network. Capture with tcpdump to analyze payload.

###🐍 **Step 7 — Bonus with Scapy**

#List unique MAC pairs from capture:

#from scapy.all import rdpcap
  #pcap = rdpcap("day1_eth.pcap")
#pairs = set((p.src, p.dst) for p in pcap if p.haslayer("Ether"))
  #print("\n".join(f"{s} -> {d}" for s, d in pairs))

#📖 Key Takeaways

*Ethernet frames carry data at Layer 2 (MAC-to-MAC).

*ARP maps IP addresses → MAC addresses.

*ICMP enables diagnostic tools like ping.

*TCP handshake builds reliable connections.

✅ That’s Day 1. You captured, inspected, and understood how traffic actually looks “on the wire.”
