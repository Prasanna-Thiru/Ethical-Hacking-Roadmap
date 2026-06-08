# Linux Networking — Solutions

## 1. IP Addressing

### Simple definition
- IP addressing assigns a unique numeric address to each device on a network.
- IPv4 uses four octets (e.g. `192.168.1.10`); CIDR notation like `/24` describes the network prefix.

### Why it matters in cybersecurity
- Correct IP addressing is critical for segmentation, routing, access control, and detection of unauthorized hosts.
- Misconfigured or spoofed addresses can allow attackers to bypass controls.

### How it works step-by-step
1. A device boots and obtains an IP address via static configuration or DHCP.
2. The subnet mask/CIDR determines which addresses are local vs routed.
3. The gateway forwards traffic outside the subnet.
4. ARP resolves local IP addresses to MAC addresses.

### Common attack methods
- IP spoofing: attacker forges source IP to masquerade as a trusted host.
- ARP poisoning: manipulates local IP-to-MAC mappings to intercept traffic.
- DHCP starvation: exhausts DHCP leases to deny service or force rogue DHCP.
- Network scanning: identifies hosts and ports in an IP range.

### Indicators of compromise (IOCs)
- Duplicate IP address alerts.
- Unexpected IP ranges on critical VLANs.
- High rate of DHCPDISCOVER messages.
- ARP table changes and unknown MACs.

### Logs and events to monitor
- DHCP server logs and lease activity.
- Firewall and router logs for unusual source IPs.
- Switch and router MAC address learning events.
- IDS/IPS alerts for ARP anomalies and scan behavior.

### Detection techniques using SIEM tools
- Create rules for duplicate IP detection and DHCP exhaustion.
- Alert on traffic from unauthorized IP ranges or unexpected network segments.
- Correlate DHCP logs with authentication and access logs.

### Prevention and mitigation
- Use DHCP snooping, dynamic ARP inspection, and port security.
- Apply IP address management (IPAM) and network segmentation.
- Restrict access to critical subnets with ACLs and firewalls.

### Incident response actions
- Isolate suspicious host or VLAN.
- Capture ARP tables and network device MAC learning tables.
- Correlate events from DHCP, switch logs, and IDS.
- Remediate misconfigured devices and revoke rogue DHCP leases.

### Real-world example
- Attackers spoof internal IPs to bypass network access controls and gain lateral movement in a corporate LAN.

### Interview Q&A
- Q: "What is CIDR and why is it useful?"
  A: "CIDR stands for Classless Inter-Domain Routing. It lets you represent subnet masks compactly and create flexible subnet sizes like `/28` or `/24`."
- Q: "How does DHCP snooping help prevent attacks?"
  A: "DHCP snooping validates DHCP messages and blocks unauthorized DHCP servers from assigning addresses."

### Practical lab exercises
- Configure a Linux host with static and DHCP IPs.
- Use `ip addr`, `ip route`, and `arp -n` to inspect networking.
- Analyze DHCP traffic with Wireshark.

### TryHackMe / Hack The Box practice suggestions
- TryHackMe: `Network Fundamentals`, `Linux Fundamentals`, `ARP Poisoning`.
- Hack The Box: beginner rooms that require network scanning and local host enumeration.

### Important tools used
- `ip`, `ifconfig`, `route`, `arp`, `dhclient`, `nmap`, `tcpdump`, `Wireshark`.

### Key commands
- Linux:
  - `ip addr show`
  - `ip route show`
  - `arp -n`
  - `ip addr add 192.168.1.100/24 dev eth0`
- Windows:
  - `ipconfig /all`
  - `route print`
  - `arp -a`

### Summary
- IP addressing is the foundation of network visibility and control. SOC analysts must understand how addresses are assigned, how spoofing and ARP attacks work, and how to detect anomalies through DHCP, firewall, and switch logs.

## 2. ifconfig / ip a

### Simple definition
- `ifconfig` and `ip a` are tools for viewing and managing network interfaces and IP addresses on Linux.
- `ip a` is part of the modern `iproute2` suite and is the preferred command.

### Why it matters in cybersecurity
- Accurate interface configuration is essential for secure connectivity, network segmentation, and forensic analysis.
- Analysts use these tools to verify host network status during incident response.

