# 🚀 CI/CD Pipeline for Static Website

![Jenkins](https://img.shields.io/badge/Jenkins-D24939?style=for-the-badge&logo=jenkins&logoColor=white)
![AWS](https://img.shields.io/badge/AWS_EC2-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)
![Nginx](https://img.shields.io/badge/Nginx-009639?style=for-the-badge&logo=nginx&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)

> **Live Demo:** [http://your-ec2-ip](http://your-ec2-ip) *(Replace with your actual EC2 IP)*

## 📌 Project Overview

This project demonstrates a **fully automated CI/CD pipeline** that deploys a static website whenever code is pushed to GitHub. No manual intervention required!

### 🔄 How It Works

```
GitHub Push → Jenkins → EC2 → Nginx → Live Website
    │           │        │       │
    ▼           ▼        ▼       ▼
 Webhook    Pipeline   Deploy   Serve
 (Auto)      (Auto)    (Auto)   (Auto)

Total deployment time: ~30 seconds
```

**Total deployment time:** ~30 seconds ⚡

---

## 🛠️ Technologies Used

| Tool | Purpose |
|------|---------|
| **Jenkins** | CI/CD automation server |
| **GitHub Webhooks** | Auto-trigger pipeline on code push |
| **AWS EC2** | Hosting Jenkins & Nginx |
| **Nginx** | Web server for static content |
| **Ubuntu 22.04** | Operating system |
| **Git** | Version control |

---

## 📸 Screenshots

### Jenkins Pipeline Success
![Pipeline Success](screenshots/pipeline-success.png)

### Live Website
![Live Website](screenshots/website-live.png)

### Jenkins Dashboard
![Jenkins Dashboard](screenshots/jenkins-dashboard.png)

---

## 🏗️ Architecture Diagram

## Architecture Diagram

```
┌──────────────────────────────────────────┐
│            DEVELOPER LAPTOP              │
│         git push origin main             │
└────────────────────┬─────────────────────┘
                     │
                     ▼
┌──────────────────────────────────────────┐
│              GITHUB REPO                 │
│    Webhook: Push event → POST to Jenkins │
└────────────────────┬─────────────────────┘
                     │
                     ▼
┌──────────────────────────────────────────┐
│           JENKINS (AWS EC2)              │
│  ┌────────────────────────────────────┐  │
│  │ 1. Checkout Code                   │  │
│  │ 2. Validate HTML                   │  │
│  │ 3. Deploy to /var/www/html/        │  │
│  │ 4. Reload Nginx                    │  │
│  │ 5. Verify HTTP 200                 │  │
│  └────────────────────────────────────┘  │
└────────────────────┬─────────────────────┘
                     │
                     ▼
┌──────────────────────────────────────────┐
│            NGINX WEB SERVER              │
│    Serves: /var/www/html/index.html      │
│         Port: 80 (HTTP)                  │
└──────────────────────────────────────────┘
```


---

