# 🚀 DevOps Learning Roadmap

A structured roadmap covering the core concepts, tools, and skills required to build strong **DevOps** fundamentals and progress toward **DevOps / MLOps / Cloud Engineering** roles.

---

## 📚 DevOps Roadmap

| # | Area | What You Should Learn | Depth |
|---|---|---|---|
| 1 | **Linux** | Filesystem, permissions, users, processes, services, networking, logs | ⭐⭐⭐⭐⭐ |
| 2 | **Shell Scripting** | Bash variables, loops, functions, arguments, exit codes, pipes, `grep`, `awk`, `sed`, `find`, `xargs` | ⭐⭐⭐⭐⭐ |
| 3 | **Computer Networking** | TCP/IP, DNS, HTTP/HTTPS, SSH, ports, sockets, firewalls, proxies, load balancers | ⭐⭐⭐⭐⭐ |
| 4 | **Git** | Branching, merging, rebase, cherry-pick, reset/revert, stash, tags, hooks | ⭐⭐⭐⭐⭐ |
| 5 | **GitHub/GitLab** | PRs, reviews, Actions, webhooks, branch protection | ⭐⭐⭐⭐ |
| 6 | **CI/CD** | Pipelines, stages, artifacts, runners/agents, triggers, deployment strategies | ⭐⭐⭐⭐⭐ |
| 7 | **Jenkins** | Pipelines, Jenkinsfile, agents, credentials, plugins, webhooks, distributed builds | ⭐⭐⭐⭐⭐ |
| 8 | **Docker** | Images, containers, Dockerfile, volumes, networks, registries, Compose | ⭐⭐⭐⭐⭐ |
| 9 | **Kubernetes** | Pods, Deployments, Services, ConfigMaps, Secrets, Ingress, volumes, probes, RBAC | ⭐⭐⭐⭐⭐ |
| 10 | **Cloud** | AWS/Azure fundamentals, compute, networking, IAM, storage | ⭐⭐⭐⭐⭐ |
| 11 | **Infrastructure as Code** | Terraform, state, modules, variables, providers | ⭐⭐⭐⭐⭐ |
| 12 | **Configuration Management** | Ansible, inventories, playbooks, roles, idempotency | ⭐⭐⭐⭐ |
| 13 | **Monitoring** | Metrics, logs, traces, alerting, Prometheus, Grafana | ⭐⭐⭐⭐ |
| 14 | **Security / DevSecOps** | IAM, secrets, image scanning, SAST/DAST, dependency scanning | ⭐⭐⭐⭐ |
| 15 | **Observability** | Logs + metrics + traces, OpenTelemetry, distributed tracing | ⭐⭐⭐⭐ |
| 16 | **Databases** | PostgreSQL/MySQL basics, backups, replication, connection pooling | ⭐⭐⭐ |
| 17 | **System Design** | Scalability, availability, load balancing, caching, queues | ⭐⭐⭐⭐ |
| 18 | **Python Automation** | APIs, subprocess, `os`, `pathlib`, YAML/JSON, automation scripts | ⭐⭐⭐⭐⭐ |
| 19 | **DevOps Architecture** | How all the above fit together | ⭐⭐⭐⭐⭐ |
| 20 | **MLOps** | Model CI/CD, model serving, experiment tracking, monitoring | ⭐⭐⭐⭐ |

---

# 1. 🐧 Linux

### Core Topics

- Linux filesystem
- Absolute and relative paths
- File and directory permissions
- Users and groups
- Processes
- Services
- Systemd
- Environment variables
- Package management
- Networking
- Logs
- Disk management
- Mounts
- File systems

### Important Commands

```bash
pwd
ls
cd
cp
mv
rm
mkdir
touch
cat
less
head
tail
find
grep
sed
awk
sort
uniq
cut
xargs
wc
diff
tar
gzip
chmod
chown
ln
df
du
mount
```

### Processes

```bash
ps
top
htop
pgrep
pkill
kill
killall
jobs
bg
fg
nohup
```

### Services

```bash
systemctl
journalctl
```

### Networking Commands

```bash
ping
curl
wget
ssh
scp
ss
netstat
traceroute
nslookup
dig
ip
tcpdump
```

### Important Concepts

- Process vs thread
- PID and PPID
- Foreground vs background processes
- Daemons
- Signals
- `SIGTERM` vs `SIGKILL`
- Zombie processes
- Orphan processes
- Inodes
- Hard links vs symbolic links
- `/etc`
- `/var/log`
- `/proc`
- `/dev`
- `/tmp`
- `/home`

---

# 2. 🐚 Shell Scripting

### Basics

- Bash syntax
- Variables
- Strings
- Numbers
- Arrays
- Conditions
- Loops
- Functions
- Command-line arguments
- Exit status
- Environment variables

### Important Concepts

