![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/d75ac741-a52a-42d9-bfdf-5e156f27cd38)# Tutorial: Self-Hosted Node.js App Deployment on On-Premise and Cloud Servers with CI/CD
# Section
I. [Create an EC2 on AWS](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud#attach-static-ip-may-be-in-other-cloud-platform-in-vietnam-static-ip-will-be-available-by-default)

II. [Create and attach Elastic IPs to EC2](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud#attach-static-ip-may-be-in-other-cloud-platform-in-vietnam-static-ip-will-be-available-by-default)

III. [Create Github Action Workflow](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud#setup-github-action-workflow-first)

IV. [Managing Secrets and Variables in GitHub Actions](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud#managing-secrets-and-variables-in-github-actions)

## I. Create and EC2 on AWS

### 1. Type "EC2"
![Step 1](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/f267946a-9653-4f66-a5e4-5a310fe5e2cc)

### 2. Click on EC2
![Step 2](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/8e8c2495-e8a1-41c9-a98f-aa5249079ed9)

### 3. Click on Launch instance
![Launch Instance](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/5c422d66-b368-433b-b64a-2cc2dbda98e6)

### 4. Type a name for your server
![Type a name for your server](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/cd8abe02-ec57-481b-b12c-06052f775d89)

### 5. Choose Ubutnu
![Choose Ubuntu](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/120a5658-99fb-4d45-8c40-6bbfd7a3a240)

### 6. Choose Amazon Machine Image (AMI)
![Choose AMI](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/a2b0d0c3-063b-4827-91f5-8369cca28d28)


### 7. Choose Instance type
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/6776335a-4a28-4b6e-83ec-313a7395f30b)

### 8. Searching t3.medium for server with 2vCPU and 4GB Ram.
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/fd6651d9-90ad-4bd9-9fed-ee610ae5a668)


### 9. Click on t3.medium. If you want more RAM, you can choose t3.large.
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/bf67db81-b919-4370-a320-6c90fa8a7f81)

### 10. Key pair (login). Click create new key pair. This will use for login to server and using in CI/CD
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/662687f1-d21b-40b8-9a8f-e0d236433eb4)

### 11. Type Key pair name. Example "self-hosted"
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/c4983642-cb88-47eb-9390-cd3e603d3a2f)

### 12. Click on Create key pair in this popup
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/19a20a0a-ecf7-4f3a-aa57-6f7468c41d96)


### 13. Check Allow HTTPS traffic from the internet (For SSL later)
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/3c23f45b-fcf0-4184-88ff-490c6096814e)

### 14. Check Allow HTTP traffic from the internet (For port 80)
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/93ff80a9-7247-4f05-ad90-77ff48cef859)

### 15. Choose storage size for SSD in "EBS Volumes". Example 32GB



### 16. Change Volume type (SSD Type).
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/a28f5f8c-b129-4fdd-95e9-1da0cfdc9f05)

### 17. Click on General purpose SSD (gp3)…
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/d12dd355-9de5-4296-8b26-2f48155a846e)

### 18. Click on Advanced details. To setup terminate protection, Cloudwatch Detailed Monitoring and UserData (For preinstall some of software we need)
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/72f03804-500d-4521-a97c-2be55828e2f3)

### 19. Enable Termination protection
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/94eb22dd-26b9-4779-92f8-caa483892d4e)

### 20. Enable Detailed CloudWatch monitoring
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/1a7f89cb-46f4-4192-80c9-0499407f698e)

### 21. Scrolldown to User data - optional

Add this content below:

```sh
#!/bin/bash
sudo apt update -y

# Install Docker and Nginx using Snap
sudo snap install docker
sudo snap install nginx

# Grant permission for run Docker without root user
sudo chmod 666 /var/run/docker.sock

# Install Certbot for Let's Encrypt
sudo apt install -y certbot python3-certbot-nginx
sudo systemctl enable nginx
sudo systemctl start nginx
```

This code is a bash script that performs several tasks related to setting up a server environment. Let's break down each step:

1. sudo apt update -y: This command updates the package lists on the server by fetching the latest version information from the repositories.

2. sudo snap install docker: This command installs Docker, a popular platform for containerization, using the Snap package manager. Snap is a software deployment and package management system used in Ubuntu and other Linux distributions.

