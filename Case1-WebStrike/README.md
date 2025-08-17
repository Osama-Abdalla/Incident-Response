# Case1 WebStrike

## Scenario 
A suspicious file was identified on a company web server, raising alarms within the intranet. The Development team flagged the anomaly, suspecting potential malicious activity. To address the issue, the network team captured critical network traffic and prepared a PCAP file for review.
Your task is to analyze the provided PCAP file to uncover how the file appeared and determine the extent of any unauthorized activity.

## Tools:
- Wireshark.

## Walkthrough
## 1. Analyze PCAP Traffic
The investigation begins by loading the provided PCAP file into Wireshark. Using the Statistics → IPv4 Statistics → Conversations feature, we can quickly identify which IP addresses generated the most traffic. Among the captured connections, one IP address stands out as highly active and performing suspicious behavior. This IP is flagged as the attacker’s IP address, which will serve as the pivot point for further analysis.

![photo_5839179773635578259_w](https://github.com/user-attachments/assets/91a2568c-8df6-44d9-982d-af549e3ddd4e)

## 2. Determine Attacker’s Geographical Origin
Once the suspicious IP is identified, the next step is to investigate its geographical location using a geo-IP lookup service such as WhatIsMyIPAddress. The analysis shows that the attacker originates from Tianjin, China. This information helps contextualize the attack and may later be correlated with known threat intelligence feeds.

![photo_5839179773635578259_w](https://github.com/user-attachments/assets/c94c70ec-0a51-4064-9c0b-898b30659725)


## 3. Extract Attacker’s User-Agent
To better understand how the attacker interacted with the server, we filter HTTP traffic using the expression:
http.request.method == "GET"
Examining the request headers reveals the attacker’s User-Agent string. In this case, it corresponds to a Linux system running Firefox:
Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0
This confirms the attacker was using a browser-based method to interact with the target system.

<img width="1427" height="620" alt="image" src="https://github.com/user-attachments/assets/178729d4-9497-4686-a64b-92f4a738a1ed" />

## 4. Identify the Malicious Web Shell Filename
In this analysis, the Wireshark filter ip.src == 117.11.88.124 and http.request.method=="POST" is applied to isolate HTTP POST requests originating from the attacker's IP address, 117.11.88.124. This filter ensures that only relevant traffic—specifically requests where the attacker may be uploading files or exploiting vulnerabilities—is displayed.the attacker attempts to upload a file named image.php via the /reviews/upload.php endpoint.
This attempt is rejected by the server with an Invalid file format error message, indicating some server-side validation.

<img width="675" height="183" alt="image" src="https://github.com/user-attachments/assets/181a236f-494d-4c86-af0d-62dd55338d7c" />

In the second POST request, the attacker slightly modifies the file name to image.jpg.php and attempts to upload the same malicious content via the same endpoint.

<img width="788" height="317" alt="image" src="https://github.com/user-attachments/assets/60e0a7ab-32a4-464d-bd5f-356d780130fe" />

This technique is a common method used by attackers to bypass file upload restrictions and gain remote access to web servers.

## 5. Determine the Port Used by the Web Shell
After establishing persistence, the attacker attempted to open an interactive session with the compromised server. By examining unusual outbound traffic, we notice connections leaving the server on TCP port 8080. This port was being used by the web shell to establish a remote connection, likely serving as a reverse shell for the attacker to issue commands on the target system.

<img width="768" height="78" alt="image" src="https://github.com/user-attachments/assets/d62d2444-bb8a-4169-b271-9c581f01382c" />

## 6.Identify Exfiltrated File
Finally, by analyzing the TCP streams associated with the attacker’s IP, we detect an attempt to exfiltrate sensitive data. The attacker accessed and transferred the contents of the Linux /etc/passwd file, which contains system account information. While the file itself does not hold passwords in modern Linux systems, it provides valuable reconnaissance data to attackers, such as valid usernames for future brute-force or privilege escalation attempts.

<img width="862" height="657" alt="image" src="https://github.com/user-attachments/assets/264704df-8867-4c95-af1c-972004611aaf" />

