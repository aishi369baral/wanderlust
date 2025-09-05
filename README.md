# Wanderlust - Your Ultimate Travel Blog 🌍✈️

WanderLust is a simple MERN travel blog website ✈ 

![Preview Image](https://github.com/krishnaacharyaa/wanderlust/assets/116620586/17ba9da6-225f-481d-87c0-5d5a010a9538)
#

# Wanderlust Mega Project End to End Implementation

### In this project, we will see how to deploy an end to end three tier MERN stack application on EKS cluster.
#
### <mark>Project Deployment Flow:</mark>

![DevSecOps+GitOps](https://github.com/user-attachments/assets/80d540ea-7884-4a62-b726-c8d31ab7cb0b)

#

## Tech stack used in this project:
- GitHub (Code)
- Docker (Containerization)
- Jenkins (CI)
- OWASP (Dependency check)
- SonarQube (Quality)
- Trivy (Filesystem Scan)
- ArgoCD (CD)
- Redis (Caching)
- AWS EKS (Kubernetes)
- Helm (Monitoring using grafana and prometheus)

### How pipeline will look after deployment:
- <b>CI pipeline to build and push</b>
<img width="1911" height="987" alt="CI_Full_StageView" src="https://github.com/user-attachments/assets/b16c8706-ac3c-4c09-b88f-390686b22a8c" />

- <b>CD pipeline to update application version</b>
<img width="1916" height="949" alt="CD_Passed" src="https://github.com/user-attachments/assets/75243c60-73be-4e37-ad60-100c01d6fe11" />

- <b>ArgoCD application for deployment on EKS</b>
<img width="1905" height="961" alt="App_Status_Argocd" src="https://github.com/user-attachments/assets/5bbf732d-dfb0-4b52-811e-60684955babb" />

#
> [!Important]
> Below table showcases Tools used.

| Tech stack    | Installation |
| -------- | ------- |
| Jenkins Master | Install and configure Jenkins    |
| eksctl | Install eksctl     |
| Argocd | Install and configure ArgoCD     |
| Jenkins Setup | Install and configure Jenkins Node    |
| OWASP setup | Install and configure OWASP     |
| SonarQube | Install and configure SonarQube     |
| Email Notification Setup | Email notification setup     |
| Monitoring | Prometheus and grafana setup using helm charts
| Clean Up | Clean up    |
#

### Pre-requisites to implement this project:
#

> [!Note]
> This project will be implemented on North California region (us-east-2).

- <b>Create 1 Master machine on AWS with 2CPU, 8GB of RAM (t2.large) and 29 GB of storage using <mark>Terraform</mark> and install Docker on it.</b>
1. Clone the Github repo to local
Go inside the terraform folder:
```bash
cd terraform
```
2. Verify terraform installation:
```bash
terraform --version
```
<img width="918" height="141" alt="terraform-version" src="https://github.com/user-attachments/assets/ae60413c-d771-4cc2-90d9-597ec9241bdf" />

3. Verify aws cli installation:
```bash
aws --version
```
<img width="1636" height="88" alt="aws--version" src="https://github.com/user-attachments/assets/f218efa0-3600-44d9-a0c7-138b318c85e1" />

4. Make IAM user with administrator access and generate secret access key:
   <img width="1909" height="885" alt="IAM_user_withAdministratorAccess_InfraTerraform" src="https://github.com/user-attachments/assets/319504aa-b58f-4dcd-89d4-58719f812410" />
   <img width="1910" height="695" alt="IAM_user_accesskey" src="https://github.com/user-attachments/assets/dc334b26-72b0-45f7-878d-85ec58cc4350" />
5. Configure Terraform using the IAM user:
   ```bash
   aws configure
   ```
   <img width="975" height="149" alt="awsConfigure_terra-admin" src="https://github.com/user-attachments/assets/9010972f-2ff9-4cdc-bfba-a9c230a948bf" />

> [!Note]
> "Terraform is configured with an AWS IAM user (using access key and secret key) to provision infrastructure on AWS."

6. Generate Private and Public key which will used to ssh into the Master Machine that will be created:
   ```bash
   ssh-keygen
   ```
   <img width="1470" height="779" alt="ssh-keygen" src="https://github.com/user-attachments/assets/02f7f669-9d12-44a7-9ca7-c677cf5a1427" />
> [!Note]   
> Upadte the public key location in the ec2.tf file

7. Run the following commands:
   ```bash
   terraform init
   terraform plan
   terraform apply
   ```
   <img width="745" height="344" alt="terraform init" src="https://github.com/user-attachments/assets/2fbbf2f1-edbe-40e7-972a-f8da07dc1305" />
   <img width="1495" height="801" alt="terraformPlan_4resources" src="https://github.com/user-attachments/assets/073505b2-472a-42b0-b0dc-b3fafde6d58c" />
   <img width="1490" height="781" alt="terraformApply_4Resources_created" src="https://github.com/user-attachments/assets/b86a70cd-142c-40f4-8abf-8c513d9d5b7d" />

8. Resources Provisioned/added so far:
   1. Master Machine (Automate).
   2. Security group for the master machine.
   3. Key-Pair added to allow ssh into the master machine.

<img width="1906" height="966" alt="MasterMachine(Automate)_created" src="https://github.com/user-attachments/assets/ee4dd6d7-f1ba-4cc0-8c24-f989f05c65ea" />
<img width="1908" height="924" alt="SecurityGroup(allow TLS)Added_WithPortsOpened_Ingress" src="https://github.com/user-attachments/assets/5a5cf907-dffb-46b8-a7f5-ee302e48fa25" />
<img width="1908" height="504" alt="KeyPair_Added_SSH" src="https://github.com/user-attachments/assets/0801e6b1-f857-4802-a00f-93ccb0fecae4" />

<b>SSH into the Master Machine and Open the below ports in security group</b>
<img width="1900" height="766" alt="Ports_ToBe_Opened_Automate" src="https://github.com/user-attachments/assets/35b2ef7b-1ac6-4e35-bd20-ac7e09417348" />

#
> [!Important]
> Below table showcases Tools need to be installed in the Master Machine.

| Tech stack    | Installation |
| -------- | ------- |
| Docker | Install docker |
| Java | Install java |
| Jenkins Master | Install and configure Jenkins    |
| eksctl | Install eksctl     |
| Argocd | Install and configure ArgoCD     |
| Jenkins Setup | Install and configure Jenkins Node    |
| OWASP setup | Install and configure OWASP     |
| SonarQube | Install and configure SonarQube     |

#

<b>Install & Configure Docker by using below command, "NewGrp docker" will refresh the group config hence no need to restart the EC2 machine.</b>

Update Packages:
```bash
sudo apt-get update
sudo apt-get install -y ca-certificates curl gnupg lsb-release
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
docker --version
docker compose version
sudo usermod -aG docker $USER && newgrp docker
```

Check Docker Working

<img width="1152" height="648" alt="dockerWorking_properly" src="https://github.com/user-attachments/assets/8004d427-fced-40b7-a992-32a8bf973314" />
#

- <b id="Jenkins">Install and configure Jenkins (Master machine)</b>

Install Java (Jenkins needs Java)
```bash
sudo apt update
sudo apt install -y fontconfig openjdk-17-jdk
java -version
```

Add Jenkins repository and install
Add Jenkins key
```bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
```

Add Jenkins repo
```bash
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | \
  sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
```

Update and install Jenkins
```bash
sudo apt update
sudo apt install -y jenkins
```

Start and enable Jenkins
```bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
sudo systemctl status jenkins
```

Open Firewall (port 8080 for Jenkins UI)


Get Initial Admin Password
```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

👉 Copy this password.

Access Jenkins UI

Open browser: http://<your-server-ip>:8080
Paste the password from Step 5

Install suggested plugins

Create your first admin user

Jenkins is ready 🎉
























