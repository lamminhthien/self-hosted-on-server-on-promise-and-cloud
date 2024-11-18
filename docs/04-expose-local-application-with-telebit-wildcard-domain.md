Here’s the revised guide, focusing on using **Telebit commands directly** from the command line without configuration files.

---

# Setting Up Telebit with Wildcard Domains for Prebuilt Docker Applications on macOS (Using Command Line)

This guide demonstrates exposing prebuilt Docker applications using Telebit and wildcard subdomains, entirely via the command line. For this example:

- A **backend** will simulate a REST API available at `api.link.telebit.io`.
- A **frontend** will serve a static website available at `www.link.telebit.io`.

---

## Prerequisites

1. **Install Telebit**  
   Install Telebit globally:
   ```bash
   npm install -g telebit
   ```

2. **Docker Installed**  
   Verify Docker is installed and running:
   ```bash
   docker --version
   ```

3. **Telebit Account**  
   Register with Telebit if you don’t already have an account:
   ```bash
   telebit login
   ```

   Follow the prompts to sign in or create a free account.

---

## Step 1: Start Prebuilt Docker Applications

### Backend: Mock API (Dockerized)

1. **Start the Backend**:  
   Use the `nginxdemos/hello` Docker image to simulate a backend.
   ```bash
   docker run -d --name backend -p 3500:80 nginxdemos/hello
   ```

   - This runs a mock backend API at `http://localhost:3500`.

2. **Verify the Backend**:  
   Open `http://localhost:3500` in your browser or test with `curl`:
   ```bash
   curl http://localhost:3500
   ```

### Frontend: Static Website

1. **Start the Frontend**:  
   Use the official Nginx Docker image for the frontend:
   ```bash
   docker run -d --name frontend -p 3000:80 nginx
   ```

   - This serves a default Nginx static page at `http://localhost:3000`.

2. **Verify the Frontend**:  
   Open `http://localhost:3000` in your browser.

---

## Step 2: Expose Applications with Telebit


### Check the wildcard domain
```bash
telebit status
```

### Expose the Backend

Run Telebit to expose the backend application (`localhost:3500`) to the wildcard domain example `api.link.telebit.io`:
```bash
telebit http 3500 api.link.telebit.io
```

### Expose the Frontend

Run Telebit to expose the frontend application (`localhost:3000`) to the wildcard domain example `www.link.telebit.io`:
```bash
telebit http 3000 www.link.telebit.io
```

---

## Step 3: Access Your Applications

Once Telebit is running, the applications will be accessible via the provided subdomains:

- **Backend**: Visit `https://api.link.telebit.io` to access the backend.
- **Frontend**: Visit `https://www.link.telebit.io` to access the frontend.

---

## Additional Tips

1. **Run Telebit for Multiple Services**:  
   You can run multiple `telebit http` commands in separate terminal windows to expose various services.

2. **Using a Custom Domain**:  
   If you have your own domain:
   - Configure DNS to point to Telebit's servers.
   - Use the `--domain` option with your custom subdomains:
     ```bash
     telebit http 3500 --domain api.yourdomain.com
     telebit http 3000 --domain www.yourdomain.com
     ```

3. **Running Telebit in the Background**:  
   Use tools like `tmux` or `screen` to keep Telebit running in the background.

---

To point your DNS to **Telebit's servers**, you need to configure your domain's DNS records to route traffic through Telebit. Here’s how you can do that:

---

## Step-by-Step Guide: Pointing Your DNS to Telebit's Servers

1. **Log in to Your Domain Registrar's Dashboard**  
   This could be where you registered your domain (e.g., GoDaddy, Namecheap, Cloudflare, etc.). You need access to the DNS management settings for your domain.

2. **Get Telebit's DNS Endpoint**  
   Telebit uses a set of DNS servers to route requests to your local machine. You don’t need to worry about Telebit’s actual IP addresses; it handles this automatically. You only need to set up **CNAME records** or **A records** for your custom domain.

   - **Telebit's DNS endpoint** for wildcard subdomains is: `telebit.io`.  
     This means you will point your subdomain (e.g., `api.yourdomain.com`) to `telebit.io`.

3. **Add DNS Records for Subdomains**

   ### Option 1: Using CNAME Record (Recommended for Subdomains)

   If you want to route a subdomain (e.g., `api.yourdomain.com` or `www.yourdomain.com`) through Telebit, you can use **CNAME** records. These will forward traffic from your subdomains to Telebit’s servers.

   - **Steps**:
     - In your DNS settings, add a **CNAME** record for your subdomain.
     - Set the **Host** or **Name** as the subdomain you want to route (e.g., `api` for `api.yourdomain.com`).
     - Set the **Value** or **Points to** to `telebit.io`.
     - Set the TTL (Time to Live) to the default or a low value (like 300 seconds) to propagate changes quickly.

     Example for `api.yourdomain.com`:
     ```bash
     Type: CNAME
     Host: api
     Points to: telebit.io
     TTL: 300
     ```

     Repeat this process for any other subdomains (e.g., `www`, `app`, etc.).
---

4. **Wait for DNS Propagation**  
   DNS changes can take anywhere from a few minutes to a couple of hours to propagate across the internet. You can check DNS propagation using tools like:

   - [DNS Checker](https://dnschecker.org)
   - `dig yourdomain.com` (in the terminal)

   Use these tools to verify that your domain points to `telebit.io`.

5. **Verify the Connection**  
   After DNS propagation, you should be able to access your service using your custom domain. For example, if you set `api.yourdomain.com` to point to Telebit, you should be able to visit `https://api.yourdomain.com`.

   If you are using Telebit with `telebit http`:
   ```bash
   telebit http 3500 --domain api.yourdomain.com
   ```

---

This approach keeps the setup simple by directly using Telebit commands to expose Docker applications without additional configuration files.
