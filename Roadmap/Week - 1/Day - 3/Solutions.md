# Linux Foundations — Solutions

## 1. File System

### Simple definition
- The Linux filesystem is a single hierarchical tree rooted at `/`.
- Directories are mounted under `/` instead of using drive letters.

### Why it matters in cybersecurity
- Understanding Linux paths helps analysts locate logs, configuration files, and hidden malware.
- Attackers often hide files in common directories, so filesystem knowledge is essential.

### How it works step-by-step
1. The root filesystem `/` contains core directories.
2. Each directory has a specific purpose, such as `/etc` for configs and `/var` for logs.
3. Devices and additional filesystems are mounted into this tree.
4. Users navigate and manage files using these directories.

### Common attack methods
- Hiding persistence scripts in `/etc/init.d`, `/usr/local/bin`, or `/tmp`.
- Placing backdoors in `/home` or web directories.
- Using cron jobs to maintain access.

### IOCs
- Unexpected files in system directories.
- Modified binaries or scripts in startup locations.
- New executable files in `/tmp` or `/var/tmp`.

### Logs and events to monitor
- File integrity monitoring on `/etc`, `/usr/bin`, and `/var/log`.
- Audit logs for file creation and modifications.
- Access to sensitive directories like `/root` or `/etc/shadow`.

### Detection techniques using SIEM tools
- Alert on creation of executable files in non-standard locations.
- Correlate unexpected file changes with process execution.

### Prevention and mitigation methods
- Harden directory permissions and use file integrity monitoring.
- Limit user write access to system directories.

### Incident response actions
- Identify suspicious files and their creation context.
- Preserve evidence and scan for related malicious activity.

### Real-world example
- A Linux server infected by a web shell hidden in `/var/www/html/uploads`.

### Interview Q&A
- Q: "What is the root directory in Linux?"
  A: "`/`, the top of the filesystem hierarchy."
- Q: "Where are logs usually stored?"
  A: "In `/var/log`."

### Practical lab exercises
- Explore the directory structure with `ls /`.
- Find system directories and understand their purposes.

### TryHackMe / Hack The Box practice suggestions
- TryHackMe: `Linux Fundamentals`, `Filesystem Navigation`.
- HTB: beginner boxes where file system enumeration is required.

### Important tools used
- `ls`, `find`, `stat`, `mount`, `df`, `du`.

### Key commands
- `ls /`
- `ls -al /etc`
- `find / -maxdepth 2 -type d`

### Summary
- Linux filesystem knowledge is foundational for both defensive and offensive security work.

## 2. Permissions

### Simple definition
- Permissions control read, write, and execute access for owner, group, and others.

### Why it matters in cybersecurity
- Incorrect permissions can allow unauthorized access or privilege escalation.
- Attackers exploit weak permissions to modify files or execute malicious code.

### How it works step-by-step
1. Each file stores permissions like `-rw-r--r--`.
2. The first set is owner rights, the second is group rights, and the third is others.
3. Special bits like SUID and SGID grant elevated execution rights.
4. Use `chmod` and `chown` to adjust permissions and ownership.

### Common attack methods
- Writable `/etc/passwd` or `/etc/shadow` files.
- SUID binaries abused for privilege escalation.
- World-writable directories used to drop malware.

### IOCs
- Files or directories with unexpected `777` permissions.
- Unknown SUID/SGID binaries.
- Permission changes on sensitive files.

### Logs and events to monitor
- File audit logs for chmod/chown operations.
- Access denied errors in logs from attempted unauthorized access.

### Detection techniques using SIEM tools
- Alert on permission changes to critical files.
- Detect unusual SUID/SGID binaries and world-writable directories.

### Prevention and mitigation methods
- Enforce least privilege and regularly audit file permissions.
- Remove unnecessary SUID/SGID settings.

### Incident response actions
- Review historical permission changes.
- Restore secure permissions and investigate how changes occurred.

### Real-world example
- A compromised web server allowed an attacker to write a shell because `/var/www/html` was world-writable.

### Interview Q&A
- Q: "What does `chmod 755` mean?"
  A: "Owner can read/write/execute; group and others can read and execute."
- Q: "How do you view file permissions?"
  A: "Use `ls -l`."

### Practical lab exercises
- Change file permissions with `chmod`.
- Identify SUID binaries with `find / -perm -4000 -type f`.

### TryHackMe / Hack The Box practice suggestions
- TryHackMe: `Linux Privilege Escalation`, `Permissions`.
- HTB: boxes that require permission misconfiguration discovery.

### Important tools used
- `ls`, `chmod`, `chown`, `find`, `getfacl`.

