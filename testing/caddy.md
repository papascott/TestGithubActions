# Use Caddy to map HTTPS to PagePark

<a href="https://caddyserver.com/">Caddy</a> is a very easy way to implement HTTPS for your PagePage domains. It is a web server that can do <a href="https://caddyserver.com/docs/automatic-https">automatic HTTPS</a>, automatically provisioning TLS certificates (from <a href="https://letsencrypt.org/">Let's Encrypt</a>) for a domain and keeping them renewed. It can even obtain TLS certificates on demand for your PagePark domains, without out having to configure the domains in Caddy. 

## How to

Here is an example of setting up Caddy on an existing Digital Ocean server running Ubuntu

1. Install the official Caddy package für Ubuntu <a href="https://caddyserver.com/docs/install#debian-ubuntu-raspbian">per their instructions</a>.  This automatically starts and runs Caddy as a systemd service.

1. Open the Caddy configuration in the nano editor with `sudo nano /etc/caddy/Caddyfile`

