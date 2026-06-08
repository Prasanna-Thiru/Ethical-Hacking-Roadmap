# Networking Basics — Solutions

1. OSI Model

- Seven layers: Physical, Data Link, Network, Transport, Session, Presentation, Application. Each layer provides services to the layer above and uses services from the layer below. Example: IP operates at Network, TCP at Transport, HTTP at Application.

2. TCP/IP Model

- Four layers: Link (Network Interface), Internet, Transport, Application. Map roughly to OSI: Link→(Physical+Data Link), Internet→Network, Transport→Transport, Application→(Session+Presentation+Application).

3. Ports and Protocols

- Ports identify services on a host. Common port numbers: 22 (SSH), 53 (DNS), 80 (HTTP), 443 (HTTPS), 25 (SMTP). TCP is connection-oriented and reliable; UDP is connectionless and lower-overhead.

4. Common Services

- Web (HTTP/HTTPS) — web servers and browsers.
- SSH (22) — secure remote shell.
- DNS (53) — domain name resolution.
- SMTP/IMAP/POP3 — email sending and retrieval.
- FTP/SFTP — file transfer (SFTP over SSH is preferred).

Tip: memorize the most-used ports and practice identifying services with `ss`, `netstat`, or `nmap -sV`.
