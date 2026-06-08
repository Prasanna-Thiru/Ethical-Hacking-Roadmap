# Kali Linux Basics — Solutions

## 1. Kali Overview

### Simple definition
- Kali Linux is a Debian-based Linux distribution built for penetration testing, red teaming, and cybersecurity assessments.
- It includes hundreds of preinstalled security tools for network scanning, exploitation, password auditing, and forensics.

### Why it matters in cybersecurity
- Kali is widely used by security professionals for learning and controlled offensive testing.
- Defenders should recognize Kali indicators and understand the tools it contains.

### How it works step-by-step
1. Boot Kali from a disk, USB, or virtual machine.
2. Use the Applications menu to access tool categories.
3. Run tools from the terminal or GUI.
4. Review results and apply findings in a controlled lab.

### Common attack methods related to Kali tools
- Reconnaissance using `nmap`.
- Web application attacks using `burpsuite` or `sqlmap`.
- Password cracking with `john` and `hashcat`.
- Exploitation using `Metasploit`.

### IOCs
- Presence of Kali tool binaries on a host.
- Shell history showing commands like `nmap`, `msfconsole`, or `hydra`.
- Traffic patterns consistent with vulnerability scanning.

### Logs and events a SOC analyst should monitor
- Endpoint execution logs for Kali commands.
- Network logs for reconnaissance and exploit traffic.
- Authentication logs on lab and production systems.

### Detection techniques using SIEM tools
- Alert on the execution of Kali tool names and known pentest commands.
- Correlate host process activity with scan-like network traffic.
- Tag lab infrastructure to reduce false positives.

### Prevention and mitigation methods
- Restrict use of Kali to approved lab environments.
- Use application whitelisting and endpoint protections.
- Separate lab networks from production.

### Incident response actions
- Confirm whether Kali use is authorized.
- Isolate any unauthorized host.
- Review the scope of the activity and remediate impacted systems.

### Real-world example
- A user installs Kali on a corporate laptop and inadvertently scans the production network, triggering security alerts.

### Common interview questions and answers
- Q: "What is Kali Linux used for?"
  A: "For penetration testing, vulnerability research, and cybersecurity training."
- Q: "How does Kali differ from general-purpose Linux distros?"
  A: "It comes preloaded with security tools and is optimized for offensive security work."

### Practical lab exercises
- Boot Kali in a VM and explore the default tool categories.
- Open and inspect the tools in Information Gathering and Vulnerability Analysis.

### TryHackMe / Hack The Box practice suggestions
- TryHackMe: `Kali Linux`, `Tools`. 
- HTB: use Kali as the attack machine in beginner rooms.

### Important tools used
- `nmap`, `Metasploit`, `Burp Suite`, `John the Ripper`, `hydra`, `Wireshark`.

### Key commands
- `which nmap`
- `ls /usr/share/tools` (or browse the menu)
- `man nmap`

### Summary
- Kali Linux is a specialized distro for security testing. SOC analysts should know its capabilities and how to detect its use in an environment.

## 2. Install Kali Linux

### Simple definition
- Installing Kali Linux means setting up the distribution on hardware or a virtual machine for security practice.

### Why it matters in cybersecurity
- A proper install ensures a stable and safe environment for testing offensive tools.
- Analysts learn how attacker tooling environments are configured.

### How it works step-by-step
1. Download the official Kali ISO from the trusted website.
2. Create bootable media using Rufus, BalenaEtcher, or a VM image.
3. Boot the installer and follow prompts.
4. Choose installation type: full, dual-boot, or VM.
5. Configure username, password, networking, and disk partitions.
6. Complete setup and reboot.

### Common risks and mistakes
- Installing on production hardware or without isolation.
- Using unofficial or tampered ISOs.
- Leaving default credentials unchanged.

### IOCs
- New Kali VMs appearing on the network.
- Unauthorized installation activity in endpoint logs.

### Logs and events a SOC analyst should monitor
- System installation logs.
- Virtualization host logs.
- Network device logs for new MAC/IP assignments.

### Detection techniques using SIEM tools
- Alert on new VM creation from Kali templates.
- Monitor for unusual installation-related processes.

### Prevention and mitigation methods
- Use isolated lab infrastructure and secure download sources.
- Document and approve all Kali installations.

### Incident response actions
- Verify the purpose and authorization of the Kali install.
- Remove unauthorized Kali VMs from production networks.

### Real-world example
- A student installs Kali on a shared workstation and triggers SOC alerts in a corporate lab.

### Interview Q&A
- Q: "What is the safest way to install Kali?"
  A: "In a virtual machine with host-only or isolated networking."
- Q: "Why avoid dual-booting Kali on production machines?"
  A: "It risks mixing offensive tools with production data and can cause accidental exposure."

### Practical lab exercises
- Build a Kali VM in VirtualBox or VMware.
- Verify the install by launching a security tool.

