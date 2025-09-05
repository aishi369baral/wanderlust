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

### Master Machine Creation :
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
> Update the public key location in the ec2.tf file

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
#


#
### Open the below ports in security group in Master Machine:
<img width="1900" height="766" alt="Ports_ToBe_Opened_Automate" src="https://github.com/user-attachments/assets/35b2ef7b-1ac6-4e35-bd20-ac7e09417348" />

### SSH into the Master Machine and install the following in it:
#
> [!Important]
> Below table showcases Tools need to be installed in the Master Machine.

| Tech stack    | Installation |
| -------- | ------- |
| Docker | Install docker |
| Java | Install java |
| Jenkins Master | Install and configure Jenkins    |
| Aws CLI | Configure aws cli |
| kubectl | Install kubectl |
| eksctl | Install eksctl     |
| Trivy | Install trivy |
| SonarQube | Install and configure SonarQube     |
| OWASP setup | Install and configure OWASP     |
| Argocd | Install and configure ArgoCD     |

#

1. Install & Configure **Docker** by using below command, "NewGrp docker" will refresh the group config hence no need to restart the EC2 machine.
>[!Note]
> Docker needs to be installed as through docker we can run the SonarQube Server.

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

<img width="1033" height="119" alt="dockerWorking_properly" src="https://github.com/user-attachments/assets/2392d8a8-4152-4eda-b022-c1cd358590f2" />

#

2. Install and configure **Jenkins** (Master machine):

> [!Note]   
> Install **Java** (Jenkins needs Java)

```bash
sudo apt update
sudo apt install -y fontconfig openjdk-17-jdk
java -version

curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null

echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | \
  sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt update
sudo apt install -y jenkins
sudo systemctl start jenkins
sudo systemctl enable jenkins
sudo systemctl status jenkins
```
#

## check the Java version:
<img width="1324" height="100" alt="java_installed" src="https://github.com/user-attachments/assets/da642ead-ecd3-4273-97d7-d02291838f76" />

## Jenkins Running on Port 8080:
<img width="1898" height="541" alt="Jenkins_Status_Running" src="https://github.com/user-attachments/assets/0721b0c3-43c8-49e8-9802-84c406f8f576" />
#


Open Firewall (port 8080 for Jenkins UI):
<img width="1906" height="750" alt="Jenkins_Port_Openned_8080" src="https://github.com/user-attachments/assets/ecc50fd6-c60e-43f2-9417-f943b1beefe7" />


Get Initial Admin Password

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

👉 Copy this password.

Access Jenkins UI:

Open browser: http://<your-server-ip>:8080

<img width="1911" height="967" alt="Run_Jenkins_Browser_unlock_it" src="https://github.com/user-attachments/assets/0c14ba72-139e-4720-a97a-097cc85565e9" />

Paste the password

Install suggested plugins

<img width="1918" height="967" alt="Jenkins_installSuggestedPlugins" src="https://github.com/user-attachments/assets/5029d5e4-9efd-41c7-925b-c5ec6863ec4b" />


Create your first admin user

Jenkins is ready 🎉


<img width="1908" height="960" alt="Jenkins_Welcome_Window" src="https://github.com/user-attachments/assets/30198521-bd35-476c-9d02-1ac2302fe1ef" />


#


### Creation of EKS Cluster:
>[!Note]
>We need to configure aws cli and install kubectl and eksctl in Master Machine before creating the cluster

1. Configure **Aws Cli**:
 ```bash
  curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
  sudo apt install unzip
  unzip awscliv2.zip
  sudo ./aws/install
  aws configure
  ```

<img width="878" height="155" alt="aws-version_aws-configure" src="https://github.com/user-attachments/assets/a41ad43b-58d5-410c-9a28-7d114b6a8309" />



 2. Install **kubectl** 
  ```bash
  curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.19.6/2021-01-05/bin/linux/amd64/kubectl
  chmod +x ./kubectl
  sudo mv ./kubectl /usr/local/bin
  kubectl version --short --client
  ```


<img width="1661" height="285" alt="kubectl_installed" src="https://github.com/user-attachments/assets/e83eeaa2-b739-40cf-9735-90c97fe7dc0d" />



