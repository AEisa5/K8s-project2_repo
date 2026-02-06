# MongoDB & Mongo-Express on Kubernetes (AWS)

## 📌 Project Overview
This project demonstrates how to deploy **MongoDB** with **Mongo-Express** on a **Kubernetes cluster running on AWS**.  
MongoDB is used as the database, while Mongo-Express provides a web-based UI to manage and visualize the data.

The architecture follows Kubernetes best practices such as **Secrets**, **ConfigMaps**, and **Persistent Volumes** backed by **AWS EBS**.

---

## 🏗️ Architecture Diagram
![Architecture Diagram](Screenshot 2026-02-05 231043.png)

---

## 🧱 Components

### 1️⃣ MongoDB
- Deployed using a **Kubernetes Deployment**
- Credentials are stored securely in a **Kubernetes Secret**
- Uses **Persistent Volume (PV)** backed by **AWS EBS**
- **Persistent Volume Claim (PVC)** is used to request storage
- Exposed internally using a **ClusterIP Service**

---

### 2️⃣ Mongo-Express
- Web-based MongoDB administration UI
- Deployed using a **Kubernetes Deployment**
- Uses **ConfigMap** for configuration values
- Uses **Secret** for MongoDB credentials
- Exposed externally using a **Service (NodePort / LoadBalancer)**

---

### 3️⃣ Kubernetes Resources
- Deployment
- Service
- Secret
- ConfigMap
- PersistentVolume (PV)
- PersistentVolumeClaim (PVC)
- StorageClass

---

## 🔄 Application Flow
1. User accesses Mongo-Express through a public IP or DNS
2. Mongo-Express reads configuration from ConfigMap
3. Mongo-Express retrieves credentials from Secret
4. Mongo-Express connects to MongoDB using internal Service
5. MongoDB stores data persistently on AWS EBS
6. Data remains available even if pods restart

---

## 🚀 How to Deploy

### 1️⃣ Create Secrets
```bash
kubectl apply -f mongo-secret.yaml
```
### 2️⃣ Create ConfigMap
```
kubectl apply -f mongo-configmap.yaml
```
3️⃣ Create Storage Resources
```
kubectl apply -f storageclass.yaml
kubectl apply -f pv.yaml
kubectl apply -f pvc.yaml
```

4️⃣ Deploy MongoDB
```
kubectl apply -f mongo-deployment.yaml
kubectl apply -f mongo-service.yaml
```

5️⃣ Deploy Mongo-Express
```
kubectl apply -f mongo-express-deployment.yaml
kubectl apply -f mongo-express-service.yaml
```

🌐 Access Mongo-Express

Get the service IP:

kubectl get svc


Then open in browser:

http://<EXTERNAL-IP>:<PORT>

✅ Key Features

Secure credentials using Kubernetes Secrets

Persistent storage using AWS EBS

Cloud-native Kubernetes architecture

Easy database management via Mongo-Express UI

Scalable and production-ready design

🛠️ Technologies Used

Kubernetes

Docker

MongoDB

Mongo-Express

AWS (EBS)

YAML

📌 Future Improvements

Add Ingress Controller

Enable MongoDB authentication with TLS

Use Helm charts

Add monitoring with Prometheus & Grafana

👨‍💻 Author

Ahmed
DevOps / Cloud Enthusiast 🚀
