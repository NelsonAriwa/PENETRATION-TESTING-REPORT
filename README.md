# PENETRATION-TESTING-REPORT
Footprinting And Network Scanning Phases
FOOTPRINTING & NETWORK SCANNING PHASES
W2-PM-FINAL | CYBERSECURITY |  NETWORKWALKS

Pentester Name
(Cybersecurity Professional)	Chinedum Nelson Ariwa
Program/Batch	B083-Networkwalks
Date	17 September 2026
Modules completed	W2-PM1 (Multiple Kali Tools)
W2-PM5 (Zenmap Scanning)
Client/Target	1. Networkwalks (secured written permission already)
2. My own local LAN Network
Permission secured from client?	Yes
Phases covered	Phase 1: Reconnaissance & Footprinting
Phase 2: Scanning & Network Discovery
Phase 3-5: In Progress




1. Liability Disclaimer
I have performed these activities only on the systems & devices where I had secured written permission or the devices/systems that I own myself. All these materials are for education and research purpose only. Do not use anything from here to break the law. The instructor, the authors and Networkwalks are not responsible for what you do with this knowledge. Every action you take is your own responsibility. Misuse can lead to criminal charges, heavy fines, loss of your job and a permanent record. In most countries unauthorised access is a crime even when nothing is damaged.
 
2. Introduction
This report covers footprinting the networkwalks.com domain using multiple Kali Linux tools (W2-PM1) and scanning my own local network with Zenmap (W2-PM5). One module covers the footprinting phase and the other covers the scanning phase, so together they show how an attacker moves from gathering public information to mapping live hosts on a network. It is the Week 2 part of my ongoing internship program at Networkwalks.
All commands were run in Kali Linux (footprinting) and on a Windows PC with Zenmap installed (scanning). Every step below includes the exact command used, the result I observed, a screenshot as evidence, and a short note on why the finding matters from an attacker's point of view.


3. Tools Used
The table below lists each tool used in this report and its purpose.
Tool	Purpose
Kali Linux & Windows	Operating systems used for reconnaissance activities
WHOIS	Find domain registration details (owner, dates, name servers).
whatweb	Fingerprint the web technologies (server, CMS, plugins, IP).
nslookup	Resolve the domain name to its IP address using DNS.
curl -I	Read the HTTP response headers of the website, to see the server banner, status, cookies and redirects.
wafw00f	Detect whether a Web Application Firewall protects the target site.
dnsrecon	Enumerate all DNS records: Name servers, Mail Servers, Sender Policy Framework, Text Record, and Service Record. (NS, MX, SPF, TXT, SRV).
Zenmap (Nmap GUI)	Scan the local subnet to find live hosts, IPs and MAC addresses.
Windows CMD	Local IP and MAC address identification

4. Activities Performed
4.1 Footprinting & Reconnaissance

I performed reconnaissance against the networkwalks.com domain using six Kali Linux tools: WHOIS, WhatWeb, Nslookup, Curl -I, Wafw00f and DNSRecon. Each tool was used to collect a different type of information about the target.
First, I used WHOIS to obtain publicly available domain registration information and identify the domain’s name servers. The results provided information about the domain registration and hosting infrastructure.
I then used WhatWeb to identify technologies used by the website. The results identified WordPress 7.0.4 and WP Download Manager 3.3.58, along with other information exposed by the website.
Using Nslookup, I resolved the domain name to its IP address. The provided result identified 192.158.56.1
I used Curl with the -I option to inspect the HTTP response headers. This provided additional information about the web application and exposed the WordPress REST API endpoint /wp-json/.
Next, I used Wafw00f to determine whether a Web Application Firewall was protecting the website. The result identified ModSecurity (SpiderLabs).
Finally, I used DNSRecon to enumerate DNS records. The results provided information relating to name servers, mail servers, SPF/TXT records, service records and DNS software information.


4.2 Network Scanning with Zenmap
For the second activity, I used Zenmap to perform network discovery on my local network. The practical required me to identify my local IP address and subnet, discover live hosts, identify their IP and MAC addresses, and generate a network topology.
I first used the Windows ipconfig command to identify my local IP address and LAN subnet. I then entered the subnet into Zenmap and selected Ping Scan to identify active hosts.
I found out only one live active host which was scanned, which is;
192.168.56.1
The results did not include a MAC address.
After completing the scan, I opened the Topology section in Zenmap, enabled the legend and saved the network topology in PDF format as required by the practical task.
Note: The actual subnet, number of hosts and addresses should be replaced with the results from my own network when submitting the report.

 
5. Risk Analysis / Impact
Based on the information collected during the footprinting and network scanning activities, I identified the following potential risks.
#	Risk / Finding	Evidence / Observation	Potential Impact	Risk Level
1	Web technology information exposed	WhatWeb identified WordPress and WP Download Manager	Attackers may use exposed technology/version information to identify software requiring further security review	● Medium
2	Server IP address/Host information exposed	Nslookup  networkwalks.com return the domain 192.232.216.135	Revels the public IP address associated with the domain. The IP address can be used for reconnaissance and infrastructure enumeration.	● Low
3	Server  information exposed/disclosure	Curl –I  response shows server: Apache and 	Exposing the server type gives attacker additional information about the technology stack.	● Low
4	WAF technology identifiable	Wafw00f identified ModSecurity (SpiderLabs) protecting the target.	Reveals information about the web application’s networkwalkks.com is protected by Modsecurity (SpiderLabs) Web Application Firewall after two requests were made to the target.	● Low
5	DNS Public IP address information exposed	DNSRecon identified DNS, mail and service-related records	It provides attackers with information about the organization’s DNS infrastructure can assist reconnaissance.	● Medium
6	Single live hosts visible on local network	Zenmap identified one live hosts with my local LAN network	The discovered host confirms that an active system is reachable. If it exposes open ports or services, an attacker could use this information for further reconnaissance and potentially target vulnerable services.	● Medium

