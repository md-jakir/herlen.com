# Link:

[Site:](https://herlan.com)

WordPress Application host in AWS with resilient architecture

# https://harlen.com - Project Overview
This is an E-commerce WordPress application hosted in Godaddy hosting provider. Client was facing the application load issues in the existing hosting platform with current setup. According to business growth it can't handle traffic with the system specifications and there was no load balancer setup to distribute the traffic into available backed systems.

There was another issue with server optimisations. PHP-FPM and Nginx weren't optimized properly. 

# Data Collection for Requirement Analysis:
I investigated the whole system and collect system level metrics data like CPU, RAM usages, write down Python script to get RAM usages data for each PHP-FPM and Nginx reuest. Installed some investigation tools in the Linux system to get disk performance, CPU performance data. 

# Users and System Space CPU usages at 12:05.03 PM on 27th June
![image](https://github.com/user-attachments/assets/e6885707-dabb-4baa-807f-63deb78871cd)

# RAM behavior at 12.05.03 PM on 27th June
![image](https://github.com/user-attachments/assets/96b3e193-13ce-4bac-87a0-03f0a0ff5806)
# TPS to Disk at 12.05.03 PM on 27th June
![image](https://github.com/user-attachments/assets/dd4fea9b-93aa-41e7-bd2e-580443304c00)
# Notice: 
_A larger number of PHP-FPM and Apache requests were found at that time and hold Apache requests for a long period._
