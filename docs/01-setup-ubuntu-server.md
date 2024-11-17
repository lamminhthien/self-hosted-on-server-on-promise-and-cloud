### **Tutorial: Set Up an Ubuntu Server with Docker, Docker Compose, Nginx Proxy Manager, and PostgreSQL via Docker**

This guide will walk you through setting up an Ubuntu server, installing Docker, Docker Compose, and setting up Nginx Proxy Manager and PostgreSQL as
Docker containers.

---

## **1. Connect to Your Ubuntu Server via SSH**

To connect to your Ubuntu server:

1. Open your terminal (Linux/macOS) or use an SSH client (like PuTTY on Windows).
2. Run the following command to connect:

   ```bash
   ssh <username>@<server_ip>
   ```

   Replace `<username>` with your server's username (default is `root` for a fresh server) and `<server_ip>` with the server's public IP address.

   Example:

   ```bash
   ssh root@192.168.1.100
   ```

3. If prompted about the authenticity of the host, type `yes`.

4. Enter your password when prompted.

   > **Tip**: If you're using an SSH key for authentication, use the `-i` flag to specify your private key:
   >
   > ```bash
   > ssh -i /path/to/private_key <username>@<server_ip>
   > ```

---

## **2. Update Your Ubuntu Server**

Before installing any software, ensure your server is up-to-date:

```bash
sudo apt update && sudo apt upgrade -y
```

---

## **3. Install Docker**

1. **Install Docker:**

   ```bash
    curl -fsSL https://get.docker.com/ | sudo sh
    sudo usermod -aG docker $USER
   ```

2. **Verify Docker installation:**
   ```bash
   docker --version
   ```

---

## **4. Install Docker Compose**

1. **Download Docker Compose binary:**

   ```bash
   sudo curl -L "https://github.com/docker/compose/releases/download/$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep tag_name | cut -d '"' -f 4)/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
   ```

2. **Make the binary executable:**

   ```bash
   sudo chmod +x /usr/local/bin/docker-compose
   ```

3. **Verify Docker Compose installation:**
   ```bash
   docker-compose --version
   ```

---

## **5. Set Up Nginx Proxy Manager**

1. **Create a directory for Nginx Proxy Manager:**

   ```bash
      echo "Nginx Proxy Manager not found, installing..."
              mkdir ~/nginx-proxy-manager && cd ~/nginx-proxy-manager

      # Install and start Nginx Proxy Manager
      docker run -d \
        --name nginx-proxy-manager \
        --restart unless-stopped \
        -p 80:80 \
        -p 81:81 \
        -p 443:443 \
        -v $(pwd)/data:/data \
        -v $(pwd)/letsencrypt:/etc/letsencrypt \
        jc21/nginx-proxy-manager:latest
   ```

2. **Access the Nginx Proxy Manager UI:**
   - Navigate to `http://<server_ip>:81` in your browser.
   - Default login:
     - **Email:** `admin@example.com`
     - **Password:** `changeme`

---

## **6. Set Up PostgreSQL via Docker**

1. **Create a directory for PostgreSQL:**

```bash
    # Pull the PostgreSQL image
    docker pull postgres:14

    # Run Database (for production)
    docker run -d \
        --name postgres_db \
        -e POSTGRES_PASSWORD=your_password \
        -p 5432:5432 \
        -v $(pwd)/postgres_data:/var/lib/postgresql/data \
        --restart always \
        postgres:14
```

2. **Verify PostgreSQL is running:**

   ```bash
   docker ps
   ```

3. **Connect to PostgreSQL:** Use a PostgreSQL client like `psql` or any database management tool. Example connection details:
   - **Host:** `<server_ip>`
   - **Port:** `5432`
   - **User:** `postgres`
   - **Password:** `your_password`
   - **Database:** `postgres`

---

## **7. Set Up Swap Memory**

Swap memory is crucial for server stability and performance. Here's why:

- Prevents Out of Memory (OOM) crashes by providing a safety buffer
- Helps manage memory-intensive Docker containers like PostgreSQL and Nginx
- Acts as an early warning system for memory issues
- Provides system stability during unexpected memory spikes
- Critical for production environments where uptime is important

> **Note**: We recommend setting swap to half of your RAM size as a best practice. Too little swap risks system crashes, while too much can impact
> performance if heavily used.

1. **Check current memory and swap:**

   ```bash
   free -h
   ```

2. **Create a swap file with half of your RAM size:**

   ```bash
   # Get total RAM in GB and calculate half (rounded down)
   total_ram=$(free -g | awk '/^Mem:/{print $2}')
   swap_size=$((total_ram / 2))

   # Create and set up swap file
   sudo fallocate -l ${swap_size}G /swapfile
   sudo chmod 600 /swapfile
   sudo mkswap /swapfile
   sudo swapon /swapfile
   ```

3. **Make swap permanent:**

   ```bash
   echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
   ```

4. **Verify swap is active:**
   ```bash
   swapon --show
   ```
