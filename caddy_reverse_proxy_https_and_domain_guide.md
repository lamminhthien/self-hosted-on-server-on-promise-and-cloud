# Install Caddy to point domain
sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https curl
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo gpg --dearmor -o /usr/share/keyrings/caddy-stable-archive-keyring.gpg
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list
sudo apt update
sudo apt install caddy

# Caddyfile
sudo nano Caddyfile
```conf
example1.com {
		reverse_proxy localhost:3001
}

example2.com {
	reverse_proxy localhost:9000
}
```

# Give permission HTTPS for caddy
sudo setcap CAP_NET_BIND_SERVICE=+eip $(which caddy)

# Reload to apply domain name without downtime
caddy reload
