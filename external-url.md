# External URL

This setting is used when Harbor is sitting behind a Reverse Proxy or a 
Load Balancer (like Nginx, HAProxy, or an F5 Big-IP) that uses a different 
address or port than Harbor itself.

## What it does:
Normally, Harbor uses the hostname field to generate links
 (like the "docker pull" commands you see in the UI). However, 
if your users connect to a proxy first, and that proxy sends the 
traffic to Harbor on a different port, the hostname might not be enough.

When you enable external_url:

* It overrides hostname: Harbor will ignore the hostname setting and use this URL for everything.

* Absolute Links: Every link, redirect, and "pull" command shown in the Harbor interface will use this exact address.

## When should you use it?
You should uncomment and use external_url in these three common scenarios:

* 1.Non-Standard Ports: If your registry is accessed via a specific port 
(like :8433 in the example) that is different from the standard 443.

* 2.SSL Termination at Proxy: If your users connect via HTTPS to a proxy, 
but the proxy talks to Harbor over HTTP (Port 80). 
Without external_url, Harbor might mistakenly give users http:// 
links instead of https://.

* 3.Complex Paths: If Harbor is hosted at a sub-path or a completely different 
domain name handled by an external gateway.

## Example:
If your hostname is internal-harbor.local but the public address 
people use is https://hub.company.com, 
you would set: external_url: https://hub.company.com
