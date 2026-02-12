# What is Internal TLS?

By default, your "main" SSL certificate
 (the one you configured at the top of the file) encrypts the 
traffic between you (the user) and Harbor. 
However, once the traffic gets inside Harbor, 
the internal parts (like the Core service talking to the Jobservice or 
the Database) usually talk to each other over plain, unencrypted HTTP.

When you enable internal_tls, Harbor encrypts the traffic between its own 
internal components.

Breakdown of the settings:

* enabled: true: This turns on encryption for the "internal" conversations 
between Harbor's microservices.

* dir: /etc/harbor/tls/internal: This is the folder on your hard drive 
where Harbor will look for the special certificates used for these 
internal "secret handshakes."

## Why use it?

|Scenario|Why enable it?|
|:-:|:-:|
|High Security / Compliance|If you are in banking, healthcare, or government, you often need "Encryption in Transit" everywhere, even inside the server.|
|Shared Networks|If Harbor components are spread across different nodes in a cluster, it prevents someone on the same network from "sniffing" the internal traffic.|

* Important Note:If you uncomment this, you must generate and provide internal 
certificates in the directory specified (dir). 
Harbor will not start if it's enabled but the certificates are missing or invalid.