```bash
$?
$0
$1
$2
$@
$#
```

### Operators

```bash
>
>>
<
2>
2>&1
|
&&
||
;
```

### Commands to Master

```bash
grep
sed
awk
find
xargs
cut
sort
uniq
tr
wc
head
tail
```

### Advanced Topics

- Pipes
- Redirection
- Command substitution
- Process substitution
- Cron jobs
- Error handling
- Debugging Bash scripts
- Shell scripting for automation

---

# 3. 🌐 Computer Networking

### Networking Fundamentals

- OSI model
- TCP/IP model
- IP addresses
- MAC addresses
- ARP
- TCP
- UDP
- Ports
- Sockets
- Routing
- NAT
- Subnetting
- CIDR
- Public vs private IP

### Protocols

- HTTP
- HTTPS
- DNS
- SSH
- FTP/SFTP
- SMTP
- DHCP

### Infrastructure Concepts

- Firewall
- Proxy
- Reverse proxy
- Load balancer
- NAT Gateway
- VPN
- Security groups

### Important Questions

Understand:

```text
What happens when you type google.com in a browser?
```

```text
How does DNS work?
```

```text
What happens during an HTTPS request?
```

```text
How does a load balancer distribute traffic?
```

---

# 4. 🔀 Git

### Basic Commands

```bash
git init
git clone
git status
git add
git commit
git push
git pull
git fetch
```

### Branching

```bash
git branch
git switch
git checkout
git merge
git rebase
```

### Advanced Commands

```bash
git cherry-pick
git stash
git reset
git revert
git reflog
```

### Concepts

- Working directory
- Staging area
- Commit
- HEAD
- Branch
- Remote
- Merge
- Rebase
- Merge conflicts
- Tags
- Git hooks

### Important Comparisons

- `merge` vs `rebase`
- `reset` vs `revert`
- `fetch` vs `pull`
- `HEAD` vs branch
- Hard link vs Git reference

---

# 5. 🐙 GitHub / GitLab

Learn:

- Repository management
- Branch protection
- Pull requests
- Merge requests
- Code reviews
- Issues
- Releases
- Tags
- Webhooks
- GitHub Actions
- GitLab CI/CD
- Secrets
- Environment variables

### GitHub Actions

Understand:

```text
Workflow
   ↓
Job
   ↓
Steps
   ↓
Runner
```

---

# 6. 🔄 CI/CD

### Core Concepts

- Continuous Integration
- Continuous Delivery
- Continuous Deployment
- Pipeline
- Stage
- Job
- Runner
- Agent
- Artifact
- Build
- Trigger
- Webhook

### Typical Pipeline

```text
Developer
    ↓
Git Push
    ↓
Build
    ↓
Unit Tests
    ↓
Code Quality
    ↓
Security Scan
    ↓
Build Artifact
    ↓
Deploy
    ↓
Test
    ↓
Monitor
```

### Deployment Strategies

- Rolling deployment
- Blue-Green deployment
- Canary deployment
- Recreate deployment

---

# 7. 🧩 Jenkins

### Core Topics

- Jenkins architecture
- Controller
- Agents
- Nodes
- Executors
- Jobs
- Pipelines
- Jenkinsfile
- Credentials
- Plugins
- Artifacts
- Webhooks
- Build triggers
- Cron jobs
- Distributed builds

### Jenkins Pipeline

Learn:

```groovy
pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                // build
            }
        }

        stage('Test') {
            steps {
                // test
            }
        }

        stage('Deploy') {
            steps {
                // deploy
            }
        }
    }
}
```

### Advanced Topics

- Declarative Pipeline
- Scripted Pipeline
- Shared libraries
- Pipeline parameters
- Environment variables
- Parallel stages
- Credentials management

---

# 8. 🐳 Docker

### Core Concepts

- Container
- Image
- Registry
- Docker Engine
- Dockerfile
- Docker Compose
- Volumes
- Networks

### Important Commands

```bash
docker build
docker run
docker ps
docker stop
docker start
docker restart
docker exec
docker logs
docker inspect
docker pull
docker push
docker images
docker rm
docker rmi
```

### Dockerfile

Learn:

```dockerfile
FROM
RUN
COPY
ADD
WORKDIR
ENV
ARG
EXPOSE
CMD
ENTRYPOINT
USER
```

### Important Comparisons

- `CMD` vs `ENTRYPOINT`
- `COPY` vs `ADD`
- `ARG` vs `ENV`
- Image vs container
- Volume vs bind mount

### Docker Networking

Understand:

```text
bridge
host
none
```

### Docker Compose

Learn:

```yaml
services:
volumes:
networks:
environment:
depends_on:
ports:
```

---

# 9. ☸️ Kubernetes

### Architecture

```text
Kubernetes Cluster
        |
   ┌────┴─────┐
   |          |
Control      Worker
Plane        Nodes
   |            |
API Server     kubelet
Scheduler      kube-proxy
etcd           Pods
```