Risk level key:  ● Critical  ● Medium  ● Low
The risks above are observations from the footprinting and scanning exercises, not confirmed vulnerabilities.
The practical exercises primarily involved information gathering and host discovery. No exploitation or vulnerability validation was performed as part of these two modules.
Therefore, the presence of information such as a software version, IP address or DNS record does not by itself mean that the system is vulnerable. Further authorized security testing would be required to confirm any actual vulnerability.



6. Recommendations
Based on the observations from these activities, I recommend the following security improvements:
1.	Review publicly exposed technology information
Organizations should regularly review what information about their web technologies, CMS and plugins is publicly visible.
2.	Keep software updated
CMS platforms, plugins and other web technologies should be regularly updated and reviewed against current security advisories.
3.	Review HTTP headers
HTTP response headers should be reviewed to determine whether unnecessary technical information is being exposed.
4.	Review DNS records regularly
DNS records should be checked periodically to ensure that only required information and services are publicly exposed.
5.	Properly configure and monitor the WAF
Keep the WAF (ModSecurity) enabled and tuned, since it already blocks naive attacks.
6.	Perform regular internal network discovery
Organizations should periodically scan their own networks to identify active devices.
7.	Investigate unknown devices
Any unexpected device discovered during network scanning should be investigated and verified.
8.	Maintain network documentation
Network topology and device information should be documented and updated regularly.
9.	Perform security testing with authorization
Reconnaissance and scanning should only be performed against systems and networks where appropriate authorization has been provided.

7. Conclusion
During Week 2 of my Cybersecurity & Ethical Hacking internship, I completed practical activities covering footprinting, reconnaissance and network scanning.
In the footprinting activity, I used six Kali Linux tools to collect information about the target domain. I learned how WHOIS can provide domain information, WhatWeb can identify web technologies, Nslookup can resolve domain names, Curl can inspect HTTP headers, Wafw00f can identify a WAF, and DNSRecon can provide additional DNS information.
In the network scanning activity, I used Zenmap to identify my local network configuration and discover active hosts. I also collected IP and MAC address information and created a network topology.
The exercises showed me that information gathering is an important part of cybersecurity. Even before attempting to exploit a system, a security professional can learn a significant amount about an environment by carefully analyzing publicly available information and network responses.
I also learned that technical findings should be documented clearly. A good cybersecurity report should explain what was performed, what was discovered, what the observation means, what risk it may create, and what can be done to reduce that risk.
Finally, I learned that reconnaissance and scanning must always be performed within an authorized scope. These activities were completed as part of the assigned educational cybersecurity lab.

8. Evidences Collected
<img width="1366" height="728" alt="Window - ScreenPal - 3 25 4 (30)" src="https://github.com/user-attachments/assets/56d2006c-070c-4b6c-a2ad-d2e64ed709de" />
 <img width="1366" height="728" alt="Window - ScreenPal - 3 25 4 (31)" src="https://github.com/user-attachments/assets/8c4bdb26-05bf-47ce-b34f-08ef4104ccd7" />
<img width="1366" height="728" alt="Window - ScreenPal - 3 25 4 (32)" src="https://github.com/user-attachments/assets/8d1d7d3f-c34e-458e-ae50-822f6d8cb1c1" />
<img width="1366" height="728" alt="Window - ScreenPal - 3 25 4 (33)" src="https://github.com/user-attachments/assets/54984c9e-13c3-4ddc-bff0-0a58fc0ccc09" />
<img width="1366" height="728" alt="Window - ScreenPal - 3 25 4 (34)" src="https://github.com/user-attachments/assets/b2627196-f9f8-49f0-933c-bfc15304cb1e" />
<img width="1366" height="728" alt="Window - ScreenPal - 3 25 4 (35)" src="https://github.com/user-attachments/assets/75e23453-688b-4594-9098-a65eee8f24b1" />
<img width="1366" height="728" alt="Window - ScreenPal - 3 25 4 (43)" src="https://github.com/user-attachments/assets/e40bb913-bbfa-4157-bb80-3782d57f49a6" />
<img width="1366" height="768" alt="Topology" src="https://github.com/user-attachments/assets/75e04537-30df-493e-93c3-099beb4c773b" />
<img width="1366" height="728" alt="Window - ScreenPal - 3 25 4 (46)" src="https://github.com/user-attachments/assets/53e511bc-5ad7-46c5-99f1-92aff693934f" />

 
 
 

 


 

 


 




-End-


bersecurity program at Networkwalks | Week: 02 | Repository: GitHub