### How it works step-by-step
1. Query interfaces: `ip a` shows active and inactive interfaces.
2. Examine assigned IPs, MAC addresses, and link status.
3. Change interface state or assign/remove addresses as needed.

### Common attack methods
- Misconfigured interfaces can expose management networks.
- Attackers may add secondary IP addresses to hide traffic.
- VPN/Tunnel interfaces can be abused for data exfiltration.

### IOCs
- Unexpected enabled interfaces (e.g., `tun0`, `tap0`).
- Missing or incorrectly configured gateway.
- Duplicate or unusual IP addresses on hosts.

### Logs and events to monitor
- Host logs of interface up/down events.
- Network device logs for abnormal interface states.
- Endpoint detection system alerts when new interfaces appear.

### Detection techniques using SIEM tools
- Monitor host configuration changes and interface creation.
- Alert on interface state changes outside maintenance windows.
- Correlate unexpected local IP changes with process execution.

### Prevention and mitigation
- Enforce configuration baselines using configuration management tools.
- Use network access control to block unauthorized interfaces.
- Harden hosts against unauthorized virtualization or tunneling.

### Incident response actions
- Capture interface configuration immediately.
- Compare with known-good baselines.
- Remove unauthorized addresses or interfaces if safe.

### Real-world example
- A compromised system creates a `tun` interface for a covert VPN backdoor and hidden C2 traffic.

### Interview Q&A
- Q: "Why is `ip a` preferred over `ifconfig`?"
  A: "`ip` supports more modern features, better IPv6 handling, and unified network management syntax."
- Q: "How do you check a Linux interface status?"
  A: "Use `ip link show` or `ip a` to view link state and assigned addresses."

### Practical lab exercises
- Use `ip a` to document the network state on a Linux VM.
- Bring an interface up/down and assign a second IP.
- Compare output from `ifconfig` and `ip a`.

### TryHackMe / Hack The Box practice suggestions
- TryHackMe: `Linux Fundamentals`, `Intro to Linux`.
- HTB: beginner boxes where network interface troubleshooting is needed.

### Important tools used
- `ip`, `ifconfig`, `iproute2`, `nmcli`, `ethtool`.

### Key commands
- `ip a`
- `ip link show`
- `ip addr add 192.168.1.50/24 dev eth0`
- `ip link set eth0 up`
- `ifconfig eth0 192.168.1.50 netmask 255.255.255.0`

### Summary
- `ip a` is a core Linux command for inspecting network interfaces. SOC analysts use it during triage to validate host connectivity and detect suspicious interface changes.

## 3. ping, traceroute

### Simple definition
- `ping` tests ICMP reachability to a remote host.
- `traceroute` maps the network path and shows each hop to a destination.

### Why it matters in cybersecurity
- These tools are used for troubleshooting connectivity and spotting network filtering or interception.
- Attackers also use them for reconnaissance, so SOCs watch for anomalous scan activity.

### How it works step-by-step
1. `ping` sends ICMP Echo Requests and waits for Echo Replies.
2. `traceroute` sends packets with incrementing TTL values.
3. Each router returns TTL-expired messages, revealing hop IPs.
4. Analysts use results to identify routing issues and path-based anomalies.

### Common attack methods
- ICMP scanning identifies live hosts.
- `traceroute` can reveal network topology for planning attacks.
- Smurf/ICMP flood attacks abuse ICMP traffic.

### IOCs
- High volume of ICMP requests from a single host.
- Frequent traceroute probes to internal or sensitive hosts.
- Failed or blocked ICMP responses on normally reachable services.

### Logs and events to monitor
- Firewall/IDS logs for ICMP and traceroute packets.
- Router and switch logs when TTL expires unexpectedly.
- Endpoint network logs showing repeated connectivity checks.

### Detection techniques using SIEM tools
- Alert on large ICMP packets or many ICMP echo requests.
- Detect traceroute patterns using multiple TTL values.
- Correlate ICMP scanning with port scan activity.

### Prevention and mitigation
- Restrict ICMP at perimeter firewalls to reduce reconnaissance.
- Use rate limiting for ICMP and disable unnecessary ICMP services.
- Block unauthorized traceroute and ping from untrusted networks.

