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

# Cracking Hashes from /etc/shadow
The /etc/shadow file is the file on Linux machines where password hashes are stored. It also stores other information, such as the date of last password change and password expiration information.
It contains one entry per line for each user or user account of the system. This file is usually only accessible by the root user, so you must have sufficient privileges to access the hashes.
However, if you do, there is a chance that you will be able to crack some of the hashes.

## Unshadowing
John can be very particular about the formats it needs data in to be able to work with it; for this reason, to crack **/etc/shadow** passwords,
you must combine it with the **/etc/passwd** file for John to understand the data it’s being given. To do this, we use a tool built into the John suite of tools called unshadow. The basic syntax of unshadow is as follows:

_unshadow [path to passwd] [path to shadow]_

- unshadow: Invokes the unshadow tool
- [path to passwd]: The file that contains the copy of the /etc/passwd file you’ve taken from the target machine
- [path to shadow]: The file that contains the copy of the /etc/shadow file you’ve taken from the target machine

### Example Usage:

unshadow local_passwd local_shadow > unshadowed.txt

### Note on the files

When using unshadow, you can either use the entire /etc/passwd and /etc/shadow files, assuming you have them available, or you can use the relevant line from each, for example:

**FILE 1 - local_passw**d

Contains the /etc/passwd line for the root user:

root:x:0:0::/root:/bin/bash

**FILE 2 - local_shadow**

Contains the /etc/shadow line for the root user: root:$6$2nwjN454g.dv4HN/$m9Z/r2xVfweYVkrr.v5Ft8Ws3/YYksfNwq96UL1FX0OJjY1L6l.DS3KEVsZ9rOVLB/ldTeEL/OIhJZ4GMFMGA0:18576::::::

## Cracking

We can then feed the output from unshadow, in our example use case called unshadowed.txt, directly into John. We should not need to specify a mode here as we have made the input specifically for John; however, in some cases, you will need to specify the format as we have done previously using: --format=sha512crypt

_john --wordlist=/usr/share/wordlists/rockyou.txt --format=sha512crypt unshadowed.txt_\

# Using Single Crack Mode
To use single crack mode, we use roughly the same syntax that we’ve used so far; for example, if we wanted to crack the password of the user named “Mike”, using the single mode, we’d use:

_john --single --format=[format] [path to file]_

--single: This flag lets John know you want to use the single hash-cracking mode

--format=[format]: As always, it is vital to identify the proper format.

### Example Usage:

_john --single --format=raw-sha256 hashes.txt_

A Note on File Formats in Single Crack Mode:

If you’re cracking hashes in single crack mode, you need to change the file format that you’re feeding John for it to understand what data to create a wordlist from.
You do this by prepending the hash with the username that the hash belongs to, so according to the above example, we would change the file hashes.txt

_From 1efee03cdcb96d90ad48ccc7b8666033_

_To mike:1efee03cdcb96d90ad48ccc7b8666033_

# Zip2John
Similarly to the unshadow tool we used previously, we will use the zip2john tool to convert the Zip file into a hash format that John can understand and hopefully crack. The primary usage is like this:

_zip2john [options] [zip file] > [output file]_

- [options]: Allows you to pass specific checksum options to zip2john; this shouldn’t often be necessary
- [zip file]: The path to the Zip file you wish to get the hash of
- >: This redirects the output from this command to another file
- [output file]: This is the file that will store the output

## Example Usage

_zip2john zipfile.zip > zip_hash.txt_

# Cracking
We’re then able to take the file we output from zip2john in our example use case, zip_hash.txt, and, as we did with unshadow, feed it directly into John as we have made the input specifically for it.

_john --wordlist=/usr/share/wordlists/rockyou.txt zip_hash.txt_

# Rar2John
Almost identical to the zip2john tool, we will use the rar2john tool to convert the RAR file into a hash format that John can understand. The basic syntax is as follows:

_rar2john [rar file] > [output file]_

- rar2john: Invokes the rar2john tool
- [rar file]: The path to the RAR file you wish to get the hash of
- >: This redirects the output of this command to another file
- [output file]: This is the file that will store the output from the command

## Example Usage

_/opt/john/rar2john rarfile.rar > rar_hash.txt_

# Cracking
Once again, we can take the file we output from rar2john in our example use case, rar_hash.txt, and feed it directly into John as we did with zip2john.

_john --wordlist=/usr/share/wordlists/rockyou.txt rar_hash.txt_
