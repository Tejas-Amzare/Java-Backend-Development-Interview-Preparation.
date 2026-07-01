# 05 — DevOps, Cloud & System Design Interview Questions (90+)

---

## 🐳 Docker (1–20)

1. **What is Docker?** Packages an app + dependencies into a container.
2. **What problem does Docker solve?** "Works on my machine" inconsistencies.
3. **Image vs container?** Blueprint vs running instance.
4. **Container vs VM?** Shares host OS (light) vs full OS per VM (heavy).
5. **What is a Dockerfile?** Instructions to build an image.
6. **What is a registry?** Store for images (Docker Hub, ECR).
7. **CMD vs ENTRYPOINT?** Default args vs main command.
8. **What is a volume?** Persistent storage outside the container.
9. **Why volumes?** Containers are ephemeral; data must survive restarts.
10. **What is Docker Compose?** Run multi-container apps via one YAML.
11. **How do containers communicate?** Docker networks (by name).
12. **What is a multi-stage build?** Separate build/run stages for smaller images.
13. **How to reduce image size?** Small base image, multi-stage, .dockerignore.
14. **What is `docker exec`?** Run a command inside a running container.
15. **What is a layer?** A cached step in an image build.
16. **What is `docker ps`?** Lists running containers.
17. **What is the difference between COPY and ADD?** COPY copies; ADD also extracts/URLs.
18. **What is `EXPOSE`?** Documents the port the app uses.
19. **How to pass env variables?** `-e` flag or `environment` in Compose.
20. **What is a bind mount?** Maps a host folder into a container.

---

## ☸️ Kubernetes (21–40)

21. **What is Kubernetes?** Orchestrates containers (scale, heal, deploy).
22. **Docker vs Kubernetes?** Runs a container vs manages many across a cluster.
23. **What is a Pod?** The smallest deployable unit (wraps containers).
24. **What is a Deployment?** Manages Pods: scaling, updates, self-healing.
25. **Deployment vs Pod?** Manager vs the unit being managed.
26. **What is a Service?** Stable network endpoint that load-balances Pods.
27. **Service types?** ClusterIP, NodePort, LoadBalancer, (Ingress).
28. **What is Ingress?** Routes external HTTP traffic by host/path.
29. **ConfigMap vs Secret?** Config vs sensitive data.
30. **What is a Namespace?** Virtual cluster to group/isolate resources.
31. **What is self-healing?** K8s restarts failed Pods automatically.
32. **What is HPA?** Horizontal Pod Autoscaler (scales on load).
33. **What is a rolling update?** Gradually replace Pods with no downtime.
34. **What is a rollback?** Revert to a previous Deployment version.
35. **What is a node?** A worker machine running Pods.
36. **What is the control plane?** The brain (API server, scheduler, etc.).
37. **What is etcd?** The cluster's key-value data store.
38. **What is a liveness probe?** Checks if a Pod is alive (restart if not).
39. **What is a readiness probe?** Checks if a Pod can receive traffic.
40. **What is kubectl?** The CLI to control Kubernetes.

---

## ☁️ AWS (41–60)

41. **What is AWS?** A cloud platform offering on-demand infrastructure.
42. **What is EC2?** Virtual servers in the cloud.
43. **What is an AMI?** A machine image (OS template) for EC2.
44. **What is S3?** Object storage for files.
45. **S3 vs EBS?** Object storage vs block storage for EC2.
46. **What is RDS?** Managed relational databases.
47. **What is IAM?** Identity and access management.
48. **What is least privilege?** Grant only the access needed.
49. **What is a VPC?** Your private isolated network.
50. **Public vs private subnet?** Internet-accessible vs internal only.
51. **What is a security group?** A virtual firewall for instances.
52. **What is Lambda?** Serverless function execution.
53. **When to use serverless?** Event-driven, spiky, small tasks.
54. **What is API Gateway?** Managed API front door (often for Lambda).
55. **What is CloudWatch?** Monitoring, logs, and alarms.
56. **What is Auto Scaling?** Automatically adjust instance count.
57. **What is ECR?** Private Docker image registry.
58. **What is ECS?** Container orchestration service.
59. **ECS vs EKS?** AWS-native containers vs managed Kubernetes.
60. **What is CloudFront?** AWS CDN for caching content near users.

---

## 🌿 Git (61–72)

61. **Git vs GitHub?** Version control tool vs hosting platform.
62. **git fetch vs pull?** Download vs download+merge.
63. **Merge vs rebase?** Keep history vs linear history.
64. **Reset vs revert?** Rewrite history vs safe undo commit.
65. **What is cherry-pick?** Apply one specific commit.
66. **What is stash?** Temporarily shelve changes.
67. **What is a merge conflict?** Two changes to the same lines.
68. **What is a pull request?** A reviewed proposal to merge branches.
69. **What is Git Flow?** A branching strategy (main/develop/feature/release/hotfix).
70. **What is HEAD?** Pointer to the current commit/branch.
71. **What is origin?** Default name for the remote repo.
72. **What is `.gitignore`?** Lists files Git should not track.

---

## 🏗️ System Design (73–90)

73. **HLD vs LLD?** Architecture vs class-level detail.
74. **What is scalability?** Handling more load by adding resources.
75. **Vertical vs horizontal scaling?** Bigger machine vs more machines.
76. **Why stateless services?** Easy horizontal scaling.
77. **What is a load balancer?** Distributes traffic across servers.
78. **Load balancing algorithms?** Round robin, least connections, IP hash.
79. **What is caching?** Storing hot data in fast memory.
80. **Cache hit vs miss?** Found vs not found in cache.
81. **What is cache invalidation?** Keeping cached data fresh.
82. **What is the CAP theorem?** Pick 2 of Consistency, Availability, Partition tolerance.
83. **CP vs AP systems?** Consistency-first vs availability-first.
84. **What is replication?** Copies of data for read scaling/redundancy.
85. **What is sharding?** Splitting data across databases.
86. **What is a message queue?** Async, decoupled communication.
87. **What is a CDN?** Servers caching static content near users.
88. **Latency vs throughput?** Delay per request vs requests per second.
89. **How to scale a read-heavy system?** Caching + read replicas.
90. **How to design a URL shortener?** Base62 of ID, cache mappings, 301 redirect.

[⬅ Back to Questions Index](./README.md)

