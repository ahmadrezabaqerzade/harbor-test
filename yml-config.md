# harbor.yml

## Host Name

Specify the IP address or the fully qualified domain name (FQDN) of the target host on which to deploy Harbor. This is the address at which you access the Harbor Portal and the registry service. For example, 192.168.1.10 or reg.yourdomain.com. The registry service must be accessible to external clients, so do not specify localhost, 127.0.0.1, or 0.0.0.0 as the hostname.

	hostname: reg.mydomain.com

## HTTP config
	http:
	   port: 80