3. sudo snap install nginx: This command installs Nginx, a high-performance web server and reverse proxy, also using the Snap package manager.

4. sudo chmod 666 /var/run/docker.sock: This command grants read and write permissions to the Docker socket file, allowing Docker to be run without root user privileges. The Docker socket file is used for communication between the Docker daemon and the Docker client.

5. sudo apt install -y certbot python3-certbot-nginx: This command installs Certbot, a tool for obtaining and managing SSL/TLS certificates from Let's Encrypt, along with the Certbot Nginx plugin. The Nginx plugin automates the process of configuring Nginx to use the obtained certificates.

6. sudo systemctl enable nginx: This command enables the Nginx service to start automatically on system boot.

7. sudo systemctl start nginx: This command starts the Nginx service immediately.

Overall, this script updates the package lists, installs Docker and Nginx, grants Docker permissions, installs Certbot and the Certbot Nginx plugin, and starts the Nginx service. It sets up a basic server environment for hosting websites or applications with SSL/TLS encryption using Let's Encrypt certificates.

![Step 22 screenshot](https://images.tango.us/workflows/6c8c03a1-e2d9-49ca-9c8b-c96b736b5e52/steps/0d313b05-6cf5-4f7c-804f-3efa238b5e45/bc224a1b-2086-4a2e-9098-68c5aeb1e659.png?crop=focalpoint&fit=crop&fp-x=0.3303&fp-y=0.5585&fp-z=1.2580&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=125&mark-y=216&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz03NDcmaD00NTQmZml0PWNyb3AmY29ybmVyLXJhZGl1cz0xMA%3D%3D)


### 23. Click on Launch instance
![Step 23 screenshot](https://images.tango.us/workflows/6c8c03a1-e2d9-49ca-9c8b-c96b736b5e52/steps/5c28d19e-2bac-443c-b7e2-d6987bad8edc/2528bb9d-3b06-432d-a4e2-f2a8f5ec7362.png?crop=focalpoint&fit=crop&fp-x=0.6774&fp-y=0.8638&fp-z=2.5557&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=389&mark-y=524&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz00MjEmaD0xMDYmZml0PWNyb3AmY29ybmVyLXJhZGl1cz0xMA%3D%3D)


## Attach Static IP (May be in other cloud platform in Vietnam, Static IP will be available by default)

### 1. Type "Elastic IPs" in Search box
![Step 1 screenshot](https://images.tango.us/workflows/202410a7-6b44-410c-b6ce-2d3d9ed3357e/steps/d44c317d-8e17-411f-9298-1146d7bd57c4/aa352ca6-2049-4a06-889f-646aeb7723b0.png?crop=focalpoint&fit=crop&fp-x=0.3791&fp-y=0.0271&fp-z=1.2931&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=221&mark-y=5&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz03MzQmaD01MSZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 2. Click on Elastic IPs
![Step 2 screenshot](https://images.tango.us/workflows/202410a7-6b44-410c-b6ce-2d3d9ed3357e/steps/a8aebdf3-46f5-4021-936b-4b25a1960c0f/c520fb1e-aa60-4cd6-ae8c-8c03721cd05c.png?crop=focalpoint&fit=crop&fp-x=0.4168&fp-y=0.2479&fp-z=2.6531&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=478&mark-y=401&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz0yNDUmaD04MiZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 3. Click on Allocate Elastic IP address
![Step 3 screenshot](https://images.tango.us/workflows/202410a7-6b44-410c-b6ce-2d3d9ed3357e/steps/65bdcfc4-e89d-48ea-aaf0-cc1ddca01117/41cf1632-3b0b-430c-ac7a-5f9395197389.png?crop=focalpoint&fit=crop&fp-x=0.8532&fp-y=0.1197&fp-z=2.9012&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=346&mark-y=250&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz02ODYmaD0xMTUmZml0PWNyb3AmY29ybmVyLXJhZGl1cz0xMA%3D%3D)


### 4. Click on Allocate
![Step 4 screenshot](https://images.tango.us/workflows/202410a7-6b44-410c-b6ce-2d3d9ed3357e/steps/190597d4-ed68-4a3f-814a-0fbf6ca65043/5d5d2591-6db3-4dc2-b136-59da1e7513d3.png?crop=focalpoint&fit=crop&fp-x=0.6831&fp-y=0.9234&fp-z=2.7576&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=449&mark-y=644&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz0zMDMmaD0xMDkmZml0PWNyb3AmY29ybmVyLXJhZGl1cz0xMA%3D%3D)


### 5. Click on Associate this Elastic IP address
![Step 5 screenshot](https://images.tango.us/workflows/202410a7-6b44-410c-b6ce-2d3d9ed3357e/steps/4e36ff25-b356-40e8-9a80-76bea4c22f68/a06fc9fd-b29c-4d24-8bb5-043718b66dfe.png?crop=focalpoint&fit=crop&fp-x=0.8110&fp-y=0.1122&fp-z=2.9012&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=202&mark-y=231&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz03OTcmaD0xMTUmZml0PWNyb3AmY29ybmVyLXJhZGl1cz0xMA%3D%3D)


### 6. Make sure Resource type is Instance. Then choose instance in Instance Select
![Step 6 screenshot](https://images.tango.us/workflows/202410a7-6b44-410c-b6ce-2d3d9ed3357e/steps/cf34954d-5fe9-4bfc-a147-8aa07bba13ec/359f7cbb-e495-4bb4-aa61-0cb380258183.png?crop=focalpoint&fit=crop&fp-x=0.2957&fp-y=0.6894&fp-z=1.2580&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=73&mark-y=513&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz03NDcmaD01MiZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 7. Choose your suitable instance
![Step 7 screenshot](https://images.tango.us/workflows/202410a7-6b44-410c-b6ce-2d3d9ed3357e/steps/26bad512-1d39-41ac-aa6a-cbdd54fe6fd4/2c90aa07-a94d-436a-a29b-5fcba0bfeb60.png?crop=focalpoint&fit=crop&fp-x=0.2957&fp-y=0.7266&fp-z=1.2580&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=73&mark-y=555&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz03NDcmaD01MiZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 8. Click on Associate
![Step 8 screenshot](https://images.tango.us/workflows/202410a7-6b44-410c-b6ce-2d3d9ed3357e/steps/5cca069a-e73d-4d9e-a09b-0e084447755e/8933593e-2a1f-4fe9-ac88-e28103848979.png?crop=focalpoint&fit=crop&fp-x=0.6796&fp-y=0.9223&fp-z=2.7049&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=440&mark-y=643&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz0zMjAmaD0xMTImZml0PWNyb3AmY29ybmVyLXJhZGl1cz0xMA%3D%3D)



### 9. On Allocated IPv4 address. Click copy IPv4 address to use for setup domain name, CI/CD,...
![Step 9 screenshot](https://images.tango.us/workflows/9cc92e62-fac1-456c-b062-2be1d095714f/steps/d6773db4-925c-4a0f-b05d-faa799124fa4/7a7211f7-0b5d-436c-8281-0a17f98d27d7.png?crop=focalpoint&fit=crop&fp-x=0.2659&fp-y=0.4415&fp-z=3.0032&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=563&mark-y=399&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz03NSZoPTg4JmZpdD1jcm9wJmNvcm5lci1yYWRpdXM9MTA%3D)



# [GitHub: Step-by-Step Instructions for Setting Up a Workflow](https://app.tango.us/app/workflow/55d4c68e-40d1-486e-9c72-8d906266f517?utm_source=markdown&utm_medium=markdown&utm_campaign=workflow%20export%20links)
## Setup Github Action Workflow first

This code is a GitHub Actions workflow that automates the deployment of a project to a server in a staging environment. Let's go through the code step by step to understand its functionality:

1. The code starts by defining the environment variables. The `APP_ENV` variable is set to the value stored in the `STAGING` secret.

2. The workflow is triggered when a push event occurs on the `main` branch.

3. The `build-and-deploy` job is defined, which runs on an `ubuntu-latest` machine.

4. The steps of the job are as follows:

   a. **Pull code**: This step uses the `actions/checkout` action to fetch the latest code from the repository.

   b. **Extract env file multi line**: This step creates an environment file (`.env`) based on the `APP_ENV` value. It removes any existing `.env` file, creates a temporary file (`.env_temp`), writes the `APP_ENV` value to it, converts spaces to newlines, and appends the contents to the final `.env` file. Finally, it removes the temporary file.

   c. **Docker**: This step builds a Docker image for the project using the `docker build` command. It then saves the image as a tar file (`your-project-name.tar`).

   d. **Copy Docker image to ec2 use SSH Key**: This step uses the `appleboy/scp-action` action to copy the Docker image tar file and the `docker-compose.yml` file to the target server. It connects to the server using SSH, specified by the `STAGE_SERVER_HOST`, `STAGE_SERVER_KEY_SSH`, and other credentials stored as secrets.

   e. **Executing remote ssh commands using SSH Key**: This step uses the `appleboy/ssh-action` action to execute remote SSH commands on the target server. It connects to the server using SSH and runs the following commands:
      - `sudo docker system prune -a -f`: Cleans up any unused Docker resources on the server.
      - `cd ~/your-project-name`: Changes the directory to the project directory on the server.
      - `sudo snap install docker`: Installs Docker on the server (if not already installed).
      - `sudo docker load --input your-project-name.tar`: Loads the Docker image from the tar file.
      - `sudo docker-compose up -d --force-recreate`: Starts the project using Docker Compose, recreating containers if necessary.
      - `rm -rf your-project-name.tar`: Removes the Docker image tar file from the server.

This workflow automates the process of building a Docker image, copying it to a server, and deploying the project using Docker Compose. It ensures consistency and simplifies the deployment process in a staging environment.

### 1. Click on Actions
![Step 1 screenshot](https://images.tango.us/workflows/55d4c68e-40d1-486e-9c72-8d906266f517/steps/81556aef-7e5b-4bb4-ad93-e94b97468437/f8b0bc1b-d662-4041-908d-e85eebe0e4b8.png?crop=focalpoint&fit=crop&fp-x=0.2916&fp-y=0.0851&fp-z=2.6475&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=477&mark-y=152&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz0yNDcmaD05NSZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 2. Click on set up a workflow yourself 
![Step 2 screenshot](https://images.tango.us/workflows/55d4c68e-40d1-486e-9c72-8d906266f517/steps/c1f7af43-0209-4624-abdc-89a8f9d6f4db/8d194000-d005-434c-80aa-72461d37abf1.png?crop=focalpoint&fit=crop&fp-x=0.1927&fp-y=0.2654&fp-z=2.1996&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=305&mark-y=417&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz00MDgmaD01MiZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 3. Type "deploy.staging.yml"
![Step 3 screenshot](https://images.tango.us/workflows/55d4c68e-40d1-486e-9c72-8d906266f517/steps/7e8a6583-b6d6-4f98-a66a-5a116f01366c/58edb120-0f97-4174-be30-13e51b07c8fa.png?crop=focalpoint&fit=crop&fp-x=0.5149&fp-y=0.1447&fp-z=2.2343&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=402&mark-y=246&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz0zOTYmaD04MCZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 4. Paste selected text into element
You can get content from folder .github/workflows
![Step 4 screenshot](https://images.tango.us/workflows/55d4c68e-40d1-486e-9c72-8d906266f517/steps/2a828c22-309b-4c3d-80f6-6df89fd3ffbd/c7789ab9-f8bd-4784-851f-0aef08053a58.png?crop=focalpoint&fit=crop&fp-x=0.5157&fp-y=0.2489&fp-z=1.0434&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=6&mark-y=210&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz0xMTg3Jmg9MzkmZml0PWNyb3AmY29ybmVyLXJhZGl1cz0xMA%3D%3D)


### 6. Click on Commit changes...
![Step 6 screenshot](https://images.tango.us/workflows/55d4c68e-40d1-486e-9c72-8d906266f517/steps/eefa6e27-54c8-4726-9924-1d5397ef41f9/ba2028fc-6188-4d46-b916-a03f3bb788b6.png?crop=focalpoint&fit=crop&fp-x=0.9286&fp-y=0.1021&fp-z=2.9193&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=733&mark-y=209&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz00MzQmaD0xMTAmZml0PWNyb3AmY29ybmVyLXJhZGl1cz0xMA%3D%3D)


### 7. Click on Commit message
![Step 7 screenshot](https://images.tango.us/workflows/55d4c68e-40d1-486e-9c72-8d906266f517/steps/da42bc50-bf59-408b-828c-0b39351e1b91/20999cca-ff42-43f3-aa9c-5087397fe69a.png?crop=focalpoint&fit=crop&fp-x=0.5000&fp-y=0.3489&fp-z=1.5236&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=274&mark-y=415&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz02NTImaD01NSZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 8. Select Create a new branch for this commit and start a pull request…
![Step 8 screenshot](https://images.tango.us/workflows/55d4c68e-40d1-486e-9c72-8d906266f517/steps/0ed16983-68cd-4821-8034-8f8bb329caf4/149b3c8a-7734-412b-8996-5123ca3468de.png?crop=focalpoint&fit=crop&fp-x=0.3305&fp-y=0.6234&fp-z=3.0719&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=565&mark-y=408&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz02OSZoPTY5JmZpdD1jcm9wJmNvcm5lci1yYWRpdXM9MTA%3D)


### 9. Type "prepare-workflow"
![Step 9 screenshot](https://images.tango.us/workflows/55d4c68e-40d1-486e-9c72-8d906266f517/steps/f01e1a56-e668-4146-8e62-df5da33b0909/46c0f48e-08de-419f-9f72-881b7d2f2b12.png?crop=focalpoint&fit=crop&fp-x=0.5141&fp-y=0.6830&fp-z=1.6584&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=299&mark-y=413&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz02MDMmaD01OSZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 10. Click on Propose changes
![Step 10 screenshot](https://images.tango.us/workflows/55d4c68e-40d1-486e-9c72-8d906266f517/steps/16ea98c0-70c0-433b-abf8-6d35fd9a5b7c/1bf4e7ec-9ab5-4a1a-99b5-3501b5d8e9dd.png?crop=focalpoint&fit=crop&fp-x=0.6205&fp-y=0.7521&fp-z=2.3983&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=432&mark-y=398&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz0zMzcmaD05MCZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 11. Click on base: main
![Step 11 screenshot](https://images.tango.us/workflows/55d4c68e-40d1-486e-9c72-8d906266f517/steps/f1e80952-dbfe-47b3-a222-c0dc664f2100/02526868-8239-4333-9676-d491ee485174.png?crop=focalpoint&fit=crop&fp-x=0.0969&fp-y=0.2479&fp-z=2.6366&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=181&mark-y=398&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz0yNTEmaD04OSZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 12. Click on main…
![Step 12 screenshot](https://images.tango.us/workflows/55d4c68e-40d1-486e-9c72-8d906266f517/steps/d52edf03-43de-4859-9a56-f67710c5b7c8/546d3995-ce1c-4554-8241-615b0b91452a.png?crop=focalpoint&fit=crop&fp-x=0.1782&fp-y=0.4154&fp-z=1.8512&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=129&mark-y=405&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz01MzQmaD03NSZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 13. Click on Create pull request
![Step 13 screenshot](https://images.tango.us/workflows/55d4c68e-40d1-486e-9c72-8d906266f517/steps/5bf714c6-71a2-4a9b-8a40-fdf986556551/fd12c702-7943-4091-939d-3e46afddbb8d.png?crop=focalpoint&fit=crop&fp-x=0.8987&fp-y=0.3287&fp-z=2.9193&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=614&mark-y=388&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz00NjImaD0xMTAmZml0PWNyb3AmY29ybmVyLXJhZGl1cz0xMA%3D%3D)


### 14. Click on Create pull request
![Step 14 screenshot](https://images.tango.us/workflows/55d4c68e-40d1-486e-9c72-8d906266f517/steps/76845072-c8ab-4415-b626-5b8201f75f59/89396554-841e-4ac1-b6d9-e80cceb71979.png?crop=focalpoint&fit=crop&fp-x=0.6221&fp-y=0.8096&fp-z=2.3197&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=418&mark-y=451&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTYlMkNGRjc0NDImdz0zNjUmaD04NyZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)

# [Managing Secrets and Variables in GitHub Actions](https://app.tango.us/app/workflow/be8b220c-72bf-44da-8094-aac7667c044d?utm_source=markdown&utm_medium=markdown&utm_campaign=workflow%20export%20links)
secrets.STAGING
secrets.STAGE_SERVER_HOST
secrets.STAGE_SERVER_KEY_SSH

Note that all of secret key in Github Action workflow must set up on Settings for each repo before use it in Github Action.

### 1. Click on Settings
![Step 1 screenshot](https://images.tango.us/workflows/be8b220c-72bf-44da-8094-aac7667c044d/steps/152ff14d-4637-4fba-ba98-d8c09ecaa25b/b50e8fd2-1b7d-4607-bc75-9cb1c07a619d.png?crop=focalpoint&fit=crop&fp-x=0.5674&fp-y=0.0825&fp-z=2.7289&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=491&mark-y=128&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTQlMkNGRjc0NDImdz0yMTgmaD04MCZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 2. Click on Secrets and variables
![Step 2 screenshot](https://images.tango.us/workflows/be8b220c-72bf-44da-8094-aac7667c044d/steps/4aa07165-edde-4bb4-ae20-bd1b4f3cf65a/d9f7f2b7-8390-4241-9945-22709b06915f.png?crop=focalpoint&fit=crop&fp-x=0.2013&fp-y=0.7258&fp-z=2.0233&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=253&mark-y=341&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTQlMkNGRjc0NDImdz00NzImaD02MiZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 3. Click on Actions
![Step 3 screenshot](https://images.tango.us/workflows/be8b220c-72bf-44da-8094-aac7667c044d/steps/f3050375-c20a-445f-82fb-dc059f65b576/97d5d962-719d-4aee-8684-9ec0b4ef52ff.png?crop=focalpoint&fit=crop&fp-x=0.2013&fp-y=0.7588&fp-z=2.0233&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=253&mark-y=350&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTQlMkNGRjc0NDImdz00NzImaD02MiZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 4. Click on New repository secret
![Step 4 screenshot](https://images.tango.us/workflows/be8b220c-72bf-44da-8094-aac7667c044d/steps/bab0a909-2637-43b2-b5ba-86a396c71151/b6172770-d6c1-490d-bf18-7e13c5b98b3a.png?crop=focalpoint&fit=crop&fp-x=0.5565&fp-y=0.7536&fp-z=2.4095&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=434&mark-y=335&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTQlMkNGRjc0NDImdz0zMzMmaD03NCZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 5. Type "STAGING"
![Step 5 screenshot](https://images.tango.us/workflows/be8b220c-72bf-44da-8094-aac7667c044d/steps/d1c7663e-a15e-422a-8bbc-89697a887ff9/679446a1-6989-49be-abf2-5576699b9eba.png?crop=focalpoint&fit=crop&fp-x=0.5565&fp-y=0.2330&fp-z=1.4464&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=170&mark-y=228&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTQlMkNGRjc0NDImdz04NjEmaD00NCZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 6. Type "TEST=123"
![Step 6 screenshot](https://images.tango.us/workflows/be8b220c-72bf-44da-8094-aac7667c044d/steps/8c5388e7-5c4e-44b2-8ea1-c00880719c5b/654879e4-825a-4b8c-a5b0-64c5fcb48b38.png?crop=focalpoint&fit=crop&fp-x=0.5565&fp-y=0.3892&fp-z=1.4464&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=170&mark-y=253&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTQlMkNGRjc0NDImdz04NjEmaD0yMzgmZml0PWNyb3AmY29ybmVyLXJhZGl1cz0xMA%3D%3D)


### 7. Click on Add secret
![Step 7 screenshot](https://images.tango.us/workflows/be8b220c-72bf-44da-8094-aac7667c044d/steps/02d3c3ff-170b-48d2-8da7-692bcd31f0df/a7b13bbd-88d3-4467-bd03-a3e52c99e408.png?crop=focalpoint&fit=crop&fp-x=0.3425&fp-y=0.5206&fp-z=2.7194&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=489&mark-y=330&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTQlMkNGRjc0NDImdz0yMjEmaD04MyZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 8. Click on New repository secret
![Step 8 screenshot](https://images.tango.us/workflows/be8b220c-72bf-44da-8094-aac7667c044d/steps/0fcf3520-d9ed-4999-90eb-0028d7b08da2/f9f356e2-587d-4310-b2eb-ad77c91b1816.png?crop=focalpoint&fit=crop&fp-x=0.7470&fp-y=0.7062&fp-z=3.1803&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=381&mark-y=323&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTQlMkNGRjc0NDImdz00MzkmaD05OCZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 9. Paste "STAGE_SERVER_HOST" into input
![Step 9 screenshot](https://images.tango.us/workflows/be8b220c-72bf-44da-8094-aac7667c044d/steps/9216c4c4-d4d3-4958-9029-db61dc2f40a0/91307809-6426-4a1b-80e4-1179732fdbe2.png?crop=focalpoint&fit=crop&fp-x=0.5565&fp-y=0.2330&fp-z=1.4464&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=170&mark-y=228&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTQlMkNGRjc0NDImdz04NjEmaD00NCZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 10. Type "abc-ap-south-east-1.ec2.com"
![Step 10 screenshot](https://images.tango.us/workflows/be8b220c-72bf-44da-8094-aac7667c044d/steps/bf69cc93-73f6-4dcd-8267-4c14ec32b2f3/07bca5c9-9a5a-4a79-84ab-696a6497f1cf.png?crop=focalpoint&fit=crop&fp-x=0.5565&fp-y=0.3892&fp-z=1.4464&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=170&mark-y=253&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTQlMkNGRjc0NDImdz04NjEmaD0yMzgmZml0PWNyb3AmY29ybmVyLXJhZGl1cz0xMA%3D%3D)


### 11. Click on Add secret
![Step 11 screenshot](https://images.tango.us/workflows/be8b220c-72bf-44da-8094-aac7667c044d/steps/b2dc4ffd-91da-4154-9a04-46654ac26a76/a7a68378-c11a-40d0-ade3-b2e18bd9554c.png?crop=focalpoint&fit=crop&fp-x=0.3425&fp-y=0.5206&fp-z=2.7194&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=489&mark-y=330&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTQlMkNGRjc0NDImdz0yMjEmaD04MyZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 12. Click on New repository secret
![Step 12 screenshot](https://images.tango.us/workflows/be8b220c-72bf-44da-8094-aac7667c044d/steps/bec280ac-7b6e-4a8d-b838-56a8d7505788/07c74449-d98d-40d1-83fd-845429982436.png?crop=focalpoint&fit=crop&fp-x=0.7470&fp-y=0.7062&fp-z=3.1803&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=381&mark-y=323&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTQlMkNGRjc0NDImdz00MzkmaD05OCZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 13. Paste "STAGE_SERVER_KEY_SSH" into input
![Step 13 screenshot](https://images.tango.us/workflows/be8b220c-72bf-44da-8094-aac7667c044d/steps/90767e80-8684-40f4-96cc-4d5c208ef0cc/ab4ff8fb-f078-4d7f-9425-592a9d3211fe.png?crop=focalpoint&fit=crop&fp-x=0.5565&fp-y=0.2330&fp-z=1.4464&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=170&mark-y=228&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTQlMkNGRjc0NDImdz04NjEmaD00NCZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)


### 14. Type "Your server key ssh copy from file pem. Must use vscode for copy key properly, don't use notepad or text editor"
![Step 14 screenshot](https://images.tango.us/workflows/be8b220c-72bf-44da-8094-aac7667c044d/steps/efa7b83f-5418-4912-8e0a-3c5a5ec5cfb8/c8ab6524-583e-49a7-9868-099993565b5e.png?crop=focalpoint&fit=crop&fp-x=0.5565&fp-y=0.3892&fp-z=1.4464&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=170&mark-y=253&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTQlMkNGRjc0NDImdz04NjEmaD0yMzgmZml0PWNyb3AmY29ybmVyLXJhZGl1cz0xMA%3D%3D)


### 15. Click on Add secret
![Step 15 screenshot](https://images.tango.us/workflows/be8b220c-72bf-44da-8094-aac7667c044d/steps/67f9803e-5a8b-46ca-aa39-c3ce527d901d/2916b5c7-f9f4-4778-870b-5cf5058fee07.png?crop=focalpoint&fit=crop&fp-x=0.3425&fp-y=0.5206&fp-z=2.7194&w=1200&border=2%2CF4F2F7&border-radius=8%2C8%2C8%2C8&border-radius-inner=8%2C8%2C8%2C8&blend-align=bottom&blend-mode=normal&blend-x=0&blend-w=1200&blend64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL21hZGUtd2l0aC10YW5nby13YXRlcm1hcmstdjIucG5n&mark-x=489&mark-y=330&m64=aHR0cHM6Ly9pbWFnZXMudGFuZ28udXMvc3RhdGljL2JsYW5rLnBuZz9tYXNrPWNvcm5lcnMmYm9yZGVyPTQlMkNGRjc0NDImdz0yMjEmaD04MyZmaXQ9Y3JvcCZjb3JuZXItcmFkaXVzPTEw)
