# 🚀 To-Do List Application Deployment Using Docker, Kubernetes & AWS EC2

## 📌 Project Overview

This project demonstrates the deployment of a To-Do List web application using Docker and Kubernetes on AWS EC2.

The application is containerized using Docker, the Docker image is stored in Docker Hub, and Kubernetes is used to deploy and manage the application on an AWS EC2 instance using K3s.

The application is accessible through a public IP address using a Kubernetes NodePort Service.

## 🎯 Project Objectives

- Develop a simple To-Do List web application.
- Containerize the application using Docker.
- Push the Docker image to Docker Hub.
- Install Kubernetes using K3s on AWS EC2.
- Deploy the application using Kubernetes Deployment.
- Expose the application using Kubernetes NodePort Service.
- Access the application through a public IP address.

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| HTML | Application structure |
| CSS | Application styling |
| JavaScript | Application functionality |
| Docker | Containerization |
| Docker Hub | Docker image storage |
| Kubernetes | Container orchestration |
| K3s | Lightweight Kubernetes distribution |
| AWS EC2 | Cloud deployment |
| Git | Version control |
| GitHub | Source code repository |

## 📂 Project Structure

```text
todo-devops/
│
├── index.html
├── style.css
├── script.js
├── Dockerfile
├── todo-deployment.yaml
├── todo-service.yaml
└── README.md
```

## 🏗️ Architecture

```text
Developer
   |
   v
GitHub Repository
   |
   v
Docker Build
   |
   v
Docker Hub
   |
   v
AWS EC2
   |
   v
K3s Kubernetes Cluster
   |
   v
Kubernetes Deployment
   |
   v
Application Pods
   |
   v
NodePort Service
   |
   v
Browser Access
```

## 🚀 Implementation Steps

### Step 1: Clone the GitHub Repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
```

Navigate to the project directory:

```bash
cd todo-devops
```

### Step 2: Build the Docker Image

Build the Docker image using the Dockerfile:

```bash
docker build -t bhavana029/todo-devops:v2 .
```

### Step 3: Login to Docker Hub

```bash
docker login
```

Enter your Docker Hub username and password or access token.

### Step 4: Push the Docker Image

```bash
docker push bhavana029/todo-devops:v2
```

Docker Hub repository:

https://hub.docker.com/r/bhavana029/todo-devops

### Step 5: Install K3s on AWS EC2

Connect to the EC2 instance using SSH.

Install K3s:

```bash
curl -sfL https://get.k3s.io | sh -
```

Check the K3s service:

```bash
sudo systemctl status k3s
```

Check Kubernetes nodes:

```bash
sudo kubectl get nodes
```

### Step 6: Create Kubernetes Deployment

Create the deployment YAML file:

```bash
sudo nano todo-deployment.yaml
```

Add the following configuration:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: todo-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: todo
  template:
    metadata:
      labels:
        app: todo
    spec:
      containers:
        - name: todo-container
          image: bhavana029/todo-devops:v2
          ports:
            - containerPort: 80
```

Apply the deployment:

```bash
sudo kubectl apply -f todo-deployment.yaml
```

Verify the deployment:

```bash
sudo kubectl get deployments
```

Check the pods:

```bash
sudo kubectl get pods
```

### Step 7: Create Kubernetes NodePort Service

Create the service YAML file:

```bash
sudo nano todo-service.yaml
```

Add the following configuration:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: todo-service
spec:
  type: NodePort
  selector:
    app: todo
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30080
```

Apply the service:

```bash
sudo kubectl apply -f todo-service.yaml
```

Verify the service:

```bash
sudo kubectl get services
```

### Step 8: Configure AWS Security Group

Configure the EC2 Security Group inbound rules.

| Type | Port | Purpose |
|---|---|---|
| SSH | 22 | Connect to EC2 |
| HTTP | 80 | Docker application access |
| Custom TCP | 30080 | Kubernetes NodePort access |

For better security, restrict SSH and NodePort access to your IP address when possible.

### Step 9: Verify Application Deployment

Check Kubernetes pods:

```bash
sudo kubectl get pods -o wide
```

Check the deployment:

```bash
sudo kubectl get deployments
```

Check the service:

```bash
sudo kubectl get services
```

Test the application from EC2:

```bash
curl http://localhost:30080
```

If the application returns HTML successfully, the Kubernetes Service is responding.

### Step 10: Access the Application

Open the following URL in your browser:

```text
http://<YOUR_EC2_PUBLIC_IP>:30080
```

Replace `<YOUR_EC2_PUBLIC_IP>` with your current EC2 public IPv4 address.

## 📊 Project Results

- Successfully containerized the To-Do List application using Docker.
- Published the Docker image to Docker Hub.
- Installed K3s on AWS EC2.
- Created a Kubernetes Deployment.
- Deployed two application pods.
- Created a NodePort Service on port 30080.
- Verified the application using curl.
- Successfully accessed the application through the EC2 public IP.

## 🔄 Updating the Application

When application code changes:

1. Update the source code.
2. Build a new Docker image.
3. Push the updated image to Docker Hub.
4. Update the Kubernetes deployment to use the new image.

Example:

```bash
docker build -t bhavana029/todo-devops:v3 .
```

```bash
docker push bhavana029/todo-devops:v3
```

Update the image in the Kubernetes Deployment YAML to `v3`, then apply:

```bash
sudo kubectl apply -f todo-deployment.yaml
```

Check the rollout:

```bash
sudo kubectl rollout status deployment/todo-deployment
```

**Note:** GitHub code updates do not automatically update Docker Hub unless a CI/CD workflow is configured.

## 📚 What I Learned

- Git and GitHub fundamentals.
- Docker image creation and containerization.
- Docker Hub image management.
- AWS EC2 instance configuration.
- K3s installation and Kubernetes cluster management.
- Kubernetes Deployments and Pods.
- Kubernetes Services and NodePort.
- AWS Security Group configuration.
- Application deployment and troubleshooting.

## 🔮 Future Enhancements

- Implement Jenkins CI/CD pipeline.
- Automate Docker image builds.
- Integrate GitHub Webhooks.
- Configure automatic Kubernetes deployment.
- Implement monitoring using Prometheus and Grafana.
- Configure HTTPS using a domain and TLS certificate.
- Improve application security and deployment automation.

## 👩‍💻 Author

**Bhavana Mekala**

GitHub: https://github.com/Bhavana029

Docker Hub: https://hub.docker.com/r/bhavana029/todo-devops

## ⭐ Conclusion

This project demonstrates the deployment of a containerized web application using Docker and Kubernetes on AWS EC2.

It provides practical experience with containerization, cloud infrastructure, Kubernetes orchestration, and application deployment.
