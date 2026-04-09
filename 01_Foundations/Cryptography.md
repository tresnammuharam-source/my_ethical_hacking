# CRYPTOGRAPH

Have you ever wondered how to prevent third parties from reading your messages? How can your app or web browser build a secure channel with a remote server? By secure, we mean that no one can read or alter the exchanged data; furthermore, we can be confident that we are connecting with the real server. Thanks to cryptography, these requirements are satisfied.

Cryptography lays the foundation for our digital world. While networking protocols have made it possible for devices spread across the globe to communicate, cryptography has made it possible to trust this communication.

This room is the first of three introductory rooms about cryptography. There are no learning prerequisites except basic abilities to use the Linux command line. If you are not sure, please consider joining the Pre Security path.

- Cryptography Basics (this room)
- Public Key Cryptography Basics
- Hashing Basics

## Learning Objectives
Upon completing this room, you will learn the following:

- Cryptography key terms
- Importance of cryptography
- Caesar Cipher
- Standard symmetric ciphers
- Common asymmetric ciphers
- Basic mathematics commonly used in cryptography

| Judul Artikel | Link Artikel |
| ------------- | --------------- |
| standard required for handling credit card information | https://drive.google.com/file/d/1cnt8Yl8tnKCeMGgn2B80fnzKGZpu8bSR/view?usp=sharing |
| link untuk membuat paintext ke ciphertext dan sebaliknya | https://cryptii.com/pipes/caesar-cipher/ |

<img width="1000" height="974" alt="image" src="https://github.com/user-attachments/assets/1de7c655-98bd-4523-9f10-7bdc28009b32" />

For encryption, we shift to the right by three; for decryption, we shift to the left by three and recover the original plaintext, as illustrated in the image above. However, if someone gives you a ciphertext and tells you that it was encrypted using Caesar Cipher, recovering the original text would be a trivial task as there are only 25 possible keys. The English alphabet is 26 letters, and shifting by 26 will keep the letter unchanged; hence, 25 valid keys for encryption with Caesar Cipher. The figure below shows how decryption will succeed by attempting all the possible keys; in this case, we recovered the original message with Key = 5. Consequently, by today’s standards, where the cipher is publicly known, Caesar Cipher is considered insecure.