3. Install **eksctl** 
  ```bash
  curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
  sudo mv /tmp/eksctl /usr/local/bin
  eksctl version
```


<img width="1910" height="164" alt="eksctl_installed" src="https://github.com/user-attachments/assets/fe2e4012-3d43-43db-9346-2ffdd6a44899" />



>[!Note]
>Before creating the cluster check in Cloud Formation if there is any pre-existing cluster with the same name.
>Make sure the ssh-public-key "eks-nodegroup-key is available in your aws account"

  - <b>Create EKS Cluster (Master machine)</b>
  ```bash
  eksctl create cluster --name=wanderlust \
                      --region=us-east-2 \
                      --version=1.30 \
                      --without-nodegroup
  ```

<img width="1456" height="161" alt="EKS_Cluster_Created_WithOutNodes" src="https://github.com/user-attachments/assets/ddef7f17-fc2c-4a6c-91fe-5b9e249d7e8e" />



  - <b>Associate IAM OIDC Provider (Master machine)</b>
  ```bash
  eksctl utils associate-iam-oidc-provider \
    --region us-east-2 \
    --cluster wanderlust \
    --approve
  ```

<img width="1880" height="211" alt="IAM_OIDC_Provider" src="https://github.com/user-attachments/assets/87df34b4-d79f-4168-bf79-4fa6a681cde3" />



  - <b>Create Nodegroup (Master machine)</b>
  ```bash
  eksctl create nodegroup --cluster=wanderlust \
                       --region=us-east-2 \
                       --name=wanderlust \
                       --node-type=t2.large \
                       --nodes=2 \
                       --nodes-min=2 \
                       --nodes-max=2 \
                       --node-volume-size=29 \
                       --ssh-access \
                       --ssh-public-key=eks-nodegroup-key 
  ```

<img width="1486" height="161" alt="added_nodeGroups_to_cluster" src="https://github.com/user-attachments/assets/e39f2009-4f6d-4f83-a65a-13f955d539a0" />


Now the 2 nodes are formed in the cluster:
```bash
kubectl get nodes
```


#




3. Install **Trivy**:
```bash
sudo apt-get install wget apt-transport-https gnupg lsb-release -y
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | sudo apt-key add -
echo deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main | sudo tee -a /etc/apt/sources.list.d/trivy.list
sudo apt-get update -y
sudo apt-get install trivy -y
```


<img width="1370" height="99" alt="trivy_installed" src="https://github.com/user-attachments/assets/ada397b7-5b63-4671-adfa-cd594780eb5b" />


#



4. Install and Configure **SonarQube** Server: 
```bash
docker run -itd --name SonarQube-Server -p 9000:9000 sonarqube:lts-community
```

<img width="1370" height="368" alt="Sonar-qube_installed" src="https://github.com/user-attachments/assets/4cdb0985-8411-4455-83ff-79da0f491f86" />


Access SonarQube Server UI:

Open browser: http://<your-server-ip>:9000


<img width="1902" height="864" alt="Sonar-qube_login" src="https://github.com/user-attachments/assets/5d4e47f5-b2b3-4787-bc47-08e9a9f86b30" />



intial username: admin

initial password: admin

Sonar Qube server is ready 🎉


<img width="1908" height="978" alt="Sonar-qube_welcome" src="https://github.com/user-attachments/assets/62a73df7-abc6-4b7d-ade9-63edf15a84b5" />


#


5. Install the following Jenkins plugins:

- <b>Go to Jenkins Master and click on <mark> Manage Jenkins --> Plugins --> Available plugins</mark> install the below plugins:</b>
  - OWASP
  - SonarQube Scanner
  - Docker
  - Pipeline: Stage View
 
    Click install
    Check box : Restart Jenkins when installation is complete.

#
## Steps to add email notification
- <b id="Mail">Go to your Jenkins Master EC2 instance and allow 465 port number for SMTPS</b>
#
- <b>Now, we need to generate an application password from our gmail account to authenticate with jenkins</b>
  - <b>Open gmail and go to <mark>Manage your Google Account --> Security</mark></b>