### Core Objects

- Pod
- Deployment
- ReplicaSet
- Service
- Namespace
- ConfigMap
- Secret
- Ingress
- Job
- CronJob
- DaemonSet
- StatefulSet

### Important Commands

```bash
kubectl get
kubectl describe
kubectl create
kubectl apply
kubectl delete
kubectl logs
kubectl exec
kubectl port-forward
kubectl get pods
kubectl get deployments
kubectl get services
```

### Pod Lifecycle

Understand:

```text
Pending
Running
Succeeded
Failed
Unknown
```

### Debugging

Learn how to troubleshoot:

```text
CrashLoopBackOff
ImagePullBackOff
Pending
OOMKilled
Container failure
Service connectivity issues
```

---

# 10. ☁️ Cloud

Focus initially on **AWS**.

### Compute

- EC2
- ECS
- EKS
- Lambda

### Storage

- S3
- EBS
- EFS

### Networking

- VPC
- Subnet
- Route Table
- Internet Gateway
- NAT Gateway
- Security Group
- NACL
- Load Balancer

### IAM

Understand:

```text
User
Role
Policy
Permission
Trust Policy
```

### Important Concepts

- Availability Zones
- Regions
- High availability
- Auto scaling
- Load balancing
- Fault tolerance
- Disaster recovery

---

# 11. 🏗️ Infrastructure as Code

## Terraform

### Core Concepts

- Provider
- Resource
- Variable
- Output
- Data source
- Module
- State

### Commands

```bash
terraform init
terraform plan
terraform apply
terraform destroy
terraform validate
terraform fmt
```

### Advanced Topics

- Terraform state
- Remote state
- State locking
- Modules
- Workspaces
- Variables
- Secrets
- Infrastructure drift

### Architecture

```text
Terraform
    ↓
Provider
    ↓
Resources
    ↓
Cloud Infrastructure
```

---

# 12. ⚙️ Configuration Management

## Ansible

Learn:

- Inventory
- Playbook
- Task
- Module
- Role
- Variables
- Handlers
- Templates
- Facts

### Important Concept

**Idempotency**

A configuration should produce the desired state even if it is executed multiple times.

### Architecture

```text
Ansible Controller
       |
 ┌─────┼─────┐
 ↓     ↓     ↓
VM1   VM2   VM3
```

---

# 13. 📊 Monitoring

Understand the difference between:

### Metrics

> How much / how often?

Examples:

```text
CPU usage
Memory usage
Request rate
Error rate
Latency
Disk usage
```

### Logs

> What happened?

### Traces

> Where did the request spend time?

### Tools

- Prometheus
- Grafana
- Alertmanager
- Loki

### Monitoring Pipeline

```text
Application
     ↓
Metrics
     ↓
Prometheus
     ↓
Grafana
     ↓
Alerts
```

---

# 14. 🔐 Security / DevSecOps

### Security Fundamentals

- Authentication
- Authorization
- IAM
- Least privilege
- Secrets management
- Encryption
- TLS
- Network security

### Application Security

- SAST
- DAST
- Dependency scanning
- Vulnerability scanning
- Container image scanning

### CI/CD Security

```text
Code
 ↓
SAST
 ↓
Dependency Scan
 ↓
Build
 ↓
Container Scan
 ↓
Deploy
```

### Important Concepts

- Secrets should not be stored in Git
- Principle of least privilege
- IAM roles
- Secret rotation
- Secure container images
- SBOM

---

# 15. 🔭 Observability

Observability has three major pillars:

```text
             Observability
             /     |     \
            /      |      \
         Logs    Metrics   Traces
```

Learn:

- Structured logging
- Centralized logging
- Metrics
- Distributed tracing
- Correlation IDs
- OpenTelemetry
- Trace IDs
- Span IDs
- SLI
- SLO
- SLA
- Alerting

---

# 16. 🗄️ Databases

Learn basic administration and production concepts for:

- PostgreSQL
- MySQL

### Core Concepts

- Tables
- Indexes
- Transactions
- ACID
- Connection pooling
- Database migrations
- Backups
- Restore
- Replication
- Primary/Replica architecture

### Important Problems

Understand why applications can fail because of:

```text
Too many connections
Slow queries
Database locks
Disk full
Replication lag
Connection timeout
```

---

# 17. 🏛️ System Design

### Scalability

- Vertical scaling
- Horizontal scaling
- Auto scaling

### Availability

- High availability
- Fault tolerance
- Redundancy
- Disaster recovery

### Components

- Load balancers
- Caches
- CDNs
- Message queues
- Databases
- Replicas

### Important Concepts

```text
Caching
Load Balancing
Database Replication
Partitioning
Sharding
Queues
Rate Limiting
Fault Tolerance
```

### Example

