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

## 
