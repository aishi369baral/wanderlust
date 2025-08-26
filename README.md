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