```text
                    Internet
                       |
                 Load Balancer
                  /         \
                 /           \
             Server 1      Server 2
                 \           /
                  \         /
                    Cache
                      |
                   Database
```

---

# 18. 🐍 Python Automation

Use Python to automate DevOps tasks.

### Important Libraries

```python
os
sys
subprocess
pathlib
shutil
json
yaml
argparse
logging
requests
```

### Learn to Automate

- File management
- Log analysis
- Server checks
- API calls
- Deployment tasks
- Health checks
- Monitoring scripts
- Report generation
- CI/CD tasks

### Example Architecture

```text
Python Script
     ↓
Read Logs
     ↓
Analyze Errors
     ↓
Call API
     ↓
Generate Report
     ↓
Send Notification
```

---

# 19. 🧠 DevOps Architecture

The most important goal is understanding **how everything fits together**.

A typical architecture:

```text
Developer
    |
    ↓
GitHub
    |
    ↓
CI/CD
    |
    ↓
Jenkins
    |
    ├── Build
    ├── Test
    ├── Security Scan
    └── Package
            |
            ↓
        Docker Image
            |
            ↓
      Container Registry
            |
            ↓
       Kubernetes
            |
       ┌────┴────┐
       ↓         ↓
    Service    Ingress
       |         |
       └────┬────┘
            ↓
        Application
            |
       ┌────┴────┐
       ↓         ↓
    Database    Cache
            |
            ↓
      Monitoring
            |
       Prometheus
            |
         Grafana
```

You should eventually be able to explain:

- Why each component exists
- How components communicate
- Where failures can occur
- How to monitor them
- How to secure them
- How to scale them
- How to deploy new versions

---

# 20. 🤖 MLOps

Since DevOps can lead naturally into MLOps, learn how DevOps concepts apply to ML systems.

### MLOps Pipeline

```text
Data
 ↓
Training
 ↓
Experiment Tracking
 ↓
Model Evaluation
 ↓
Model Registry
 ↓
Docker
 ↓
CI/CD
 ↓
Model Deployment
 ↓
Kubernetes
 ↓
Monitoring
 ↓
Retraining
```

### Topics

- Model versioning
- Data versioning
- Experiment tracking
- Model registry
- Model CI/CD
- Model serving
- Batch inference
- Real-time inference
- Model monitoring
- Data drift
- Model drift
- Inference latency
- Automated retraining

### Tools

- MLflow
- Docker
- Kubernetes
- FastAPI
- Jenkins / GitHub Actions
- AWS
- Prometheus
- Grafana

---

# 🎯 Recommended Learning Order

Follow this order instead of studying everything randomly:

```text
1. Linux
      ↓
2. Networking
      ↓
3. Git
      ↓
4. Shell Scripting
      ↓
5. Docker
      ↓
6. CI/CD
      ↓
7. Jenkins
      ↓
8. Kubernetes
      ↓
9. AWS
      ↓
10. Terraform
      ↓
11. Ansible
      ↓
12. Monitoring
      ↓
13. Observability
      ↓
14. DevSecOps
      ↓
15. System Design
      ↓
16. DevOps Architecture
      ↓
17. MLOps
```

---

# ⭐ Priority

## Must Master — ⭐⭐⭐⭐⭐

- Linux
- Networking
- Git
- Shell Scripting
- Docker
- CI/CD
- Jenkins
- Kubernetes
- AWS
- Terraform
- Python Automation
- Troubleshooting

## Learn Well — ⭐⭐⭐⭐

- Ansible
- Prometheus
- Grafana
- DevSecOps
- Observability
- System Design

## Learn Later

- Helm
- ArgoCD
- Istio
- OpenTelemetry
- Vault
- Kafka
- Advanced Kubernetes
- Advanced AWS
- Advanced MLOps

---

# 🔥 Final Goal

Do not aim to simply memorize DevOps commands.

Your goal should be:

> **Understand the problem → choose the right tool → implement it → deploy it → monitor it → troubleshoot it → secure it → scale it.**

A strong DevOps engineer should be able to take an application from:

```text
Code
 ↓
Git
 ↓
Build
 ↓
Test
 ↓
Docker
 ↓
CI/CD
 ↓
Cloud
 ↓
Kubernetes
 ↓
Monitoring
 ↓
Production
```

and understand **every layer of the system**.

---

## 🛠️ Recommended Capstone Project

Build one complete project that combines the major concepts:

```text
Python FastAPI Application
          ↓
        GitHub
          ↓
       Jenkins
          ↓
    Automated Tests
          ↓
        Docker
          ↓
   Docker Registry
          ↓
      Kubernetes
          ↓
        AWS
          ↓
      Terraform
          ↓
   Prometheus + Grafana
          ↓
       Monitoring
```

This single project will give you significantly stronger practical understanding than learning each tool independently.
