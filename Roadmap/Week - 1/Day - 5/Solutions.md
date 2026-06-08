# Networking Basics — Solutions

## 1. OSI Model

### Simple definition
- The OSI model is a conceptual framework that divides network communication into seven layers.
- Layers: Physical, Data Link, Network, Transport, Session, Presentation, Application.

### Why it matters in cybersecurity
- It helps analysts isolate where failures or attacks occur.
- Security controls are often applied at different layers, such as firewalls at Layer 3 and application controls at Layer 7.

### How it works step-by-step
1. Data originates at the Application layer.
2. Each layer adds headers or transforms data for transport.
3. The Physical layer transmits bits over wire or air.
4. The reverse happens at the receiving host, stripping headers layer by layer.

### Common attack methods
- Layer 2: MAC spoofing, ARP poisoning.
- Layer 3: IP spoofing, route hijacking.
- Layer 4: TCP SYN flood, port scanning.
- Layer 7: SQL injection, web application attacks.

### IOCs
- Unexpected ARP table changes.
- Abnormal TCP connection attempts.
- Application errors and malformed traffic.

### Logs/events to monitor
- Network device logs for MAC and routing changes.
- Firewall logs at Network/Transport layers.
- Web server and application logs at Layer 7.

### SIEM detection techniques
- Map rules to OSI layers and correlate across layers.
- Alert on Layer 2 anomalies plus suspicious application activity.

### Prevention and mitigation
- Apply defense in depth across all layers.
- Use network segmentation, encryption, and secure coding.

### Incident response actions
- Identify the impacted OSI layer and isolate affected infrastructure.
- Capture packet data and application logs.

### Real-world example
- A web attack exploiting Layer 7 vulnerabilities while reconnaissance is done at Layer 3/4.

### Interview Q&A
- Q: "What is the OSI model used for?"
  A: "To provide a standardized way to understand network communication and troubleshoot issues at each layer."
- Q: "Which layer does a firewall operate on?"
  A: "Typically Layer 3/4 for packet filtering, and Layer 7 for application-level firewalls."

### Practical lab exercises
- Map common protocols to OSI layers.
- Use Wireshark to view packet encapsulation.

### TryHackMe / HTB suggestions
- TryHackMe: `OSI Model`, `Network Fundamentals`.

### Important tools used
- Wireshark, tcpdump, nmap, firewall logs.

### Key commands
- `tcpdump -i eth0`
- `tshark -V`

### Summary
- OSI is the backbone of network understanding and a useful model for SOC analysts.

## 2. TCP/IP Model

### Simple definition
- The TCP/IP model is a practical networking model with four layers: Link, Internet, Transport, Application.

### Why it matters in cybersecurity
- It matches real-world Internet protocols and helps analysts understand traffic flow.

### How it works step-by-step
1. Application layer creates a payload.
2. Transport layer segments data using TCP or UDP.
3. Internet layer routes packets using IP.
4. Link layer delivers frames on the physical network.

### Common attack methods
- IP spoofing at Internet layer.
- UDP amplification at Transport layer.
- DNS poisoning at Application layer.

### IOCs
- Suspicious IP fragments.
- Unexpected TCP/UDP ports.

### Logs/events to monitor
- Packet capture and flow logs.
- IDS alerts for IP and transport anomalies.

### SIEM detection techniques
- Build detection rules around TCP flags and IP anomalies.
- Monitor for out-of-sequence or malformed packets.

### Prevention and mitigation
- Use anti-spoofing ACLs, segment networks, and harden application services.

### Incident response actions
- Trace attack path through TCP/IP layers.
- Capture packet headers and flow records.

### Real-world example
- UDP reflection DDoS attacks exploit Transport and Internet layer protocols.

### Interview Q&A
- Q: "How does TCP differ from UDP?"
  A: "TCP is connection-oriented and reliable; UDP is connectionless and faster but best-effort."
- Q: "What is the Internet layer responsible for?"
  A: "Routing packets between networks using IP."

### Practical lab exercises
- Capture TCP vs UDP traffic.
- Analyze packet headers in Wireshark.

### TryHackMe / HTB suggestions
- TryHackMe: `Network Services`, `TCP/IP`.

### Important tools used
- Wireshark, tshark, tcpdump, nmap.

