# Practice Day — Solutions

## 1. Explore Kali

### Simple definition
- Exploring Kali means learning the environment, tool categories, and the default security distribution layout.

### Why it matters in cybersecurity
- Familiarity with Kali helps analysts and pentesters quickly locate the right tools and avoid mistakes in high-pressure situations.

### How it works step-by-step
1. Open the Kali applications menu.
2. Review categories such as Information Gathering, Vulnerability Analysis, and Exploitation.
3. Inspect the options available in each tool group.
4. Read man pages or help output for tools you don’t know.

### Common attack methods
- Attackers use Kali to perform reconnaissance, scanning, exploitation, and post-exploitation.
- The environment itself is not malicious, but the tools can support offensive techniques.

### IOCs
- Unexpected tool use on production systems.
- Execution of known Kali binaries outside authorized lab networks.

### Logs/events to monitor
- Host command audit logs.
- Proxy/network logs for scan and exploit traffic.

### SIEM detection techniques
- Detect unusual execution of Kali tools from non-lab hosts.
- Alert on internal scanning or reconnaissance patterns.

### Prevention and mitigation
- Keep offensive tools confined to isolated lab networks.
- Use role-based access control to limit tool usage.

### Incident response actions
- Determine whether tool use is authorized.
- Isolate and investigate hosts using Kali in unauthorized environments.

### Real-world example
- A contractor uses Kali on a corporate network without authorization, triggering an internal security investigation.

### Interview Q&A
- Q: "Why is it important to know Kali tool categories?"
  A: "So you can choose the right tool for each stage of testing and recognize suspicious activity."
- Q: "How do you avoid using tools unsafely?"
  A: "By practicing in lab environments and reading help output before running commands."

### Practical lab exercises
- Launch Kali and note the categories.
- Open tool documentation for one item in each category.

### TryHackMe / HTB suggestions
- TryHackMe: `Kali Linux` learning path.
- HTB: use Kali in early boxes as your primary distro.

### Important tools used
- `Katool`, Kali menu, `man`, `whatis`, `apropos`.

### Key commands
- `man nmap`
- `apropos scan`
- `which msfconsole`

### Summary
- Exploring Kali builds the foundation for safe and effective use of security tools.

## 2. Practice Commands

### Simple definition
- Practicing commands means repeatedly using core Linux and security commands until they become second nature.

### Why it matters in cybersecurity
- Command fluency reduces mistakes and speeds up investigations.
- Analysts need to execute commands confidently during incident response.

### How it works step-by-step
1. Identify a command to practice.
2. Run it in a safe lab environment.
3. Review output and understand the meaning.
4. Repeat across variations and scenarios.

### Common attack methods
- Command history can reveal attacker activity.
- Malicious users may abuse legitimate commands like `curl` or `wget`.

### IOCs
- Unusual or suspicious command lines.
- Newly created scripts or binaries executed from unexpected locations.

### Logs/events to monitor
- Shell histories and process execution logs.
- EDR alerts for suspicious command strings.

### SIEM detection techniques
- Detect abnormal command usage patterns.
- Correlate commands with other suspicious activity.

### Prevention and mitigation
- Enforce command logging and auditing on endpoints.
- Use secure shell access and limit shell privileges.

### Incident response actions
- Capture shell history from affected hosts.
- Validate commands against known baselines.

### Real-world example
- Attackers use `nmap` and `find` to enumerate systems and search for credentials.

### Interview Q&A
- Q: "What command would you use to view active processes?"
  A: "`ps aux`, `top`, or `htop`."
- Q: "How do you verify a command before running it?"
  A: "I use `--help`, man pages, and test in a sandbox first."

### Practical lab exercises
- Practice `ls`, `cd`, `man`, `ip a`, `ping`, `nmap -sV`, `ss -tuln`.
- Document what each command reveals.

### TryHackMe / HTB suggestions
- TryHackMe: `Bash Scripting`, `Linux Fundamentals`.
- HTB: beginner boxes where Linux command skills are required.

### Important tools used
- `bash`, `man`, `nmap`, `ss`, `ip`, `ping`, `cat`, `grep`.

