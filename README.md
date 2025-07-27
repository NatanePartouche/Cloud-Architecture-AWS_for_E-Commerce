
# 🌐 Cloud System Architecture for Online Ordering

## 📖 Project Overview
This project is a **basic cloud system architecture** designed for an **online ordering application**, leveraging various **AWS services**.  
The main objective is to provide a **secure, scalable, and cost-effective** infrastructure for handling online orders efficiently.  

The architecture includes **three main components**:
1. **Web Server** 🌍 – The user-facing website.
2. **Backend Server** ⚙️ – Handles orders and business logic.
3. **Database** 🗄️ – Securely stores products and orders.

Our team (Group 22) aimed for a solution that is **reliable, scalable, and cost-effective**, using **AWS services**.

---

## 🅰️ Part A: Basic System Architecture
This is the initial design focused on a **functional, low-cost system**.

### **Components:**
- **Web Server** 🌍:  
  - EC2 instance: **t3.medium** (2 vCPUs, 4 GB RAM).  
  - Capable of handling thousands of users while staying cost-efficient.

- **Backend Server** ⚙️:  
  - EC2 instance: **t3.large** (2 vCPUs, 8 GB RAM).  
  - Handles order processing and data exchange between web and database.

- **Database** 🗄️:  
  - **Amazon RDS MySQL** – **db.m6g.large** (2 vCPUs, 8 GB RAM).  
  - 100 GB **GP3 SSD** for fast read/write operations.

### **Security** 🔒:
- Hosted inside a **VPC**.  
- **Internet Gateway** only for the web server.  
- Backend and database are **isolated**, communicating internally only.  
- **Security Groups** restrict access between layers.

---

## 🅱️ Part B: Durable (High Availability) Architecture
The aim here was to ensure **continuous service** even if an instance or an availability zone fails.

### **Key Improvements:**
- **Web Layer** 🌍:  
  - Replaced single EC2 with **Auto Scaling Group** (minimum 2 **t3.medium**).  
  - Spanning **2 Availability Zones (AZs)**.  
  - **Application Load Balancer (ALB)** distributes traffic.

- **Backend Layer** ⚙️:  
  - 2 **t3.large** instances under an **Auto Scaling Group** behind an internal ALB.

- **Database Layer** 🗄️:  
  - **RDS MySQL Multi-AZ** with automatic failover.

- **Network & Security** 🔐:  
  - Still VPC-based with strict security rules.

---

## 🆂 Part C: Scalable System Design
We made the system **elastic** to handle spikes in traffic without performance issues.

### **Features:**
- **Smart Auto Scaling** 📈 based on real-time CPU or traffic.  
  - Web Layer: Scales **2 → 10 EC2s**.  
  - Backend: Scales according to request load.

- **Database Scaling** 🗄️:  
  - **Aurora Serverless v2** for automatic capacity scaling.  
  - Alternatively, RDS MySQL Multi-AZ with auto-scaling storage.

- **Additional Services**:  
  - **Amazon CloudFront** 🌍 – Content Delivery Network.  
  - **Amazon S3** 📦 – File storage offloading.  
  - **AWS Lambda or Kinesis** ⚡ – Event-based processing (e.g., IoT).

---

## 🎯 Key Benefits
- **High Availability** 🟢 – Multi-AZ and Auto Scaling ensure zero downtime.  
- **Elasticity** ⚡ – Adapts to load automatically.  
- **Security** 🔒 – Layer isolation and strict network rules.  
- **Cost Efficiency** 💰 – Pay only for what is used.

---

## 📊 Figures (not included in this file)
- **Figure 1:** vCPU & RAM per component.  
- **Figure 2:** Durable Architecture (Multi-AZ + Auto Scaling).  
- **Figure 3:** Scalable Architecture (Auto Scaling + RDS Multi-AZ).  