### Key commands
- `tcpdump -i eth0 tcp`
- `tcpdump -i eth0 udp`

### Summary
- The TCP/IP model is the practical reference for network traffic and security monitoring.

## 3. Ports and Protocols

### Simple definition
- Ports identify application endpoints on hosts.
- Protocols are rules for communication between endpoints.

### Why it matters in cybersecurity
- Knowing ports and protocols helps identify allowed services, detect unauthorized access, and build firewall rules.

### How it works step-by-step
1. A service listens on a port.
2. A client connects using a protocol over TCP or UDP.
3. Data is exchanged according to the protocol specification.

### Common attack methods
- Port scanning to discover services.
- Exploiting vulnerable services on open ports.
- Protocol misuse or injection.

### IOCs
- Unexpected open ports.
- Connections to known malicious port/protocol combinations.

### Logs/events to monitor
- Firewall logs showing allowed/denied ports.
- NIDS alerts for protocol anomalies.
- Service logs for unexpected connections.

### SIEM detection techniques
- Correlate source IP, destination port, and service.
- Alert on known risky ports like 445, 3389, 22 from suspicious sources.

### Prevention and mitigation
- Close unused ports and harden exposed services.
- Use service whitelisting and network segmentation.

### Incident response actions
- Identify the service and process behind the port.
- Block or isolate the host if the port is unauthorized.

### Real-world example
- Attackers scan port 22 and exploit weak SSH credentials.

### Interview Q&A
- Q: "What is port 443 used for?"
  A: "HTTPS secure web traffic."
- Q: "Why is port 53 important?"
  A: "It is used for DNS, which is critical for name resolution and a common target."

### Practical lab exercises
- Scan a lab network with `nmap -sS -sU`.
- Identify open ports and map them to services.

### TryHackMe / HTB suggestions
- TryHackMe: `Port Scanning`, `Networking`.

### Important tools used
- `nmap`, `ss`, `netstat`, IDS/IPS.

### Key commands
- `nmap -sS -p 1-1024 <target>`
- `ss -tuln`

### Summary
- Ports and protocols define how traffic flows. SOC analysts must map them to services and monitor for unauthorized or abnormal usage.

## 4. Common Services

### Simple definition
- Common services are widely-used network applications like web, DNS, SSH, and email.

### Why it matters in cybersecurity
- These services are frequent attack targets. Monitoring them reduces risk and improves incident detection.

### How it works step-by-step
1. A host runs a service on a port.
2. Clients connect and authenticate.
3. Service logs and network traffic reveal activity.

### Common attack methods
- Web application attacks on HTTP/HTTPS.
- Brute-force SSH attacks.
- DNS tunneling and cache poisoning.
- Email phishing and malware delivery.

### IOCs
- Multiple failed SSH logins.
- Strange DNS queries or long domain names.
- Unexpected HTTP methods or abnormal URLs.

### Logs/events to monitor
- Web server access/error logs.
- DNS query logs.
- SSH authentication logs.
- Email gateway logs.

### SIEM detection techniques
- Alert on brute-force patterns and abnormal service access.
- Correlate DNS queries with endpoint alerts.

### Prevention and mitigation
- Patch services, use MFA, and deploy WAFs for web applications.
- Harden SSH with key-based auth and disable root login.

### Incident response actions
- Quarantine affected service hosts.
- Review service logs and correlate with network traffic.

### Real-world example
- A web server exploited via an unpatched CMS plugin leading to data theft.

### Interview Q&A
- Q: "What port does HTTPS use?"
  A: "443"
- Q: "How do you secure SSH?"
  A: "Use keys, disable password auth, and restrict access with firewalls."

### Practical lab exercises
- Analyze HTTP logs for suspicious requests.
- Investigate SSH auth logs for brute-force attempts.

### TryHackMe / HTB suggestions
- TryHackMe: `Web Fundamentals`, `SSH Basics`, `DNS`.

### Important tools used
- `curl`, `nmap`, `bro/Zeek`, `Splunk`, `ELK`, `OSSEC`.

### Key commands
- `journalctl -u sshd`
- `grep "Failed password" /var/log/auth.log`
- `curl -I https://example.com`

### Summary
- Common services are high-value targets. Monitoring, hardening, and logging these services are essential for SOC operations.
