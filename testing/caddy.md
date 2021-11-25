# Use Caddy to map HTTPS to PagePark
<i>Draft 2021-11-21 SMH</i>

<a href="https://caddyserver.com/">Caddy</a> is a very easy way to implement HTTPS for your PagePage domains. It is a web server that can do <a href="https://caddyserver.com/docs/automatic-https">automatic HTTPS</a>, automatically provisioning TLS certificates (from <a href="https://letsencrypt.org/">Let's Encrypt</a>) for a domain and keep them renewed. It can even obtain TLS certificates on demand for your PagePark domains, without out having to configure the domains in Caddy. 
## How to
Here is an example of setting up Caddy on an existing PagePark installation on a Digital Ocean server running Ubuntu (assuming you have domains in your domains folder and have <a href="https://github.com/scripting/pagePark#mapping-port-80-to-1339">mapped port 80 to PagePark</a> using iptables as in the instructions).
1. Install the official Caddy package für Ubuntu <a href="https://caddyserver.com/docs/install#debian-ubuntu-raspbian">per their instructions</a>.  This automatically starts and runs Caddy as a systemd service.
1. Open the Caddy configuration file in the nano editor with `sudo nano /etc/caddy/Caddyfile`
1. Replace the entire contents with: 
   ```
   {
     on_demand_tls {
       ask http://localhost:1339/isdomainvalid
       interval 2m
       burst    5
     }
   }
   https:// {
     tls {
       on_demand
     }
     reverse_proxy localhost:1339
   }
   ```
1. Restart the Caddy service with `sudo service caddy restart`
1. Test https for one of your domains in the terminal with curl: e.g. `curl https://www.example.com`. This first time it will take several seconds for Caddy to request and obtain a certificate. It may even fail the first time, but then try again. The content of the index page of your domain should be printed to the terminal. That means it works!
This configuration means that both HTTP (over iptables) and HTTPS (over Caddy) will work for your domains!
## Running Caddy without iptables mapping
If you have not mapped port 80 to PagePark, this configuration will also listen to port 80 and redirect HTTP requests to HTTPS. 
If you'd rather not redirect port 80, you can extend the Caddy configuration file to this:
   ```
   {
     auto_https disable_redirects

     on_demand_tls {
       ask http://localhost:1339/isdomainvalid
       interval 2m
       burst    5
     }
   }
   https:// {
     reverse_proxy localhost:1339
   }
   https:// {
     tls {
       on_demand
     }
     reverse_proxy localhost:1339
   }
   ```
