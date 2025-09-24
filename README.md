# Network-Labs
Networking experiments, configs and lab notes  
Hands on networking labs: subnetting, routing, DNS, and wireshark captures 
### Currently: 🌐 Day 1 — Networking Foundations: Seeing the Invisible
🔹 Introduction

Day 1 is all about understanding the building blocks of how your computer talks to the network.
Think of it like learning how cars move on the road before learning to drive Formula 1 — you need to see the basics before you can race.

By the end of this lesson, you should be able to:

- Identify which “door” your system uses to access the network (interfaces).

- Understand what a MAC address is and why it matters.

- Capture and read live network traffic (packets).

- Recognize ARP, ICMP (ping), and TCP’s famous 3-way handshake.

- Discover devices around you with a basic scan.

- Use a simple tool (Netcat) to create direct communication.

- Automate packet analysis with Python + Scapy.


🔹 Step 1: Identifying Your Network Interface

Your system can have multiple network interfaces — Ethernet (wired), Wi-Fi (wireless), or even virtual ones.
Each one is like a separate doorway to the internet.

Why it matters: You need to know which doorway is active before capturing traffic. Otherwise, you’ll just be staring at an empty corridor.

Key learning: Interfaces often have names like eth0, ens33, enp0s3, or wlan0. The system’s routing table shows which one is carrying traffic to the internet.


🔹 Step 2: Understanding MAC Addresses

Every interface has a MAC address — a unique hardware ID burned into your network card.
It looks like this: 08:00:27:12:34:56.

Why it matters:

On your local network, devices don’t talk to IPs first — they talk to MACs.

Think of MAC addresses as license plates for your devices. They’re how switches and ARP keep track of “who’s who” on the local road.


🔹 Step 3: Capturing ARP & ICMP Packets

Now we start “listening to the traffic.” Using tools like tcpdump or Wireshark, you captured packets in real time.

ARP: The protocol that asks, “Who has this IP? Tell me your MAC.”

Example: Who has 192.168.1.1? Tell 192.168.1.10

Reply: 192.168.1.1 is at aa:bb:cc:dd:ee:ff

ICMP: The protocol behind ping. It checks reachability between devices.

Example: Echo request → Echo reply

Why it matters:

ARP is the glue between IP and MAC addresses.

ICMP is the simplest way to confirm if a host is alive.

Attackers can exploit ARP (via ARP spoofing) or ICMP (ping sweeps), while defenders monitor them for anomalies.


🔹 Step 4: The TCP 3-Way Handshake

When you visit a website, your system doesn’t just send data blindly. It performs a handshake first:

SYN → “Hey, can we talk?”

SYN/ACK → “Sure, let’s talk!”

ACK → “Cool, let’s start.”

Why it matters:

This is the foundation of every reliable connection on the internet.

If you understand this, you can later learn attacks like SYN floods, or defenses like SYN cookies.


🔹 Step 5: Basic Local Network Scan

Using nmap, you discovered active devices on your local network.

Why it matters:

Scanning is what attackers do first — mapping the terrain.

As a defender, knowing what’s on your network prevents “shadow devices” from hiding.


🔹 Step 6: Netcat Testing

Netcat (often called the Swiss Army knife of networking) let you create a simple chat between two terminals.

Why it matters:

It shows how raw connections work without the complexity of web browsers or apps.

In pentesting, Netcat is used for backdoors, file transfer, and debugging.

In defense, you might spot unauthorized Netcat traffic in logs.


🔹 Step 7: Automating with Python + Scapy

Finally, you wrote a small script that extracts MAC address pairs from a packet capture.

Why it matters:

This is your first taste of building custom tools.

As networks get bigger, automation is key. You can’t manually analyze every packet.


🔹 Key Takeaways

Interfaces = doorways. MAC = license plate. IP = street address.

ARP finds “who lives where.” ICMP tests reachability.

TCP handshake builds reliable conversations.

Scanning = discovery. Netcat = raw communication.

Scripting = automation and power.

