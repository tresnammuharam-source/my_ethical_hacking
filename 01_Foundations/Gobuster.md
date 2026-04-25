# GOBUSTER

Gobuster is an open-source offensive tool written in Golang. It enumerates web directories, DNS subdomains, vhosts, Amazon S3 buckets, and Google Cloud Storage by brute force,
using specific wordlists and handling the incoming responses. Many security professionals use this tool for penetration testing, bug bounty hunting, and cyber security assessments.
Looking at the phases of ethical hacking, we can place Gobuster between the reconnaissance and scanning phases.

Before exploring Gobuster, let’s briefly discuss the concepts of enumeration and Brute Force.

## Enumeration

Enumeration is the act of listing all the available resources, whether they are accessible or not. For example, Gobuster enumerates web directories.

## Brute Force

Brute force is the act of trying every possibility until a match is found. It is like having ten keys and trying them all on a lock until one fits. Gobuster uses wordlists for this purpose.

## Gobuster: Overview
Gobuster is included by default in distributions like Kali Linux. Let’s start by looking at Gobuster’s help page. This help page gives us a good overview of its functionalities and options.

Enter the following command: `gobuster --help`. You should get the help page for the Gobuster tool as shown below:
```
 gobuster [command]

Available Commands:
  completion  Generate the autocompletion script for the specified shell
  dir         Uses directory/file enumeration mode
  dns         Uses DNS subdomain enumeration mode
  fuzz        Uses fuzzing mode. Replaces the keyword FUZZ in the URL, Headers and the request body
  gcs         Uses gcs bucket enumeration mode
  help        Help about any command
  s3          Uses aws bucket enumeration mode
  tftp        Uses TFTP enumeration mode
  version     shows the current version
  vhost       Uses VHOST enumeration mode (you most probably want to use the IP address as the URL parameter)

Flags:
      --debug                 Enable debug output
      --delay duration        Time each thread waits between requests (e.g. 1500ms)
  -h, --help                  help for gobuster
      --no-color              Disable color output
      --no-error              Don't display errors
  -z, --no-progress           Don't display progress
  -o, --output string         Output file to write results to (defaults to stdout)
  -p, --pattern string        File containing replacement patterns
  -q, --quiet                 Don't print the banner and other noise
  -t, --threads int           Number of concurrent threads (default 10)
  -v, --verbose               Verbose output (errors)
  -w, --wordlist string       Path to the wordlist. Set to - to use STDIN.
      --wordlist-offset int   Resume from a given position in the wordlist (defaults to 0)

Use "gobuster [command] --help" for more information about a command.
```
The help page contains multiple sections:

Usage: Shows the syntax on how to use the command.
Available Commands: Multiple commands are available to aid us in enumerating directories, files, DNS subdomains, Google Cloud Storage buckets, and Amazon AWS S3 buckets.
Throughout this room, we will focus on the dir, dns, and vhost commands. We will cover each of them in the following tasks.
Flags: These are specific options we can configure to customize our commands. Let’s look at the flags we will often use throughout this room:

<img width="1198" height="542" alt="image" src="https://github.com/user-attachments/assets/efcc508e-00e0-4a80-8b44-3dc7556adfea" />

## Example
Let us look at an example of how we would use these commands and flags together to enumerate a web directory:

`gobuster dir -u "http://www.example.thm/" -w /usr/share/wordlists/dirb/small.txt -t 64`

- `gobuster dir` indicates that we will use the directory and file enumeration mode.
- `-u "http://www.example.thm/"` tells Gobuster that the target URL is http://example.thm/(opens in new tab).
- `-w /usr/share/wordlists/dirb/small.txt` directs Gobuster to use the small.txt wordlist to brute force the web directories.
Gobuster will use each entry in the wordlist to form a new URL and send a GET request to that URL. If the first entry of the wordlist were images,
Gobuster would send a GET request to http://example.thm/images/.(opens in new tab)
- `-t 64` sets the number of threads Gobuster will use to 64. This improves the performance drastically.

## Hand-on

Important: We work in a local network with a DNS server on the web server. To ensure we can resolve the domains used throughout this room, you need to change the `/etc/resolv-dnsmasq` file:

