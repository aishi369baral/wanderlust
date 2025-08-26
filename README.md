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

- <b>Create 1 Master machine on AWS with 2CPU, 8GB of RAM (t2.large) and 29 GB of storage and install Docker on it.</b>
#
- <b>Open the below ports in security group of master machine</b>
<img width="1900" height="766" alt="Ports_ToBe_Opened_Automate" src="https://github.com/user-attachments/assets/35b2ef7b-1ac6-4e35-bd20-ac7e09417348" />

> [!Note]
> We are creating this master machine because we will configure Jenkins master, eksctl, EKS cluster creation from here.

Install & Configure Docker by using below command, "NewGrp docker" will refresh the group config hence no need to restart the EC2 machine.

Update Packages:
```bash
sudo apt-get update
```

Install dependencies
```bash
sudo apt-get install -y ca-certificates curl gnupg lsb-release
```

Add Docker’s official GPG key
```bash
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

Set up Docker repository
```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

Update package index again
```bash
sudo apt-get update
```

Install Docker Engine, CLI, and containerd
```bash
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Verify Docker installation
```bash
docker --version
```

Verify Docker Compose installation
```bash
docker compose version
```

Add $USER to the docker group and update the group
```bash
sudo usermod -aG docker $USER && newgrp docker
```

<b>Check Docker Working</b>

<img width="1152" height="648" alt="dockerWorking_properly" src="https://github.com/user-attachments/assets/8004d427-fced-40b7-a992-32a8bf973314" />











