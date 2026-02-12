# harbor.yml

## Host Name

Specify the IP address or the fully qualified domain name (FQDN) of the target host on which to deploy Harbor. This is the address at which you access the Harbor Portal and the registry service. For example, 192.168.1.10 or reg.yourdomain.com. The registry service must be accessible to external clients, so do not specify localhost, 127.0.0.1, or 0.0.0.0 as the hostname.

	hostname: reg.mydomain.com

## HTTP config
Do not use HTTP in production environments. Using HTTP is acceptable only in air-gapped test or development environments that do not have a connection to the external internet. Using HTTP in environments that are not air-gapped exposes you to man-in-the-middle attacks.

	http:
	   port: 80

## HTTPS config
Use HTTPS to access the Harbor Portal and the token/notification service. Always use HTTPS in production environments and environments that are not air-gapped.

	https:
	   port: 443
	   certificate: your/certificate/path #.crt file path
	   private_key: your/private/key/path #.key file path
	   strong_ssl_ciphers: false #(default:false) you can comment this line

* port: The port number for HTTPS, for both Harbor portal and Docker commands. The default is 443.

* certificate: The path to the SSL certificate.

* private_key: The path to the SSL key.

* [strong_ssl_ciphers](strong-ssl-ciphers.md)


## IP Family

	ip_family:
		ipv6:
		   enabled: false
		ipv4:
		   enabled: true

* ip_family: This is the category for your network protocol settings.

* ipv4: enabled: true: This is the default. Most networks today still run on IPv4 (addresses like 192.168.1.1). Harbor leaves this on so it can communicate with almost any server.

* ipv6: enabled: false: IPv6 uses much longer addresses (like 2001:0db8:85a3...). By default, Harbor keeps this off because many Docker networks aren't configured for it yet.


## Internal TLS

	internal_tls:
		enabled: true
		dir: /etc/harbor/tls/internal

* enabled: true: This turns on encryption for the "internal" conversations between Harbor's microservices.

* dir: /etc/harbor/tls/internal: This is the folder on your hard drive where Harbor will look for the special certificates used for these internal "secret handshakes."

[more information](internal-tls.md)

## External URL
	external_url: https://reg.mydomain.com:8433

* It overrides hostname: Harbor will ignore the hostname setting and use this URL for everything.

* Absolute Links: Every link, redirect, and "pull" command shown in the Harbor interface will use this exact address.

[more information](external-url.md)

## Harbor Admin Password
	harbor_admin_password: init password

This sets the initial password for the default admin user. When you first 
open the Harbor web interface, you will log in with the username admin and 
whatever password you type here.

## Database
	database:
  		password: init password
  		max_idle_conns: 100
  		max_open_conns: 900
  		conn_max_lifetime: 5m
  		conn_max_idle_time: 0

* password: root123: This is the password for the internal postgres user.

* max_idle_conns: 100: This is how many "receptionists" stay at the desk even 
when no one is asking for help. 
It keeps Harbor snappy during sudden bursts of traffic.

* max_open_conns: 900: This is the absolute limit of "receptionists" working at
 once. It should be lower than the database's own max_connections
 (usually 1024) to leave room for maintenance tasks.

* conn_max_lifetime: 5m: After 5 minutes, a connection is "retired" and replaced 
with a fresh one. 
This prevents issues like memory leaks or stale connections.

* conn_max_idle_time: 0: If set to 0, idle connections are never closed 
based on age (they only close if they hit the max_lifetime).

## Data Volume
	data_volume: path

The data_volume is the persistent storage location. Even though Harbor runs 
inside Docker containers, the containers themselves are "ephemeral" 
(meaning they lose their data if they are deleted). This setting maps a folder on 
your physical 
server's hard drive into those containers so your data is saved forever.

[more information](data-volume.md)