> [!Important]
> Make sure 2 step verification must be on

  

  - <b>Search for <mark>App password</mark> and create a app password for jenkins</b>

  
#
- <b> Once, app password is create and go back to jenkins <mark>Manage Jenkins --> Credentials</mark> to add username and password for email notification</b>


# 
- <b> Go back to <mark>Manage Jenkins --> System</mark> and search for <mark>Extended E-mail Notification</mark></b>


### OWASP Dependency-Check installation:
After OWASP plugin is installed, Now move to <mark>Manage jenkins --> Tools</mark>



### Integrate SonarQube to Jenkins: via Tokens
- <b>Login to SonarQube server and create the credentials for jenkins to integrate with SonarQube</b>
  - Navigate to <mark>Administration --> Security --> Users --> Token</mark>


  #
- <b>Now, go to <mark> Manage Jenkins --> credentials</mark> and add Sonarqube credentials:</b>


- <b>Go to <mark> Manage Jenkins --> Tools</mark> and search for SonarQube Scanner installations:</b>

- <b>Go to <mark> Manage Jenkins --> System</mark> and search for SonarQube installations:</b>

>[!Note]
> SonarQube will hit Jenkins to reply back after a job is complete hence we will need a webhook

- <b>Login to SonarQube server, go to <mark>Administration --> Webhook</mark> and click on create </b>

Hence SonarQube must have the Jenkins URL http://<your-server-ip>:9000 to send a reply back to Jenkins on job completion.
    
#
### Jenkins needs Personal Access Token of your Github account to push the updated code in Github Repository: 
- <b> Create Personal Access Token in Github Account:</b>

- <b> Go to <mark> Manage Jenkins --> credentials</mark> and add Github Personal Access Token to push updated code from the pipeline:</b>

> [!Note]
> While adding github credentials add Personal Access Token in the password field.
#

#
### Telling jenkins to  use Shared Library:
- <b> Go to <mark> Manage Jenkins --> System</mark> and search for Global Trusted Pipeline Libraries:</b>

### Add Docker Hub credentials to Jenkins so that it can push built images:
- <b>Navigate to <mark> Manage Jenkins --> credentials</mark> and add credentials for docker login to push docker image:</b>



### Create IAM Role for our Master Machine:
- <b>Go to IAM --> Roles --> Create Role </b>

- <b>Attach the IAM Role to the Master Machine</b>

### Provide Jenkins permission to docker socket so that docker build and push command do not fail
```bash
sudo usermod -aG docker jenkins
sudo systemctl restart jenkins
```


### Create CI CD Pipeline:
- <b>Create a <mark>Wanderlust-CI</mark> pipeline</b>

#
- <b>Create one more pipeline <mark>Wanderlust-CD</mark></b>

### Install and Configure Argo CD :
- <b id="Argo">Install and Configure ArgoCD (Master Machine)</b>
  - <b>Create argocd namespace</b>
  ```bash
  kubectl create namespace argocd
  ```
  - <b>Apply argocd manifest</b>
  ```bash
  kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
  ```
  - <b>Make sure all pods are running in argocd namespace</b>
  ```bash
  watch kubectl get pods -n argocd
  ```
  - <b>Install argocd CLI</b>
  ```bash
  sudo curl --silent --location -o /usr/local/bin/argocd https://github.com/argoproj/argo-cd/releases/download/v2.4.7/argocd-linux-amd64
  ```
  - <b>Provide executable permission</b>
  ```bash
  sudo chmod +x /usr/local/bin/argocd
  ```
  - <b>Check argocd services</b>
  ```bash
  kubectl get svc -n argocd
  ```
  - <b>Change argocd server's service from ClusterIP to NodePort</b>
  ```bash
  kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "NodePort"}}'
  ```
  - <b>Confirm service is patched or not</b>
  ```bash
  kubectl get svc -n argocd
  ```
  - <b> Check the port where ArgoCD server is running and expose it on security groups of a worker node</b>

  - <b>Access it on browser, click on advance and proceed with</b>
  ```bash
  <public-ip-node>:<port>
  ```

  - <b>Fetch the initial password of argocd server</b>
  ```bash
  kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
  ```
  - <b>Username: admin</b>
  - <b> Now, go to <mark>User Info</mark> and update your argocd password
 