### Key commands
- `ip a`
- `ping -c 4 8.8.8.8`
- `nmap -sV <target>`
- `ss -tuln`

### Summary
- Repeated practice with core commands is essential for analysts. Strong command skills improve troubleshooting and response speed.

## 3. Solve Basic Labs

### Simple definition
- Solving basic labs means working through guided cybersecurity challenges to gain practical experience.

### Why it matters in cybersecurity
- Labs provide real-world scenarios for learning detection, exploitation, and response techniques.
- They build muscle memory for SOC workflows.

### How it works step-by-step
1. Choose a lab or challenge.
2. Read the objective and scope.
3. Perform reconnaissance and analysis.
4. Document findings and complete the lab tasks.

### Common attack methods
- Labs often simulate scanning, exploitation, privilege escalation, and data exfiltration.

### IOCs
- The lab environment itself may generate simulated IOCs like suspicious connections.

### Logs/events to monitor
- Lab server logs, application logs, and network captures.
- Tool output during each exercise.

### SIEM detection techniques
- Practice creating detection rules based on lab-generated events.
- Validate alert logic against known lab behaviors.

### Prevention and mitigation
- Follow lab rules and isolate lab traffic from production.
- Use snapshots to restore environments after mistakes.

### Incident response actions
- Document each step and evidence.
- Practice reporting findings with clear timelines.

### Real-world example
- Many SOC analysts start with CTF-style labs before moving into live environments.

### Interview Q&A
- Q: "How do labs help you prepare for security operations?"
  A: "They let me practice detection, analysis, and response in a controlled setting."

### Practical lab exercises
- Complete basic TryHackMe rooms on networking, Linux, and detection.
- Solve simple HTB machines focused on enumeration.

### TryHackMe / HTB suggestions
- TryHackMe: `Intro to Offensive Security`, `Blue Team Fundamentals`.
- HTB: beginner-friendly boxes like `Legacy` or `Blue`. 

### Important tools used
- `nmap`, `tcpdump`, `Wireshark`, `burpsuite`, `metasploit`, `bash`.

### Key commands
- `nmap -A <target>`
- `tcpdump -i eth0 port 80`
- `curl http://<target>`

### Summary
- Basic labs build practical experience and confidence for SOC analysts and interview preparation.

## 4. Document Learning

### Simple definition
- Documenting learning means recording observations, commands, and lessons from each exercise.

### Why it matters in cybersecurity
- Good documentation preserves knowledge and supports handoffs during investigations.
- Analysts need clear notes for reports and evidence.

### How it works step-by-step
1. Note the objective and environment.
2. Record commands and outputs.
3. Summarize findings and lessons learned.
4. Save notes in a structured format.

### Common attack methods
- Poor documentation can hide attacker activity and slow response.

### IOCs
- Missing or inconsistent incident notes.
- Gaps in the timeline of events.

### Logs/events to monitor
- Documented evidence from tools and host logs.
- Lab completion notes and work product.

### SIEM detection techniques
- Not directly applicable, but analysts should capture event IDs and timestamps.

### Prevention and mitigation
- Use templates for incident notes and lab reports.
- Keep notes organized by date and topic.

### Incident response actions
- Maintain an investigation journal for each incident.
- Record every action, tool, and result.

### Real-world example
- Analysts who document clearly can accelerate remediation and provide stronger evidence.

### Interview Q&A
- Q: "How do you keep track of your investigations?"
  A: "I use structured notes, capture commands and outputs, and summarize key findings."

### Practical lab exercises
- Create a Markdown lab report for each challenge.
- Include goal, commands, results, and conclusions.

### TryHackMe / HTB suggestions
- Practice writing notes for every room or box you complete.

### Important tools used
- `Markdown`, `OneNote`, `Notion`, `Obsidian`, `Jupyter Notebook`.

### Key commands
- `mkdir -p ~/notes && cd ~/notes`
- `code lab-notes.md` or `nano lab-notes.md`

### Summary
- Documenting learning is a force multiplier. Good notes make practice, reporting, and incident response more effective.
