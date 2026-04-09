# 🚀  Deploying Spring Boot application on Kubernetes (Minikube)

## 📌 Project Overview

This project demonstrates how to deploy a **Spring Boot CRUD application** with a **MySQL database** on **Kubernetes using Minikube**.
The application is containerized using Docker and deployed on a Kubernetes cluster.

---

## 🛠️ Tech Stack

* Java (Spring Boot)
* MySQL
* Docker
* Kubernetes (Minikube)
* AWS EC2 (Ubuntu)
  
```

---

## ⚙️ Step-by-Step Setup

### 🔹 Step 1: Launch EC2 Instance

* Launch Ubuntu EC2 instance
* Connect using SSH

```bash
ssh -i <key.pem> ubuntu@<EC2-IP>
```

---

### 🔹 Step 2: Install Docker

```bash
sudo apt update
sudo apt install -y docker.io
sudo systemctl start docker
sudo systemctl enable docker
```

---

### 🔹 Step 3: Install Kubernetes & Minikube

```bash
sudo apt install -y curl
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
chmod +x kubectl
sudo mv kubectl /usr/local/bin/

curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
chmod +x minikube-linux-amd64
sudo mv minikube-linux-amd64 /usr/local/bin/minikube
```

---

### 🔹 Step 4: Start Minikube

```bash
minikube start --driver=docker
```

---

### 🔹 Step 5: Build Docker Image

```bash
docker build -t anujaayare/springboot-crud-k8s:1.0 .
```

---

### 🔹 Step 6: Push Image to Docker Hub

```bash
docker login
docker push anujaayare/springboot-crud-k8s:1.0
```

---

### 🔹 Step :7 Deploy Spring Boot App

```bash
kubectl apply -f k8s/app-deployment.yaml
kubectl apply -f k8s/app-service.yaml
```

---

### 🔹 Step 8: Verify Pods

```bash
kubectl get pods
```

---

### 🔹 Step 9: Test API using Postman

* Use endpoints:

  * GET
  * POST
  * PUT
  * DELETE

---

### 🔹 Step 10: Verify Data in MySQL Pod

```bash
kubectl get pods
kubectl exec -it <mysql-pod-name> -- /bin/sh
mysql -u root -p
```

```sql
SHOW DATABASES;
USE <db_name>;
SELECT * FROM <table_name>;
```

---0

### 🔹 Step 11: Access Kubernetes Dashboard

Start proxy:

```bash
kubectl proxy --address='0.0.0.0' --accept-hosts='^*$'
```

Open in browser:

```
http://<EC2-IP>:8001/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/
```

---

### 🔹 Step 12: Access Application

```bash
kubectl port-forward svc/springboot-crud-svc 8081:8080
```

Open:

```
http://<EC2-IP>:8081
```

---

## 📊 Kubernetes Components Used

* Deployment
* Service (ClusterIP / NodePort)
* Pods
* Configurations

---

## ⚠️ Common Issues & Fixes

### ❌ Docker push access denied

✔ Ensure correct Docker username

### ❌ ImagePullBackOff

✔ Check image name & Docker Hub push

---

## 🎯 Outcome

* Successfully containerized Spring Boot application
* Deployed MySQL and application on Kubernetes
* Verified CRUD operations via Postman
* Visualized cluster using Kubernetes Dashboard

---

## 👩‍💻 Author

Anuja Ayare

---

## ⭐ If you like this project, give it a star!
