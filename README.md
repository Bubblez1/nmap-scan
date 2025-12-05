Namae: Bernice Mafu
Student Number: 2022044985
Course Name: Information Management Security
Assignment Number: 2 (two)
Title: Pactical Nmap workflow 

This document summarizes and interprets the findings from the Nmap XML scan file, `nmap_scan.xml`, which targeted the IP address `182.27.134.119`. 
The scan was initiated on Friday, December 5, 2025, using the command `/usr/lib/nmap/nmap -Pn -oX nmap_scan.xml 182.27.134.119`. 
The target host's reverse DNS record identifies it as an Amazon EC2 instance: ec2-182-27-134-119.ap-southeast-6.compute.amazonaws.com`, suggesting the host resides within the AWS cloud environment. 
The Nmap scan performed a TCP SYN scan across 1000 common ports. 
The results indicate that the host is highly secured and/or heavily filtered. Out of the 1000 ports scanned, **999 ports** were reported as `filtered`. 
This filtered state means that Nmap's probe packets did not receive a response, which is a strong indicator of an active stateful firewall, like a host-based firewall or an AWS Security Group, dropping the packets before they reach the service. 
This security measure prevents the scanner from determining if the port is truly open or closed.
Crucially, only one port was identified as `open`: TCP Port 21, which corresponds to the File Transfer Protocol (FTP) service.
The open status indicates that a service is actively listening on this port and is accessible through the filtering layer established for the target. 
Since FTP is accessible while almost all other ports are blocked, the filtering mechanism is specifically configured to permit this traffic. 
The presence of this single open port on an otherwise blocked system makes it the sole point of entry for immediate security assessment.
Given the findings, the primary focus for any security investigation should be the **open FTP service on Port 21. 
The next logical step would be to actively connect to the service and use Nmap's scripting engine (`--script`) for deeper enumeration. 
This would involve checking for known vulnerabilities, attempting anonymous access, and identifying the specific software and version of the FTP server running. 
This information is critical for determining the security posture of the host and planning any potential further actions.
