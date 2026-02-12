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

* strong_ssl_ciphers [read this](README/strong-ssl-ciphers.md)
