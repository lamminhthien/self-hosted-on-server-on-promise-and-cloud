# Tutorial: Self-Hosted Node.js App Deployment on AWS EC2 or On-Premise and other Cloud Servers provider with CI/CD
# Section
I. [Create an EC2 on AWS](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud#attach-static-ip-may-be-in-other-cloud-platform-in-vietnam-static-ip-will-be-available-by-default)

II. [Create and attach Elastic IPs to EC2](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud#attach-static-ip-may-be-in-other-cloud-platform-in-vietnam-static-ip-will-be-available-by-default)

III. [Create Github Action Workflow](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud#setup-github-action-workflow-first)

IV. [Managing Secrets and Variables in GitHub Actions](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud#managing-secrets-and-variables-in-github-actions)

V. [Prepare Dockerfile and docker-compose-ssh.yml](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/blob/main/README.md#prepare-dockerfile-and-docker-compose)

VI. [Ready for deploy](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/blob/main/README.md#prepare-dockerfile-and-docker-compose)

VII. [Setup Security Group to open port for testing](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/blob/main/README.md#after-complete-all-we-can-merge-pull-request-set-up-github-action-and-ready-for-deploy-to-server-ec2)

VIII [Setup Portainer for monitor, manage and log on Docker Containers](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/blob/main/README.md#setup-portainer-ce-for-manager-logging-docker-container)

IX [Setup Domain on namecheap](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/tree/main#setup-domain-on-namecheap)

X [Setup SSL](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/blob/main/README.md#setup-ssl)

XI [Cloudwatch Alarm CPU High and send email (Youtube) (AWS Only)](https://www.youtube.com/watch?v=mcV1idfCXOo)

XII [Promethus + Grafana to monitor CPU, RAM, etc (AWS or Any Cloud Provider like ViettelHost , Vietnix)](https://viblo.asia/p/monitor-cach-giam-sat-he-thong-don-gian-voi-prometheus-va-grafana-BQyJKjW54Me)

## I. Create and EC2 on AWS

### 1. Type "EC2" and Select it.
![Step 1](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/f267946a-9653-4f66-a5e4-5a310fe5e2cc)

### 3. Click on Launch instance
![Launch Instance](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/5c422d66-b368-433b-b64a-2cc2dbda98e6)

### 4. Type a name for your server
![Type a name for your server](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/cd8abe02-ec57-481b-b12c-06052f775d89)

### 5. Choose Ubutnu and Choose Amazon Machine Image (AMI)
![Choose AMI](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/a2b0d0c3-063b-4827-91f5-8369cca28d28)

### 6. Choose Instance type
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/6776335a-4a28-4b6e-83ec-313a7395f30b)

### 7. Searching t3.medium for server with 2vCPU and 4GB Ram.
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/fd6651d9-90ad-4bd9-9fed-ee610ae5a668)

### 8. Click on t3.medium. If you want more RAM, you can choose t3.large.
### 9. Key pair (login). Click create new key pair. This will use for login to server and using in CI/CD
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/662687f1-d21b-40b8-9a8f-e0d236433eb4)

### 10. Type Key pair name. Example "self-hosted"
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/c4983642-cb88-47eb-9390-cd3e603d3a2f)

### 11. Click on Create key pair in this popup
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/19a20a0a-ecf7-4f3a-aa57-6f7468c41d96)

### 12. Check Allow HTTPS traffic from the internet (For SSL later)
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/3c23f45b-fcf0-4184-88ff-490c6096814e)

### 13. Check Allow HTTP traffic from the internet (For port 80)
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/93ff80a9-7247-4f05-ad90-77ff48cef859)

### 14. Choose storage size for SSD in "EBS Volumes". Example 32GB

### 15. Change Volume type (SSD Type).
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/a28f5f8c-b129-4fdd-95e9-1da0cfdc9f05)

### 16. Click on General purpose SSD (gp3)…
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/d12dd355-9de5-4296-8b26-2f48155a846e)

### 17. Click on Advanced details. To setup terminate protection, Cloudwatch Detailed Monitoring and UserData (For preinstall some of software we need)
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/72f03804-500d-4521-a97c-2be55828e2f3)

### 18. Enable Termination protection
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/94eb22dd-26b9-4779-92f8-caa483892d4e)

### 19. Enable Detailed CloudWatch monitoring
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/1a7f89cb-46f4-4192-80c9-0499407f698e)

### 20. Scrolldown to User data - optional

Add this content below:

```sh
#!/bin/bash
sudo apt update -y

# Install Docker using Snap
sudo snap install docker

# Grant permission for run Docker without root user
sudo chmod 666 /var/run/docker.sock
```

![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/3a17ef63-65e8-48c4-a059-ec1873aba4b5)

### 23. Click on Launch instance
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/b8ad8118-7cf7-4c95-95d6-8596b16f0ffe)

