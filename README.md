# Suricata IDS
What is suricata
Suricata is network IDS/IPS networking monitoring tool.This documentation is written on version 7.0.8 which is the latest at the time of writing this documentation. Suricata uses signatures  used to detect anomalies or threats in the network. Suricata is open source and it was developed by Open Information Security Foundation.

Features of Suricata

Intrusion Detection and Prevention(IDS/IPS):Just like I have mentioned earlier suricata can detect and prevent known threats by using signatures.Signatures are pre-defined rules.
Network Security Monitoring: In addition to IDS/IPS functionality, it provides detailed metadata about network flows, including flow duration, packet counts, and byte counts.
Deep Packet Inspection(DPI): It can analyze network traffic in detail, including the application layer (e.g., HTTP, DNS, FTP, SMTP).
 Protocol Detection and Logging:Suricata supports decoding and logging of network protocols such as HTTP, TLS, FTP, and DNS.

How does suricata work

Suricata listens network traffic via network interface card that support and are in  promiscuous mode. 
The captured traffic is analyzed against the configured or known signatures it has and knows. 
If it matches a particular network traffic against a known signature, an alert is generated
Logs are generated of the metadata files, protocol, address details for deeper investigation.

Problem
Without a robust intrusion detection and prevention system like Suricata in place, network traffic remains vulnerable to a variety of threats that can progress unchecked.Additionally, the absence of traffic analysis increases the risk of regulatory non-compliance.Without real-time alerts or detailed traffic logs, organizations face delayed incident response, incomplete forensic investigations, and reduced threat intelligence, leaving them reactive and vulnerable to evolving cyber threats.

Objective
To ehance threat detection and network anomalies in the network that better enhance the problems stated earlier in the problem statement.

Tools Used
Ubuntu Server
Vmware



Project Scope

This project gives a detailed description of how suricata was installed on an ubuntu server and how traffic is analysed,monitored and  alerted for investigation and remidiation. 
Limitation: This project only looks at the IDS of Suricata. It is can out of band network architecture that actively  listen to the network traffic.Hence it cannot a prevent an attack from happening in the network.


Implementation Process

To install suricata,we will need an ubuntu server where suricata will be installed on to actively listen on the network for anomalies.

Requirements
For optimal performance, Suricata recommends at least 2 CPU cores and 4 GB of RAM. In a production environment, you typically need at least two CPUs and 4–8 GB of RAM.

In this project, I used 7gb of RAM and 2 core cpus.
  

Installation
Have an installed version of an ubuntu server.
Run the following commands in your ubuntu server terminal.
sudo apt-get install software-properties-common
sudo add-apt-repository ppa:oisf/suricata-stable
sudo apt update
sudo apt install suricata jq
The dedicated PPA repository is added, and after updating the index, Suricata can be installed. We recommend installing the jq tool at this time as it will help with displaying information from Suricata's EVE JSON output
Run the command to see the status of suricata whether it is running.
Sudo systemctl status suricata

The next thing is to determine the interface and  ip address of the server that will be inspecting the network traffice, Use the command ip a

Based on that information  we are going to configure Suricata.
Use any preferred text editor of your choice.But I will be using nano
Run the command  nano  /etc/suricata/suricata.yaml
We will configure the following
Home_Net section:Change the ip address of your local network that is being used.


Af-packet: Change the interface being used with the interface your network is using. 


The next thing to do is to update the suricate signatures. Suricata uses Signatures to trigger alerts so it's necessary to install those and keep them updated. Use the command
 sudo suricata-update.
With the rules installed, restart suricata using the command
sudo systemctl restart suricata



Testing suricata
In testing whether suricata is working, I run an aggressive nmap scan on to the server that is running suricata.


Alerts generated in suricata can be found in the /var/log/suricata/fast.log
Because of how voluminous the alerts can be, I just used the 
tail -f /var/log/suricata/fast.log to view if an alert has been generated with the nmap scan earlier.
The results is shown below.


Challenges
Because my personal NIC doesn’t support promiscuous mode, I was not able to monitor all traffic in the network, expect the ubuntu server that has suricata installed on it.

Results
I was able to learn how suricata works, how with the use of rules alerts can be generated and how to install and deploy suricata.

References
https://docs.suricata.io/en/latest/index.html

Future Enhancements
Integrating suricata with an open source siem preferably wazuh.
This can help display alerts directly on the dashboard as and when they happen.
It will prevent me from manually checking for alerts.

