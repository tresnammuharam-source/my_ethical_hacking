# John The Ripper

## Learning Objectives
Upon the completion of this room, you learn about using John for:

- Cracking Windows authentication hashes
- Crack /etc/shadow hashes
- Cracking password-protected Zip files
- Cracking password-protected RAR files
- Cracking SSH keys

## Installation
John the Ripper is supported on many Operating Systems, not just Linux Distributions.
Before we go through this, there are multiple versions of John, the standard “core” distribution, and multiple community editions, which extend the feature set of the original John distribution.
The most popular of these distributions is the “Jumbo John,” which we will use specific features of later.

### AttackBox and Kali

Jumbo John is already installed on the attached virtual machine and on the AttackBox, so if you plan to use either one, you need not take any further action.
Furthermore, offensive Linux distributions like Kali are shipped with Jumbo John installed.

You can double-check this by typing john into the terminal. You should be met with a usage guide for John, with the first line reading “John the Ripper 1.9.0-jumbo-1” or something similar with a different version number.
Other Linux Distributions

Many Linux distributions have John the Ripper available for installation from their official repositories.
For instance, on Fedora Linux, you can install John the Ripper with sudo dnf install john, while on Ubuntu, you can install it with sudo apt install john.
Unfortunately, at the time of writing, these versions provided core functionality and missed some of the tools available through Jumbo John.

Consequently, you need to consider building from the source to access all the tools available via Jumbo John.
The official installation guide(opens in new tab) provides detailed installation and build configuration instructions.

### Installing on Windows

To install Jumbo John the Ripper on Windows, you need to download and install the zipped binary for either 64-bit systems here(opens in new tab) or for 32-bit systems here(opens in new tab).

## Wordlists
Now that we have john ready, we must consider another indispensable component: wordlists.

As we mentioned earlier, to use a dictionary attack against hashes, you need a list of words to hash and compare; unsurprisingly, this is called a wordlist.
There are many different wordlists out there, and a good collection can be found in the SecLists(opens in new tab) repository. There are a few places you can look for wordlists for attacking the system of choice;
we will quickly run through where you can find them.

On the AttackBox and Kali Linux distributions, the /usr/share/wordlists directory contains a series of great wordlists.

RockYou

For all of the tasks in this room, we will use the infamous rockyou.txt wordlist, a very large common password wordlist obtained from a data breach on a website called rockyou.com in 2009.
If you are not using any of the above distributions, you can get the rockyou.txt wordlist from the SecLists(opens in new tab) repository under the /Passwords/Leaked-Databases subsection.
You may need to extract it from the .tar.gz format using tar xvzf rockyou.txt.tar.gz.

