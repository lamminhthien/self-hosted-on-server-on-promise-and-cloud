### **Tutorial: Set Up Domains and Subdomains with Namecheap and Nginx Proxy Manager**

This guide explains how to configure your domains and subdomains in Namecheap and use **Nginx Proxy Manager** to route traffic to your API, admin
portal, and website. It also includes instructions for redirecting non-www traffic to www for the website.

---

### **1. Prerequisites**

- **Domain Purchased on Namecheap:** Example: `example.com`.
- **Server IP Address:** Example: `103.15.15.1`.
- **Nginx Proxy Manager Installed:** Running on your server as per the [setup guide above](#).

---

### **2. Configure DNS Records in Namecheap**

1. **Log in to Namecheap:**

   - Go to [Namecheap](https://www.namecheap.com/) and log in to your account.

2. **Navigate to Domain List:**

   - Click on **Domain List** in the left sidebar.
   - Find your domain (e.g., `example.com`) and click **Manage**.

3. **Set Up DNS Records:** Under the **DNS Settings** tab, do the following:

   | **Type** | **Host** | **Value**     | **TTL**     |
   | -------- | -------- | ------------- | ----------- |
   | `A`      | `@`      | `103.15.15.1` | `Automatic` |
   | `A`      | `www`    | `103.15.15.1` | `Automatic` |
   | `A`      | `api`    | `103.15.15.1` | `Automatic` |
   | `A`      | `admin`  | `103.15.15.1` | `Automatic` |

   > **Note:**

   - `@` represents the root domain (e.g., `example.com`).
   - Subdomains (`www`, `api`, `admin`) also point to your server.

4. **Save Changes:**

   - After adding all records, ensure the changes are saved.

   > **DNS Propagation:** These changes may take up to 24 hours to propagate globally, but it usually happens within minutes.

---

### **3. Set Up Nginx Proxy Manager**

1. **Access Nginx Proxy Manager:**

   - Navigate to `http://<server_ip>:81` (e.g., `http://103.15.15.1:81`).
   - Log in using your credentials.

2. **Add Proxy Hosts:**

#### **a. API Subdomain (`api.example.com`):**

1. Go to **Proxy Hosts** → Click **Add Proxy Host**.
2. Fill in the form:
   - **Domain Names:** `api.example.com`.
   - **Scheme:** Select `http` or `https` based on your backend service.
   - **Forward Hostname/IP:** Enter the IP or hostname of the API backend.
   - **Forward Port:** Enter the port your API service is running on (e.g., `3500`).
   - **Websockets Support:** Check this box if your API uses websockets.
3. **SSL Setup:**
   - Enable **Force SSL** to redirect HTTP traffic to HTTPS.
   - Click **Request a New SSL Certificate** → Select **Let’s Encrypt**.
   - Enter your email and agree to the terms.
4. Save the configuration.

#### **b. Admin Portal Subdomain (`admin.example.com`):**

Repeat the steps for the API, using `admin.example.com` as the **Domain Names** and the corresponding backend host and port.

#### **c. Website (`example.com` and `www.example.com`):**

1. Add a Proxy Host for the website.
   - **Domain Names:** Add both `example.com` and `www.example.com`.
   - **Forward Hostname/IP:** Enter the website backend’s hostname or IP.
   - **Forward Port:** Enter the port (e.g., `3000`).
2. **Redirect Non-www to www:**
   - Enable **Force SSL**.
   - Check **Block Common Exploits**.
   - Under the **Custom Nginx Config** section, add:
     ```nginx
     if ($host = example.com) {
         return 301 https://www.example.com$request_uri;
     }
     ```
3. Request and enable an SSL certificate as above.

---

### **4. Verify Configuration**

- Open your browser and verify:
  - `api.example.com` routes to your API.
  - `admin.example.com` routes to the admin portal.
  - `example.com` redirects to `www.example.com`, which routes to your website.

---

### **5. Troubleshooting**

- **DNS Issues:** Use `nslookup` or `ping` to check DNS propagation:
  ```bash
  nslookup api.example.com
  ```
- **Nginx Logs:** Check Nginx Proxy Manager logs for errors:
  ```bash
  docker logs nginx-proxy-manager
  ```
- **Firewall:** Ensure your server firewall allows ports `80`, `443`, and the backend service ports.

---

This setup ensures your API, admin portal, and website are accessible with secure SSL and appropriate redirections using Nginx Proxy Manager!