### Incident response actions
- Identify source of suspicious ICMP traffic.
- Check if it's benign troubleshooting or malicious scanning.
- Block or quarantined hosts exhibiting scanning behavior.

### Real-world example
- A threat actor scans a subnet with `ping` and `traceroute` before launching a lateral movement campaign.

### Interview Q&A
- Q: "What is the purpose of `traceroute`?"
  A: "It shows the path packets take through the network, which helps identify routing issues and intermediate devices."
- Q: "How can ICMP be abused by attackers?"
  A: "Attackers use ICMP for host discovery and can launch denial-of-service attacks like ping floods."

### Practical lab exercises
- Run `ping -c 4 8.8.8.8` and interpret packet loss and RTT.
- Run `traceroute google.com` and identify each hop.
- Use `tcpdump icmp` to capture ping traffic.

### TryHackMe / Hack The Box practice suggestions
- TryHackMe: `Network Traffic Analysis`, `Introduction to Networking`.
- HTB: beginner boxes where network reconnaissance is required.

### Important tools used
- `ping`, `traceroute`, `tracepath`, `tcpdump`, `Wireshark`, `fping`.

### Key commands
- `ping -c 4 8.8.8.8`
- `traceroute example.com`
- `tracepath example.com`
- `tcpdump -n icmp`

### Summary
- `ping` and `traceroute` are essential troubleshooting and reconnaissance tools. SOC analysts use them to validate connectivity and detect suspicious network discovery activity.

## 4. netstat, ss

### Simple definition
- `netstat` and `ss` show network connections, listening ports, and socket statistics.
- `ss` is the modern replacement for `netstat` with better performance and more options.

### Why it matters in cybersecurity
- Monitoring open ports and established connections helps identify malicious services, backdoors, and unauthorized communication.
- Analysts use these tools for endpoint triage and network forensics.

### How it works step-by-step
1. Run `ss -tuln` to view listening services.
2. Use `ss -tunap` to display active connections and associated processes.
3. Compare output with expected service configurations.
4. Investigate unexpected ports or connections.

### Common attack methods
- Port scanning to discover services.
- Backdoors listening on non-standard ports.
- Malware making outbound connections to C2 servers.

### IOCs
- Unknown process listening on a high-numbered port.
- Connections to suspicious external IP addresses.
- Services bound to localhost that should not exist.

### Logs and events to monitor
- Endpoint process and network activity logs.
- EDR alerts for unknown network listeners.
- Application logs showing unexpected remote connections.

### Detection techniques using SIEM tools
- Correlate process names with open ports.
- Alert on new listening sockets or unusual remote destinations.
- Track changes in socket state from `ss`/`netstat` snapshots.

### Prevention and mitigation
- Harden systems by disabling unused services.
- Use host-based firewalls to restrict listening ports.
- Apply least privilege to network-facing applications.

### Incident response actions
- Capture current socket state and process details.
- Kill malicious processes if safe and document the connection.
- Perform malware analysis on suspicious binaries.

### Real-world example
- A compromised host runs a web shell and listens on an unexpected port, allowing remote access.

### Interview Q&A
- Q: "How do you find listening TCP ports on Linux?"
  A: "Use `ss -tuln` or `netstat -tuln` to list listening TCP/UDP sockets."
- Q: "Why use `ss` instead of `netstat`?"
  A: "`ss` is faster and provides richer filtering for modern Linux kernels."

### Practical lab exercises
- Examine active sockets with `ss -tunap`.
- Identify the process ID for a suspicious listener.
- Compare `ss` and `netstat` output on the same host.

### TryHackMe / Hack The Box practice suggestions
- TryHackMe: `Linux Networking`, `Threat Hunting`.
- HTB: boxes where network service discovery is part of the challenge.

### Important tools used
- `ss`, `netstat`, `lsof -i`, `nmap`, `tcpdump`, `ps`.

### Key commands
- `ss -tuln`
- `ss -tunap`
- `netstat -tuln`
- `lsof -i -P -n`

### Summary
- `netstat` and `ss` are vital for discovering network activity and identifying suspicious sockets during investigations. `ss` is the preferred modern tool.
