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

# John Basic Syntax
The basic syntax of John the Ripper commands is as follows. We will cover the specific options and modifiers used as we use them.

_john [options] [file path]_

- john: Invokes the John the Ripper program
- [options]: Specifies the options you want to use
- [file path]: The file containing the hash you’re trying to crack; if it’s in the same directory, you won’t need to name a path, just the file.

# Automatic Cracking

John has built-in features to detect what type of hash it’s being given and to select appropriate rules and formats to crack it for you; this isn’t always the best idea as it can be unreliable, but if you can’t identify what hash type you’re working with and want to try cracking it, it can be a good option! To do this, we use the following syntax:

_john --wordlist=[path to wordlist] [path to file]_

--wordlist=: Specifies using wordlist mode, reading from the file that you supply in the provided path

[path to wordlist]: The path to the wordlist you’re using, as described in the previous task

Example Usage:

_john --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt_

# Format-Specific Cracking

Once you have identified the hash that you’re dealing with, you can tell John to use it while cracking the provided hash using the following syntax:

_john --format=[format] --wordlist=[path to wordlist] [path to file]_

--format=: This is the flag to tell John that you’re giving it a hash of a specific format and to use the following format to crack it

[format]: The format that the hash is in

Example Usage:

_john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt_

### A Note on Formats:

When you tell John to use formats, if you’re dealing with a standard hash type, e.g. md5 as in the example above, you have to prefix it with raw- to tell John you’re just dealing with a standard hash type, though this doesn’t always apply. To check if you need to add the prefix or not, you can list all of John’s formats using john --list=formats and either check manually or grep for your hash type using something like _john --list=formats | grep -iF "md5"_