### Key commands
- `ls -l /etc/passwd`
- `chmod 644 file.txt`
- `chown user:group file.txt`

### Summary
- Permissions are a core defense mechanism. SOC analysts must understand and monitor them to prevent misuse.

## 3. Users & Groups

### Simple definition
- Users are accounts on a Linux system; groups are collections of users with shared permissions.

### Why it matters in cybersecurity
- User and group management controls access to systems and data.
- Misconfigured accounts are common entry points for attackers.

### How it works step-by-step
1. Users are defined in `/etc/passwd`.
2. Groups are defined in `/etc/group`.
3. Users can belong to multiple groups.
4. Group membership determines file access and privileges.

### Common attack methods
- Weak or default passwords on user accounts.
- Privilege escalation through group membership.
- Creation of hidden or unauthorized accounts.

### IOCs
- New accounts created unexpectedly.
- Accounts added to privileged groups like `sudo`.
- Login activity from unusual users.

### Logs and events to monitor
- Authentication logs (`/var/log/auth.log`, `/var/log/secure`).
- `/etc/passwd` and `/etc/group` modification events.
- sudo and su command usage.

### Detection techniques using SIEM tools
- Alert on new user creation and group membership changes.
- Monitor privilege escalation and sudo activity.

### Prevention and mitigation methods
- Enforce strong passwords and MFA where possible.
- Use least privilege and remove obsolete accounts.

### Incident response actions
- Disable suspicious accounts immediately.
- Audit account activity and group changes.

### Real-world example
- An attacker creates a backdoor user account in `/etc/passwd` to maintain access.

### Interview Q&A
- Q: "Where are Linux users stored?"
  A: "In `/etc/passwd` and password hashes in `/etc/shadow`."
- Q: "How do you add a user to a group?"
  A: "Use `usermod -aG group username`."

### Practical lab exercises
- Create a new user and assign group membership.
- Inspect `/etc/passwd` and `/etc/group`.

### TryHackMe / Hack The Box practice suggestions
- TryHackMe: `Linux User Management`, `Privilege Escalation`.

### Important tools used
- `adduser`, `useradd`, `usermod`, `passwd`, `groups`.

### Key commands
- `cat /etc/passwd`
- `cat /etc/group`
- `sudo adduser testuser`
- `sudo usermod -aG sudo testuser`

### Summary
- User and group management is fundamental for secure Linux operations and effective threat response.

## 4. File Operations

### Simple definition
- File operations are commands used to create, move, copy, and inspect files and directories.

### Why it matters in cybersecurity
- Attackers and defenders both depend on file operations. Analysts need to manipulate files safely during investigations.

### How it works step-by-step
1. Navigate directories with `cd`.
2. List contents with `ls`.
3. Create files and directories with `touch` and `mkdir`.
4. Copy, move, or delete files with `cp`, `mv`, and `rm`.
5. View file contents with `cat`, `less`, `head`, and `tail`.

### Common attack methods
- Attackers copy persistence scripts into startup directories.
- Malicious files are moved into trusted paths.
- Temporary directories are used to stage payloads.

### IOCs
- New suspicious files in `/tmp`, `/var/tmp`, or web directories.
- Deleted or moved files in sensitive locations.

### Logs and events to monitor
- File access and deletion events from audit logs.
- Process activity when files are created or modified.

### Detection techniques using SIEM tools
- Alert on file creation in unusual directories.
- Correlate file operations with suspicious process execution.

### Prevention and mitigation methods
- Monitor filesystem activity and restrict write access.
- Use immutable file flags for critical files.

### Incident response actions
- Capture a snapshot of file system state.
- Preserve suspicious files for analysis.

### Real-world example
- A threat actor drops a reverse shell script in `/tmp` and executes it.

### Interview Q&A
- Q: "How do you create an empty file?"
  A: "Use `touch filename`."
- Q: "How can you view the last 10 lines of a log file?"
  A: "Use `tail -n 10 logfile`."

### Practical lab exercises
- Create, copy, move, and delete test files.
- Use `less`, `head`, and `tail` to inspect file contents.

### TryHackMe / Hack The Box practice suggestions
- TryHackMe: `Bash Basics`, `Linux File Management`.

### Important tools used
- `touch`, `mkdir`, `cp`, `mv`, `rm`, `cat`, `less`, `head`, `tail`.

### Key commands
- `touch test.txt`
- `mkdir labdir`
- `cp test.txt labdir/`
- `mv test.txt labdir/`
- `rm labdir/test.txt`
- `less /var/log/auth.log`

### Summary
- File operations are daily essentials for Linux security work. Mastering them supports both defensive investigations and offensive testing.
