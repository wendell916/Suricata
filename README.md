# Suricata IDS

# What is Suricata?

Suricata is an open-source network Intrusion Detection System (IDS) and Intrusion Prevention System (IPS), as well as a network monitoring tool. This documentation is based on version 7.0.8, which is the latest at the time of writing. Developed by the Open Information Security Foundation (OISF), Suricata uses pre-defined signatures to detect anomalies or threats within a network.

# Features of Suricata

* Intrusion Detection and Prevention (IDS/IPS): Suricata detects and prevents known threats by using signatures, which are pre-defined rules.

* Network Security Monitoring: Suricata provides detailed metadata about network flows, including flow duration, packet counts, and byte counts.

* Deep Packet Inspection (DPI): It analyzes network traffic in detail, including the application layer (e.g., HTTP, DNS, FTP, SMTP).

* Protocol Detection and Logging: Suricata supports decoding and logging of protocols such as HTTP, TLS, FTP, and DNS.

# How Does Suricata Work?

* Suricata listens to network traffic via a network interface card (NIC) configured in promiscuous mode.

* The captured traffic is then analyzed against known or configured signatures.

* If a match is found, an alert is generated.

* Logs are created containing metadata, protocol details, and addresses for deeper investigation.

# Problem Statement

Without a robust intrusion detection and prevention system like Suricata, network traffic remains vulnerable to threats that can progress unchecked. The lack of traffic analysis increases the risk of regulatory non-compliance, delayed incident response, incomplete forensic investigations, and reduced threat intelligence. Organizations become reactive and vulnerable to evolving cyber threats.

# Objective

To enhance threat detection and identify network anomalies, addressing the issues highlighted in the problem statement.

# Tools Used

* Ubuntu Server

* VMware

# Project Scope

* This project provides a detailed guide on installing Suricata on an Ubuntu server, analyzing, monitoring, and generating alerts for investigation and remediation.

* Limitation: This project focuses only on the IDS functionality of Suricata. It uses an out-of-band network architecture that listens to traffic but cannot prevent attacks actively.

# Implementation Process

# Requirements

For optimal performance, Suricata recommends:

At least 2 CPU cores

4 GB of RAM

# Project Setup:

7 GB of RAM

2 CPU cores

# Installation

1 Make sure to have an installed Ubuntu Server.


Run the following commands in the ubuntu terminal:

``````
sudo apt-get install software-properties-common
``````
Installs software-properties-common

`````
sudo add-apt-repository ppa:oisf/suricata-stable
``````
Adds a Personal Package Archive (PPA) to your debain-based linux system

``````
sudo apt update
``````
Updates the local packages
``````
sudo apt install suricata jq
``````
This command installs suricata and the jq tool that will be used to parse the logs into json format 

Verify Suricata's status with the command 
``````
sudo systemctl status suricata
``````

Determine the interface and IP address of the server with the command,
``````
ip a
``````
Configure Suricata:

Use a preferred text editor (e.g., nano):

nano /etc/suricata/suricata.yaml

Modify the following:

Home_Net Section: Update the IP address of the local network.

AF-Packet Section: Set the interface to the one used by your network.

Update signatures:

sudo suricata-update
sudo systemctl restart suricata

Testing Suricata

Perform an aggressive Nmap scan on the server running Suricata.

View alerts:

tail -f /var/log/suricata/fast.log

Alerts generated from the Nmap scan can be found in /var/log/suricata/fast.log.

# Challenges

Due to a NIC that doesn’t support promiscuous mode, I was unable to monitor all traffic on the network, except for the Ubuntu server hosting Suricata.

# Results

* Learned how Suricata works.

* Understood how rules generate alerts.

* Successfully installed and deployed Suricata.

# References

https://docs.suricata.io/en/latest/

# Future Enhancements

Integration with Wazuh (Open-source SIEM): Display alerts directly on a dashboard in real-time, eliminating the need for manual checks.
