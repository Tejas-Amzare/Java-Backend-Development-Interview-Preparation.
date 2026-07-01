# 1. AWS Core Services Guide

> 🟡 **Level:** Intermediate | ⭐ **Interview Frequency:** High (cloud roles)

---

## 🧠 Concept

**AWS** is a cloud platform — you rent servers, storage, databases, and more **on demand**
instead of buying hardware. Pay only for what you use.

---

## 📋 Core Services (know these!)

| Service | What it does | Simple analogy |
|---------|-------------|----------------|
| **EC2** | Virtual servers | Rent a computer |
| **S3** | Object storage (files, images) | Unlimited cloud drive |
| **RDS** | Managed SQL databases | Database without admin work |
| **IAM** | Users, roles, permissions | Security guard / access control |
| **VPC** | Private network | Your own isolated network |
| **Lambda** | Run code without servers | Function on demand |
| **API Gateway** | Manage/route APIs | Front door for APIs |
| **CloudWatch** | Monitoring & logs | CCTV + logbook |
| **ECS** | Run Docker containers | Container manager |
| **ECR** | Store Docker images | Docker Hub on AWS |

---

## 🔍 Key Services Explained

### EC2 (Elastic Compute Cloud)
Virtual machines in the cloud. Choose CPU/RAM, install anything.
- **AMI** = the OS image. **Instance types** = t2.micro, m5.large, etc.
- **Auto Scaling** adds/removes instances based on load.

### S3 (Simple Storage Service)
Store any files (images, backups, videos) as **objects** in **buckets**.
- Very durable (99.999999999%), cheap, scalable.
- Use for: static websites, uploads, backups, data lakes.

### RDS (Relational Database Service)
Managed MySQL/Postgres/Oracle/SQL Server — AWS handles backups, patching, replication.

### IAM (Identity and Access Management)
Controls **who** can do **what**.
- **Users, Groups, Roles, Policies**.
- **Principle of least privilege** — give only needed access.

### VPC (Virtual Private Cloud)
Your own private network with **subnets** (public/private), security groups (firewalls),
and route tables.

### Lambda (Serverless)
Run code **without managing servers**. Triggered by events (HTTP, S3 upload, queue). Pay per
execution. Great for small, event-driven tasks.

### API Gateway
Creates, routes, secures, and throttles REST/HTTP APIs — often front for Lambda.

### CloudWatch
Collects **metrics, logs, and alarms**. Set alerts (e.g., CPU > 80%).

### ECS & ECR
- **ECR** = private registry for Docker images.
- **ECS** = runs containers (with Fargate = serverless containers).

---

## 🗺️ Typical Architecture

```
Users → API Gateway → Lambda / EC2 (app)
                          │
                    RDS (database)
                    S3 (files)
        IAM controls access · CloudWatch monitors · VPC isolates
```

---

## 🌍 Real-World Use Case
Host a Spring Boot app on **EC2** (or containers on **ECS**), store user uploads in **S3**, use
**RDS** for the database, secure with **IAM**, and monitor with **CloudWatch**.

---

## ❓ Interview Questions
1. What is EC2? What is an AMI?
2. What is S3? Difference between S3 and EBS? (S3 = object storage; EBS = block storage for EC2)
3. What is RDS? Benefits over self-managed DB?
4. What is IAM? What is the least privilege principle?
5. What is a VPC? Public vs private subnet?
6. What is AWS Lambda? When to use serverless?
7. Difference between ECS and EKS? (EKS = managed Kubernetes)
8. What is CloudWatch used for?
9. What is auto scaling?
10. Difference between security group and NACL?

---

## ✅ Best Practices
- Follow **least privilege** with IAM.
- Never hardcode AWS keys — use IAM roles.
- Enable CloudWatch alarms & billing alerts.
- Put databases in **private** subnets.
- Enable S3 encryption and block public access by default.

## ⚠️ Common Mistakes
- Leaving S3 buckets public → data leaks.
- Hardcoding access keys in code.
- Over-permissive IAM policies (`*` everything).
- Forgetting to stop unused EC2 (surprise bills).

---

## ⚡ Quick Revision Notes
- EC2 = servers, S3 = file storage, RDS = managed DB, Lambda = serverless.
- IAM = access control (least privilege), VPC = private network.
- API Gateway = API front door, CloudWatch = monitoring/logs.
- ECR = image store, ECS = run containers.

## 🙋 FAQs
**Q: EC2 vs Lambda?** EC2 = always-on server you manage; Lambda = event-driven, no servers, pay per call.

## 📎 References
- aws.amazon.com/documentation

[⬅ Back to AWS Index](./README.md)