### TryHackMe / Hack The Box practice suggestions
- TryHackMe: `Virtual Machine Setup`, `Kali Linux`.

### Important tools used
- VirtualBox, VMware, Rufus, BalenaEtcher, Kali ISO.

### Key commands
- `VBoxManage createvm --name Kali --register`
- `virsh define kali.xml`

### Summary
- Installing Kali safely is foundational for secure security training.

## 3. Update & Upgrade

### Simple definition
- Updating and upgrading keeps Kali Linux and its tools current with security patches and new releases.

### Why it matters in cybersecurity
- Outdated security tools or OS packages can be insecure and unreliable.
- Analysts need current toolsets to accurately assess vulnerabilities.

### How it works step-by-step
1. Run `sudo apt update` to refresh package lists.
2. Run `sudo apt upgrade -y` to upgrade installed packages.
3. Optionally run `sudo apt dist-upgrade -y` for distribution-level changes.
4. Reboot if kernel or critical packages are updated.

### Common attack methods related to outdated tools
- Exploiting known vulnerabilities in old tool versions.
- Supply-chain attacks on package repositories.

### IOCs
- Use of outdated packages and tools.
- Unexpected package installation or repository changes.

### Logs and events a SOC analyst should monitor
- `/var/log/apt/history.log`
- System update task logs.
- Audit logs for package management commands.

### Detection techniques using SIEM tools
- Alert on package management activity and unauthorized repository changes.
- Correlate update events with system changes.

### Prevention and mitigation methods
- Use official repositories and signed packages.
- Schedule updates during maintenance windows.

### Incident response actions
- Verify the integrity of updated packages.
- Roll back or restore if malicious packages were installed.

### Real-world example
- A security analyst installs a tool version with a known backdoor because the environment was not updated from official repos.

### Interview Q&A
- Q: "What command updates Kali package lists?"
  A: "`sudo apt update`"
- Q: "What is the difference between `upgrade` and `dist-upgrade`?"
  A: "`upgrade` updates existing packages, while `dist-upgrade` may install or remove packages to satisfy dependencies."

### Practical lab exercises
- Run a full update cycle on a Kali VM.
- Review the `apt` history log for the changes.

### TryHackMe / Hack The Box practice suggestions
- TryHackMe: `Linux Package Management`, `Kali Linux`.

### Important tools used
- `apt`, `dpkg`, `apt-cache`, `apt-key`.

### Key commands
- `sudo apt update`
- `sudo apt upgrade -y`
- `sudo apt dist-upgrade -y`
- `cat /var/log/apt/history.log`

### Summary
- Regular updates are crucial for a secure and dependable Kali environment.

## 4. Basic Commands

### Simple definition
- Basic Linux commands are the essential operations for navigating and managing the system.

### Why it matters in cybersecurity
- SOC analysts and pentesters rely on these commands every day for investigation, data collection, and tool usage.

### How it works step-by-step
1. Navigate the filesystem with `pwd`, `cd`, and `ls`.
2. Manage files using `cp`, `mv`, `rm`.
3. Install and inspect packages with `apt`.
4. Use `man` to learn command syntax.

### Common attack methods related to command usage
- Attackers may use legitimate commands to evade detection.
- Malicious scripts often rely on standard utilities.

### IOCs
- Unusual command execution patterns in shell history.
- Commands run from unexpected locations or by unauthorized users.

### Logs and events a SOC analyst should monitor
- Shell histories and process execution logs.
- EDR/endpoint command-line audit data.

### Detection techniques using SIEM tools
- Alert on suspicious uses of file copy, network download, and shell commands.
- Correlate command activity with data access events.

### Prevention and mitigation methods
- Enable command auditing and restrict shell access.
- Use role-based access and least privilege.

### Incident response actions
- Collect shell history and command execution evidence.
- Reconstruct attacker activity using command logs.

### Real-world example
- A threat actor uses `wget` and `chmod` to deploy a reverse shell script.

### Interview Q&A
- Q: "How do you view the current directory in Linux?"
  A: "Use `pwd`."
- Q: "What command shows the manual page for `ls`?"
  A: "`man ls`."

### Practical lab exercises
- Practice basic navigation and file management commands.
- Use `man` to explore options for at least three commands.

### TryHackMe / Hack The Box practice suggestions
- TryHackMe: `Linux Fundamentals`, `Command Line Basics`.
- HTB: early boxes that require Linux command usage.

### Important tools used
- `pwd`, `ls`, `cd`, `cp`, `mv`, `rm`, `apt`, `man`.

### Key commands
- `pwd`
- `ls -la`
- `cd /etc`
- `cp file1.txt file2.txt`
- `mv oldname newname`
- `rm file.txt`
- `sudo apt install <package>`
- `man ls`

### Summary
- Mastering basic Linux commands is essential for security operations and investigative work.

