# Test localhost:3001
curl localhost:3001

# Completely remove nginx before install caddy
sudo apt remove nginx
sudo apt remove nginx nginx-commons
sudo apt purge nginxsudo apt-get autoremove
sudo apt-get autoremove

# Using server free from google cloud
https://console.cloud.google.com

# Domain free for learning
https://freedomain.one/index.jsp

# Test Domain after point to ip server (Mac and linux)
dig your-domain-name

# Install Caddy to point domain
sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https curl &&\
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo gpg --dearmor -o /usr/share/keyrings/caddy-stable-archive-keyring.gpg &&\
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list &&\
sudo apt update -y &&\
sudo apt install caddy -y

# Give permission HTTPS for caddy
sudo setcap CAP_NET_BIND_SERVICE=+eip $(which caddy)

# Restart for take effect
caddy stop
caddy start

# Caddyfile
mkdir caddy-config && cd caddy-config
sudo nano Caddyfile

```Caddyfile
kuma.thienlam3.line.pm {
		reverse_proxy localhost:3001
}
```
# Reload to apply domain name without downtime
caddy reload

