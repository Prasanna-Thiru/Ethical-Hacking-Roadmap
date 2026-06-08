# Linux Networking — Solutions

# 1. IP Addressing

- IPv4 uses four octets (e.g., 192.168.1.10). The CIDR suffix (/24) or subnet mask (255.255.255.0) shows which bits are network vs host. Default gateway routes traffic to other networks. Example: 192.168.1.10/24 → network 192.168.1.0/24.

# 2. ifconfig / ip a

- `ifconfig` is older; `ip` is modern and preferred. `ip a` lists interfaces and addresses. Useful commands:

  - `ip a` — list interfaces and addresses
  - `ip link set dev eth0 up` — enable interface
  - `ip addr add 192.168.1.100/24 dev eth0` — add an IP address

# 3. ping, traceroute

- `ping` tests basic connectivity and measures RTT: `ping target`. Use `-c` to limit packets (`ping -c 4 target`).
- `traceroute` shows each hop along the route and where latency occurs: `traceroute target` or `tracepath target`.

# 4. netstat, ss

- `netstat` displays network connections and routing (legacy). `ss` is faster and recommended. Examples:

  - `ss -tuln` — show listening TCP/UDP sockets
  - `ss -s` — summary
  - `netstat -rn` — routing table (older)

Always use `sudo` when required and consult `man` pages for options.