### Attach Git Repository to Argo CD:
- <b>Go to <mark>Settings --> Repositories</mark> and click on <mark>Connect repo</mark> </b>


> [!Note]
> Connection should be successful


### Attach your EKS Cluster to Argo CD:
- <b> Go to Master Machine and add our own eks cluster to argocd for application deployment using cli</b>
  - <b>Login to argoCD from CLI</b>
  ```bash
   argocd login   <public-ip-node>:32738 --username admin
  ```

  - <b>Check how many clusters are available in argocd </b>
  ```bash
  argocd cluster list
  ```

  - <b>Get your cluster name</b>
  ```bash
  kubectl config get-contexts
  ```
  - <b>Add your cluster to argocd</b>
  ```bash
  argocd cluster add Wanderlust@wanderlust.us-west-1.eksctl.io --name wanderlust-eks-cluster
  ```
  > [!Tip]
  > Wanderlust@wanderlust.us-west-1.eksctl.io --> This should be your EKS Cluster Name.

  - <b> Once your cluster is added to argocd, go to argocd console <mark>Settings --> Clusters</mark> and verify it</b>

### Add a new App in Argo CD:

- <b>Now, go to <mark>Applications</mark> and click on <mark>New App</mark></b>

> [!Important]
> Make sure to click on the <mark>Auto-Create Namespace</mark> option while creating argocd application


- <b>Congratulations, your application is deployed on AWS EKS Cluster</b>

- <b>Open port 31000 and 31100 on worker node and Access it on browser</b>
```bash
<worker-public-ip>:31000
```

### Email Confirmation that the app has been deployed:
- <b>Email Notification</b>


#
## How to monitor EKS cluster, kubernetes components and workloads using prometheus and grafana via HELM (On Master machine)

- <p id="Monitor">Install Helm Chart</p>
```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
```
```bash
chmod 700 get_helm.sh
```
```bash
./get_helm.sh
```

#
-  Add Helm Stable Charts for Your Local Client
```bash
helm repo add stable https://charts.helm.sh/stable
```

#
- Add Prometheus Helm Repository
```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
```

#
- Create Prometheus Namespace
```bash
kubectl create namespace prometheus
```
```bash
kubectl get ns
```

#
- Install Prometheus using Helm
```bash
helm install stable prometheus-community/kube-prometheus-stack -n prometheus
```

#
- Verify prometheus installation
```bash
kubectl get pods -n prometheus
```

#
- Check the services file (svc) of the Prometheus
```bash
kubectl get svc -n prometheus
```

#
- Expose Prometheus and Grafana to the external world through Node Port
> [!Important]
> change it from Cluster IP to NodePort after changing make sure you save the file and open the assigned nodeport to the service.

```bash
kubectl edit svc stable-kube-prometheus-sta-prometheus -n prometheus
```
![image](https://github.com/user-attachments/assets/90f5dc11-23de-457d-bbcb-944da350152e)
![image](https://github.com/user-attachments/assets/ed94f40f-c1f9-4f50-a340-a68594856cc7)

#
- Verify service
```bash
kubectl get svc -n prometheus
```

#
- Now,let’s change the SVC file of the Grafana and expose it to the outer world
```bash
kubectl edit svc stable-grafana -n prometheus
```
![image](https://github.com/user-attachments/assets/4a2afc1f-deba-48da-831e-49a63e1a8fb6)

#
- Check grafana service
```bash
kubectl get svc -n prometheus
```

#
- Get a password for grafana
```bash
kubectl get secret --namespace prometheus stable-grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
```
> [!Note]
> Username: admin

#
- Now, view the Dashboard in Grafana


#
## Clean Up

- <b id="Clean">Delete eks cluster</b>
```bash
eksctl delete cluster --name=wanderlust --region=us-west-1
```

- <b> terminate the Master Machine</b>
Go to local and cd into terraform folder and run:
```bash
terraform destroy
```
#



