- Open up a terminal on the the AttackBox and enter the command: `sudo nano /etc/resolv-dnsmasq`.
- Insert `nameserver 10.49.178.232` as the first line.
- Save the file by pressing CTRL+O, followed by pressing ENTER, and then exit the editor by pressing CTRL+X.
- Enter the command `/etc/init.d/dnsmasq restart` to restart the Dnsmasq service.
The file should look something like this:
```
root@tryhackme:~# cat /etc/resolv-dnsmasq 
nameserver 10.49.178.232
nameserver 169.254.169.253
```
- If error for after restart you mush check terminal DNS with command: `sudo systemctl status dnsmasq.servvice -l`. check port number error.
- if port already in use, now you check who is used the port number with command: `sudo lsof -i :53` if port 53 already in use
- and disconnect the port number who not used with command: `sudo systemctl disable systemd-resolved` and `sudo rm /etc/resolv.conf` and make `echo "nameserver 8.8.8.8" | sudo tee /etc/resolv.conf`
- and restart with `/etc/init.d/dnsmasq restart`

---
# ENUMERATION DIRECTORY

Gobuster has a `dir` mode, allowing users to enumerate website directories and their files. This mode is useful when you are performing a penetration test and would like to see what the directory structure of a website is and what files it contains. Often, directory structures of websites and web apps follow a particular convention, making them susceptible to Brute Force using wordlists. For example, the  directory structure on the web server hosting WordPress looks something  like this:
```
root@tryhackme:~# tree -L 3 -d
.
└── html
    └── wordpress
        ├── wp-admin
        ├── wp-content
        └── wp-includes
```

Gobuster is powerful because it allows you to scan the website and return the status codes. These status codes immediately tell you if you, as an outside user, can request that directory or not.

## Help
If you want a complete overview of what the Gobuster dir command can offer, you can look at the help page. Seeing the extensive help page for the dir command can somewhat be intimidating. So, we will focus on the most essential flags in this room. Type the following command to display the help: gobuster dir --help.

Many flags are used to fine-tune the gobuster dir command. It is out of scope to go over each one of them, but in the table below, we have listed the flags that cover most of the scenarios:

<img width="1240" height="798" alt="image" src="https://github.com/user-attachments/assets/c27a1abf-879a-485e-a221-d5fcf5822b8e" />

## How To Use dir Mode
To run Gobuster in `dir` mode, use the following command format:

`gobuster dir -u "http://www.example.thm" -w /path/to/wordlist`

Notice that the command also includes the flags `-u` and `-w`, in addition to the dir keyword. These two flags are required for the Gobuster directory enumeration to work. Let us look at a practical example of how to enumerate directories and files with Gobuster dir mode:

`gobuster dir -u "http://www.example.thm" -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -r`

This command scans all the directories located at _www.example.thm_ using the wordlist _directory-list-2.3-medium.txt_. Let’s look a bit closer at each part of the command:

- gobuster dir: Configures Gobuster to use the directory and file enumeration mode.
- -u http://www.example.thm:
  - The URL will be the base path where Gobuster starts looking. So, the URL  above is using the root web directory. For example, in a typical Apache installation on Linux, this is `/var/www/html`. So if you have a “resources” directory and you want to enumerate that directory, you’d set the URL as `http://www.example.thm/resources`. You can also think of this like `http://www.example.thm/path/to/folder`.
  - The URL must contain the protocol used, in this case, HTTP. This is important and required. If you pass the wrong protocol, the scan will fail.
  - In the host part of the URL, you can either fill in the IP or the HOSTNAME. However, it is important to mention that when using the IP, you may target a different website than intended. A web server can host multiple websites using one IP (this technique is also called virtual hosting). Use the HOSTNAME if you want to be sure.
  - Gobuster does not enumerate recursively. So, if the results show a directory path you are interested in, you will have to enumerate that specific directory.
- `-w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt` configures Gobuster to use the directory-list-2.3-medium.txt wordlist to enumerate. Each entry of the wordlist is appended to the configured URL.
- `-r` configures Gobuster to follow the redirect responses received from the sent requests. If a status code 301 was received, Gobuster will navigate to the redirect URL that is included in the response.

Let’s look at a second example where we use the `-x` flag to specify what type of files we want to enumerate:

`gobuster dir -u "http://www.example.thm" -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x .php,.js`

This command will look for directories located at _http://example.thm_ (opens in new tab) using the wordlist directory-list-2.3-medium.txt. In addition to directory listing, this command also lists all the files that have a .php or .js extension.

---
# ENUMERATION SUBDOMAIN

subdomain is same server but have domain linked to main-domain.


