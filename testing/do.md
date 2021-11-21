# Setting up PagePark on DigitalOcean from scratch

1. Tip: add an SSH key to your <a href="https://cloud.digitalocean.com/account/security">DigitalOcean Security settings</a> to make logging in easier

Does this help?

1. Spin up an Ubuntu droplet (choose the SSH key you uploaded earlier)

Does this help

1. Initial <a href="https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-20-04">server setup</a>

  1. Login as root

  2. Create a new user

  3. Grant administrative privleges

  4. Setting up basic firewall

  5. Enable external access for your regular user 

1. Additional server setup

1. Disable root login for ssh: delete /root/.ssh/authorized_keys 

1. <a href="https://askubuntu.com/questions/147241/execute-sudo-without-password">Enable password-less sudo</a> for your user 

1. Allow HTTP and HTTPS in your firewall (ufw allow 80; ufw allow 443) 

1. Install nodejs 

I personally like <a href="https://github.com/nvm-sh/nvm#installing-and-updating">nvm</a> as the regular user, it keeps node and npm modules separate from the system

nvm install --lts (or 'nvm install 14.17.5' for a specific version  

When you install a new version of nodejs, 'nvm install node --reinstall-packages-from=node' to migrate global packages 

1. Install pm2 globally

1. <a href="https://caddyserver.com/docs/install#debian-ubuntu-raspbian">Install Caddy</a> for Ubuntu

sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https

curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo tee /etc/apt/trusted.gpg.d/caddy-stable.asc

curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list

sudo apt update

sudo apt install caddy

