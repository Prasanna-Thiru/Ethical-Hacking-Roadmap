# Kali Tools Intro — Solutions

1. Tool Categories

- Common categories: Reconnaissance (e.g., `whois`, `theHarvester`), Scanning (e.g., `nmap`), Vulnerability analysis (e.g., `nikto`, `openvas`), Exploitation (e.g., `metasploit`), Password attacks (e.g., `hydra`, `john`), Post-exploitation, Forensics, and Reporting.

2. Klai --help

- Most command-line tools offer `--help` (or `-h`) to show usage and options. Example: `nmap --help` or `nmap -h`. Use this first to understand flags, examples, and required arguments.

3. Updating Tools

- Keep Kali tools updated with the package manager. Typical commands:

  - `sudo apt update && sudo apt full-upgrade -y` — update package lists and upgrade installed packages
  - `sudo apt install --reinstall <package>` — reinstall a broken package

4. Favourites Setup

- Create aliases and scripts for frequently used commands in `~/.bash_aliases` or `~/.bashrc`.
- Add custom tool scripts to `~/bin` and ensure it's in `PATH`.
- Use a note file (Markdown) to record favorite commands and examples for quick reference.