## Attach Static IP (May be in other cloud platform in Vietnam, Static IP will be available by default)

### 1. Type "Elastic IPs" in Search box
### 2. Click on Elastic IPs
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/77fc6736-4b9e-4dac-8738-9f45e0a7b45d)

### 3. Click on Allocate Elastic IP address
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/224f6fba-d0f6-4c30-a3de-566a5d0f021a)

### 4. Click on Allocate
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/e66b795a-d9dc-40a5-bcad-a756a2dc0be5)

### 5. Click on Associate this Elastic IP address
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/a084a730-b612-4ab4-83ea-a422be6587b5)

### 6. Make sure Resource type is Instance. Then choose instance in Instance Select
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/fcb046f4-04e0-4b2d-bc8f-72bf590aa233)

### 7. Choose your suitable instance
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/fe6ee9f8-673c-4b31-bf29-442cd83936c7)

### 8. Click on Associate
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/0ec43c80-d5bc-4ad5-a5de-eb5ced99a4c1)

### 9. On Allocated IPv4 address. Click copy IPv4 address to use for setup domain name, CI/CD,...
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/c55ba4ec-e322-48a3-8f9d-6cc061e3f110)


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
      - `sudo docker load --inputnestjs-22.tar`: Loads the Docker image from the tar file.
      - `sudo docker-compose up -d --force-recreate`: Starts the project using Docker Compose, recreating containers if necessary.
      - `rm -rfnestjs-22.tar`: Removes the Docker image tar file from the server.

This workflow automates the process of building a Docker image, copying it to a server, and deploying the project using Docker Compose. It ensures consistency and simplifies the deployment process in a staging environment.

### 1. Click on Actions
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/eb9d20a8-f33b-4193-b257-bbcbd8b8228b)

### 2. Click on set up a workflow yourself 
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/0db9bdad-8069-475a-9954-3b204df2228c)

### 3. Type "deploy.staging.yml"
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/64ce0b2c-b370-47c2-9bf1-8e60cab08937)

### 4. Paste selected text into element
You can get content from folder .github/workflows
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/4037672f-11c6-4f9c-a997-35cc3d42fe3c)

### 6. Click on Commit changes...
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/a2d6d12e-76c5-4ebf-9c25-18140e660f5c)

### 7. Click on Commit message
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/abed567c-93f5-4e4f-9791-6079d674ad96)

### 8. Select Create a new branch for this commit and start a pull request…
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/1e01db64-fa40-4265-a273-cc3211287ae0)

### 9. Type "prepare-workflow"
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/1ed1c61a-cc55-4a06-aa24-0b872b5ab9c5)


### 10. Click on Propose changes
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/9362cc76-c807-43cb-b45d-f593357b3898)

### 11. Click on base: main
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/fc390785-23e0-4ab3-90d4-7e741b4c5667)

### 12. Click on main…
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/cd64fe58-a591-4112-801e-6ad3b16b7e95)

### 13. Click on Create pull request
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/7ce5e6a6-e8e9-4de4-b744-effb62104db8)

### 14. Click on Create pull request
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/d2832112-5bce-45db-a6b2-d131a46f9399)

# [Managing Secrets and Variables in GitHub Actions](https://app.tango.us/app/workflow/be8b220c-72bf-44da-8094-aac7667c044d?utm_source=markdown&utm_medium=markdown&utm_campaign=workflow%20export%20links)
Currently, we will set up for the following keys:

 - secrets.STAGING
 - secrets.STAGE_SERVER_HOST
 - secrets.STAGE_SERVER_KEY_SSH

Note that all of secret key in Github Action workflow must set up on Settings for each repo before use it in Github Action.

### 1. Click on Settings
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/2d23bc3f-f5b3-4b60-a515-2a48320d6349)

### 2. Click on Secrets and variables
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/faa968df-2e8d-4950-92ee-8e0281e634a2)

### 3. Click on Actions
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/ccdf1627-0441-47d0-b9e2-c8b7dcdd140a)

### 4. Click on New repository secret
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/ab3dc4c9-5daf-4e68-897e-c20c946d9a6e)

### 5. Type "STAGING"
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/04339100-1b22-4e18-bb5d-074523fe97f8)

### 6. Type "TEST=123"
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/ee89fa01-1320-4949-9b30-d38373df9d79)

### 7. Click on Add secret
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/ebcb90a6-7adb-43fa-b2c6-bfe0e6d41ecf)

### 8. Click on New repository secret
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/1ed6ceef-c8e7-441d-aabb-900adad6a3c1)

### 9. Paste "STAGE_SERVER_HOST" into input
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/d514cf03-837e-4d1a-88b2-e25f9213397a)

### 10. Type "abc-ap-south-east-1.ec2.com"
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/9e3b6e37-325f-4558-8bce-3d9388763aa9)

