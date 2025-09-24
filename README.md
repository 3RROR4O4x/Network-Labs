# Network-Labs
Networking experiments, configs and lab notes  
Hands on networking labs: subnetting, routing, DNS, and wireshark captures 
### Currently: Week1 (Networking Foundations :Ethernet, ARP, IP, ICMP, TCP handshake)

## Objectives
- Identify the active network interface and MAC address on Kali.
- Capture and analyze Ethernet frames, ARP requests/replies, and ICMP traffic.
- Observe a TCP 3-way handshake.
- Run a basic local network scan and a netcat test.
- Produce a short PCAP timeline and a small script to parse captures.

Step 1 — Identify Your Active Interface

- Check all network interfaces and pick the one carrying your Internet traffic.


  USE
- ip addr show
- ip route show

- Look for an interface like eth0, ens33, enp0s3, or wlan0 with an IP (e.g. 192.168.1.x). 
- Confirm with ip route show → the line default via ... dev <iface> tells you which one is used.

Example:
- default via 192.168.1.1 dev eth0


Here, the interface is eth0.
