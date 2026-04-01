# detection-lab-01
Using my homelab, I exercised a simulated Nmap port scan and network analysis using Wireshark on my Kali and Metasploitable virtual machines, while practicing SIEM alert rule creation.

1. What attack was run?    
    Using Kali Linux, I was able to use NMAP to port scan my Metasploit-able VM. This “attack” is used as reconnaissance or probing to see which services are alive and accessible to the threat actor. The attack identifies opens ports by analyzing which ports respond with SYN-ACK versus RST.    
2. What I observed in Wireshark
    The pattern I noticed through this exercise, is a single IP address probing a high volume of ports within a short time period (seconds) through the TCP protocol. 
3. SIEM Detection Rule
    We would want an alert that activates when a single IP sends more than 30 SYN packets to different destination ports within 2 seconds. Another way to filter those SYN packets in that timeframe is the percentage of RST packets sent back, as that can be a key identifier to a port scan. 
    The threshold above was used as a baseline for this lab. In proper application, this threshold would require tuning to an organization’s normal network behavior. Larger organizations or environments require different thresholds to help reduce false positives.
    
Evidence:
![metasploitable_pcap.png](/metasploitable_pcap.png)
*Screenshot of a Wireshark PCAP.
 This screenshot shows multiple TCP SYN packets sent from one IP address to multiple ports within a short timeframe. 

![metasploitable_packet_dissection.png](/metasploitable_packet_dissection.png)
*Screen shot of a Wireshark Packet Dissection.
This screenshot shows multiple attempted TCP SYN packets being sent and receiving either ACK or RST packets in return. This allows a threat actor to identify which ports are open.