### 11. Click on Add secret
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/9f2f6338-6533-453c-b437-766b9a299a35)

### 12. Click on New repository secret
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/b04ba448-fe7d-4a7d-bdba-d9048086ab8f)

### 13. Paste "STAGE_SERVER_KEY_SSH" into input
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/67b68eda-a220-4acc-b773-569906459421)


### 14. Type "Your server key ssh copy from file pem. Must use vscode for copy key properly, don't use notepad or text editor"
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/83b47868-6005-4b41-8d27-dc9f545686dd)


### 15. Click on Add secret
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/9d130217-8093-43a5-8986-8fd71bad6d40)

## Prepare Dockerfile and docker-compose:
Both file are available in this repository.Make sure your image name is the same as tar file name, which created by docker build command in Build Stage in Github Action. You can see some picture below for more detail
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/ed34d906-30b4-4fd0-ba61-feba6fc6439f)

## After complete all, we can merge pull request set up github action and ready for deploy to Server EC2.

## How to open port for testing web, and prepare for using Portainer later, setup Security Group.
### In page detail of EC2, Select Tab "Security". Choose a Security Group.
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/d013095d-d048-48a1-8d28-56ca211299c2)

### Click on Inbound rules
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/061a243e-6164-4ad8-8180-fcf18b5d5a87)

### Click on Edit inbound rules
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/477268b7-d16b-4e14-a3cc-259245186c8c)

### Click Add Rule
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/4177587d-0429-4533-901b-89b1fd725a51)

### Choose Custom TCP
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/a16785bb-101a-41ca-9233-0becc64480c8)

### Choose suitable Port, example 3000
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/3b3a8a8a-f195-442d-b01a-136fd5c2ffea)

### Change CIDR Blocks to 0.0.0.0
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/2c3efdc6-bbd8-4c02-b240-f7e1e51200e6)
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/003e9755-389f-4334-9084-cf71462ede8a)

### Save Rules
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/5e423ae7-1a2b-48b7-a970-5cba9d342b57)


## Setup SSL with Caddy Web Server

## Setup Portainer CE for manager, logging Docker Container:
https://docs.portainer.io/start/install-ce/server/docker/linux#deployment

### Command to setup
```bash
docker volume create portainer_data
docker run -d -p 8000:8000 -p 9000:9000 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```

### Using
http://localhost:9000 or http://<ip_address>:9000

### Login UI
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/98f578bb-9c63-46de-ab27-ba7596337036)

### Main UI
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/bfbbe12e-acd6-469e-a71a-477702d8bedb)

### Container List
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/9f98eeaa-29db-453b-a70c-daa4b171f058)

### View Detail Environment 
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/91b60c82-0b40-4fb0-8b85-b4adf77a01f9)

### Checking status, logs, stat
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/68e75f28-4f17-4d3d-be95-5efe9f06b9be)
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/ce8339a9-9d97-4b10-a915-af56f8ebf179)
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/d6ddc48a-c6ff-46d2-8a53-d1ae1d8429a7)
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/00922dd0-4650-4631-bcb9-079ebd87b45c)


## Setup Domain on Namecheap
### Copy Your Elastic IPs
### Login Namecheap and choose your domain to manage
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/49dea789-30e1-41e2-9642-16a24e854e30)
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/f15756d7-027f-4674-861e-7448778d0b1c)
### Click Advanced DNS
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/6a13a9ae-4418-4aaf-9882-2501e7e7701d)
### Add new Record
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/15a3108d-1441-42b6-b1d1-86b5f8489df3)
### Choose A Record
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/dc30f170-9ce0-42b7-9df3-d2b7988ea5d3)
### Type wildcard domain name: Example "test" mean "test.todooy.com"
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/646f0abe-a3c3-4e62-851d-c343e77ba103)
### Type your Elastic IP which you copied and click green ticked to save
![image](https://github.com/lamminhthien/self-hosted-on-server-on-promise-and-cloud/assets/99172799/3466d433-15bf-4732-b763-50736847de6f)


## Setup SSL
### Connect to your Server:

### Install Caddy web server
```bash
sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https curl &&\
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo gpg --dearmor -o /usr/share/keyrings/caddy-stable-archive-keyring.gpg &&\
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list &&\
sudo apt update -y &&\
sudo apt install caddy -y
```

### Give permission HTTPS for caddy
sudo setcap CAP_NET_BIND_SERVICE=+eip $(which caddy)

### Restart Caddy server for take effect
caddy stop
caddy start

### Create Caddyfile config
mkdir caddy-config && cd caddy-config
sudo nano Caddyfile

```Caddyfile
kuma.thienlam3.line.pm {
		reverse_proxy localhost:3001
}
```
Save this file

### Reload Caddy web server to apply domain name without downtime
caddy reload

### Waiting about 2 to 15 minutes and then cerification obtained appear, and we are done.
## Create S3 with cloud formation
