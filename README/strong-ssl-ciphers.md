# The Concept of Strong SSL Ciphers in Simple Terms

When your browser or Docker client connects to Harbor,
 they perform an "initial handshake" to agree on how to encrypt the information.
 The set of mathematical algorithms that handle this encryption is called a
 **Cipher Suite**.

Some of these older algorithms (such as DES or RC4) are now considered insecure,
 and hackers can break them.

## What does this setting do in Harbor?

If you set this option to true:

* Removal of Weak Algorithms: Harbor instructs Nginx (its internal web server) 
to use only modern and highly secure encryption algorithms 
(like AES-GCM and ChaCha20).

* Higher Security: Older protocols like TLS 1.0 and TLS 1.1 are disabled,
 and only secure versions (like TLS 1.2 and TLS 1.3) will be permitted.

* Attack Prevention: It prevents threats such as
 Man-in-the-Middle and Downgrade Attacks.

## Pros and Cons of Enabling It

|Pros|Cons (Cautions)|
|:-:|:-:|
|Superior Security: Your data is protected by the best modern world standards.
|No Support for Legacy Clients: If you have very old systems on your network,
 they may be unable to connect to Harbor.|
|Compliance: This is mandatory for obtaining standards like SOC2 or PCI-DSS.
|Minor CPU Load: Stronger encryption may result in a very negligible increase in processing load.|
