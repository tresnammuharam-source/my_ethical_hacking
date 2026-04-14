# Daftar Tools untuk diperdalam dan Praktik


## NMAP
The undisputed king of network scanning. It discovers active devices, open ports, and running services across any network. This is your essential first step for mapping a target.

Top 10 Commands:

1. nmap -A -T4 [Target_IP] (Aggressive scan: OS, Service, Script detection)
2. nmap -sS -Pn [Target_IP] (Stealth SYN scan to bypass firewalls)
3. nmap -sU [Target_IP] (UDP port scan for common services)
4. nmap -p- [Target_IP] (Scan all 65535 ports on a target)
5. nmap --script vuln [Target_IP] (Check for known vulnerabilities)
6. nmap -sn 192.168.1.0/24 (Ping sweep to find live hosts)
7. nmap -O [Target_IP] (OS detection for target system)
8. nmap -iL targets.txt (Scan multiple targets from a list)
9. nmap -oA output [Target_IP] (Save all output formats)
10. nmap --traceroute [Target_IP] (Show the network path to the target)

## HASHCAT
The world's fastest password recovery tool, leveraging GPU power for incredible cracking speeds. It supports a vast array of hash types and attack modes, making it indispensable for offline password auditing.
No hash is safe when Hashcat is unleashed.

Top 10 Commands:

1. hashcat -m 0 hash.txt wordlist.txt (Crack MD5 hashes with a wordlist)
2. hashcat -m 1000 hash.txt wordlist.txt (Crack NTLM (Windows) hashes)
3. hashcat -a 3 hash.txt ?I?I?I?I (Brute-force 4-character lowercase passwords)
4. hashcat -I (Display information about your GPU devices)
5. hashcat -b (Benchmark your system's cracking speed)
6. hashcat --show hash.txt (Display successfully cracked passwords)
7. hashcat -m 2500 wpa.hccapx wordlist.txt (Crack WPA/WPA2 handshakes)
8. hashcat -a 1 hash.txt list1.txt list2.txt (Perform a combination attack)
9. hashcat -m 1800 hash.txt wordlist.txt (Crack SHA512 (Linux) hashes)
10. hashcat --session mysession --status (Check cracking status of a session)

