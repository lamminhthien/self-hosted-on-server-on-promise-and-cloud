# **GitHub Actions Secrets Setup Documentation**

## **Required Secrets**

### **1. Server Configuration**

- **`STAGE_SERVER_HOST`**: Hostname or IP address of your staging server.
- **`STAGE_SERVER_USER_NAME`**: SSH username for the staging server.
- **`STAGE_SERVER_PASSWORD`**: SSH password for the staging server.

### **2. Application Environment Variables**

- **`PORTAL_STAGE`**: Environment variables for the **Admin Portal**.
- **`API_STAGE`**: Environment variables for the **Admin API**.
- **`WEBSITE_STAGE`**: Environment variables for the **Website**.

---

## **How to Add Secrets**

### **Steps to Add Secrets in GitHub**

1. Navigate to your **GitHub repository**.
2. Go to **Settings → Secrets and variables → Actions**.
3. Click on **New repository secret**.
4. Add each secret using the details below:

#### **Server Access Secrets**

- **Example for `STAGE_SERVER_PASSWORD`:**
  - Add the password used to authenticate with your staging server.

#### **Application Environment Secrets**

- Each secret should include all environment variables for the respective application, in the format:
  - `KEY=value` (space-separated, all on one line).

**Example Formats:**

- **`PORTAL_STAGE`**:
  ```
  DB_HOST=portal-db.example.com DB_PORT=5432 DB_USER=admin DB_PASSWORD=securepassword
  ```
- **`API_STAGE`**:
  ```
  API_KEY=12345abcde API_SECRET=supersecret API_HOST=api.example.com
  ```
- **`WEBSITE_STAGE`**:
  ```
  NEXT_PUBLIC_API_URL=https://api.example.com NEXT_PUBLIC_ENV=staging
  ```

---

## **Important Notes**

### **Environment Variables Format**

- All variables for **`PORTAL_STAGE`**, **`API_STAGE`**, and **`WEBSITE_STAGE`** should:

  - Be **space-separated**.
  - Appear on a **single line**.
  - Follow the format: `KEY=value`.

- The workflow automatically converts these variables into a proper `.env` file format.

---

### **Security Considerations**

- Never commit sensitive information directly to your repository.
- Regularly **rotate passwords and sensitive credentials**.
- Prefer **SSH keys** over passwords for server authentication.

---

### **Port Mappings**

- **Admin Portal**: Port **3001**.
- **Admin API**: Port **3500**.
- **Website**: Port **3000** (mapped internally to **3001**).
- Ensure these ports are available on your staging server.

---

### **Deployment Verification**

- The workflows include a **health check**:
  - Pings the application after deployment.
  - Deployment fails if the application doesn’t respond within **5 seconds**.

---

## **Troubleshooting**

If deployments fail, check the following:

1. **Server Connectivity and Credentials**:
   - Verify the server's availability and credentials used.
2. **Port Availability**:
   - Ensure required ports are free on the staging server.
3. **Environment Variables Format**:
   - Double-check the format of `PORTAL_STAGE`, `API_STAGE`, and `WEBSITE_STAGE` secrets.
4. **Application Health Check**:
   - Confirm the health check endpoints are responding.
5. **Docker Daemon Status**:
   - Ensure Docker is running on the staging server.

---

By following this guide, you can ensure smooth deployment workflows while maintaining security and reliability.
