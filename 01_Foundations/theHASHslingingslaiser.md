# The HASH

### What is a Hash Function?
Hash functions are different from encryption. There is no key, and it’s meant to be impossible (or computationally impractical) to go from the output back to the input.

A hash function takes some input data of any size and creates a summary or digest of that data. The output has a fixed size. It’s hard to predict the output for any input and vice versa. Good hashing algorithms will be relatively fast to compute and prohibitively slow to reverse, i.e., go from the output and determine the input. Any slight change in the input data, even a single bit, should cause a significant change in the output.

Let’s check an example. In the terminal below, we can see two files; the first contains the letter T, while the second contains the letter U. If you check T and U in an ASCII table or using hexdump, you will notice that the two letters differ by a single bit.

The letter T is 54 in hexadecimal, i.e., 01010100 in binary.

The letter U is 55 in hexadecimal, i.e., 01010101 in binary.

Consequently, the following two files differ by a single bit. However, if we compare their MD5 (Message-Digest Algorithm 5) hashes, their SHA1 (Secure Hash Algorithm 1) hashes, or their SHA-256 (Secure Hash Algorithm 256) hashes, we will notice that they are entirely different

- **Rainbow Table** adalah tabel dalam mencocokan Hash yang sedang kita cari, jadi ada Hash yang sudah kita punya, terus di cocokan degan tabel rainbow yng isisnya kumpulan hash, jika hash yang kita punya sama dengan hash yang ada di tabel,
maka hash tersebut menampilkan isi dari hash yang ada dalam tabel rainbow tersebut, bisa file, kata kunci, password dll

## Link penting dalam pencairan Hash dan cracking hash :

| link | Keterangan |
| :---: | :---: |
| https://hashes.com/en/decrypt/hash | untuk mendari code hash dan identity type hash |\
| https://hashcat.net/wiki/doku.php?id=example_hashes | untuk melihat Hash-Mode dari serangkaian hash name dan contohnya |

## Linux Passwords
On Linux, password hashes are stored in /etc/shadow, which is normally only readable by root. They used to be stored in /etc/passwd, which was readable by everyone.

The shadow file contains the password information. Each line contains nine fields, separated by colons (:). The first two fields are the login name and the encrypted password. More information about the other fields can be found by executing man 5 shadow on a Linux system.

The encrypted password field contains the hashed passphrase with four components: prefix (algorithm id), options (parameters), salt, and hash. It is saved in the format $prefix$options$salt$hash. The prefix makes it easy to recognise Unix and Linux-style passwords; it specifies the hashing algorithm used to generate the hash.

Here’s a quick table of some of the most common Unix-style password prefixes you might encounter. They are listed in the order of decreasing strength. You can read more about them by checking the man page with man 5 crypt.

<img width="1247" height="542" alt="image" src="https://github.com/user-attachments/assets/8a0cef78-0222-4960-b4b7-76aa8d761e42" />

