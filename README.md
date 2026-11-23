<!-- ===================== HEADER BANNER ===================== -->
<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:FF9900,50:232F3E,100:2088FF&height=220&section=header&text=GitHub%20Actions%20CI%2FCD&fontSize=52&fontColor=ffffff&animation=fadeIn&fontAlignY=36&desc=Deploy%20an%20HTML%20Website%20to%20AWS%20S3%20Automatically&descSize=20&descAlignY=58" alt="Banner"/>

<a href="https://github.com/ajaydhadi95-gif/devops-roadmap">
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=22&duration=3000&pause=800&color=FF9900&center=true&vCenter=true&width=700&lines=Push+to+main+%E2%86%92+Live+on+S3+%F0%9F%9A%80;GitHub+Actions+%2B+AWS+IAM+%2B+S3;Zero+Manual+Deployment+%E2%9C%A8;Built+with+%E2%9D%A4%EF%B8%8F+for+DevOps+Learners" alt="Typing animation"/>
</a>

<br/>

![AWS S3](https://img.shields.io/badge/AWS-S3-FF9900?style=for-the-badge&logo=amazons3&logoColor=white)
![AWS IAM](https://img.shields.io/badge/AWS-IAM-DD344C?style=for-the-badge&logo=amazonaws&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub-Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white)
![YAML](https://img.shields.io/badge/YAML-CB171E?style=for-the-badge&logo=yaml&logoColor=white)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![AWS CLI](https://img.shields.io/badge/AWS-CLI-232F3E?style=for-the-badge&logo=gnubash&logoColor=white)

![Status](https://img.shields.io/badge/Status-Successfully%20Deployed-2EA44F?style=flat-square&logo=checkmarx&logoColor=white)
![Region](https://img.shields.io/badge/Region-ap--south--1%20(Mumbai)-8A2BE2?style=flat-square&logo=amazonaws&logoColor=white)
![Trigger](https://img.shields.io/badge/Trigger-push%20to%20main-00B8D9?style=flat-square&logo=git&logoColor=white)
![Made with](https://img.shields.io/badge/Made%20with-DevOps%20%E2%9D%A4-FF4081?style=flat-square)

</div>

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%" alt="divider"/>

## 📑 Table of Contents

- [🌟 Project Overview](#-project-overview)
- [🏗️ Architecture](#️-architecture)
- [🧰 Technologies Used](#-technologies-used)
- [📂 Project Structure](#-project-structure)
- [☁️ AWS Configuration](#️-aws-configuration)
- [⚙️ GitHub Actions Pipeline](#️-github-actions-cicd-pipeline)
- [🔍 Pipeline Explanation](#-pipeline-explanation)
- [🌐 S3 Static Website Access](#-s3-static-website-access)
- [▶️ How to Execute](#️-how-to-execute-the-project)
- [✅ Expected Results](#-expected-pipeline-results)
- [🛠️ Troubleshooting](#️-troubleshooting)
- [🔐 Security Best Practices](#-security-best-practices)
- [🎓 Key Learning Outcomes](#-key-learning-outcomes)

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%" alt="divider"/>

## 🌟 Project Overview

This project demonstrates an **end-to-end CI/CD pipeline** using **GitHub Actions** and **AWS S3** to automatically deploy a static HTML website.

> 💡 Whenever a developer pushes code to the `main` branch, GitHub Actions triggers the pipeline, authenticates with AWS, and uploads the website to an S3 bucket — **no manual steps required**.

<div align="center">

| ⚡ Automated | 🔒 Secure | ☁️ Serverless | 🚀 Fast |
|:---:|:---:|:---:|:---:|
| Push → Deploy | GitHub Secrets + IAM | Static hosting on S3 | Live in seconds |

</div>

<!--
  🎬 DEMO GIF (optional but recommended)
  1. Record your pipeline run + live site with ScreenToGif / LICEcap / Kap
  2. Save it as  assets/pipeline-demo.gif  in this repo
  3. Uncomment the block below
-->
<!--
<div align="center">
  <img src="assets/pipeline-demo.gif" width="85%" alt="Pipeline demo"/>
  <br/><sub>Live pipeline run: push → build → deploy</sub>
</div>
-->

## 🏗️ Architecture

```mermaid
flowchart TD
    A([👨‍💻 Developer]) -->|git push| B[📦 GitHub Repository]
    B --> C{{⚙️ GitHub Actions}}
    C --> C1[Checkout Code]
    C1 --> C2[Verify HTML File]
    C2 --> C3[Configure AWS Credentials]
    C3 --> C4[Verify AWS Identity]
    C4 --> D[🔐 AWS IAM Authentication]
    D --> E[(🪣 Amazon S3 Bucket)]
    E -->|Upload as index.html| F[🌐 S3 Static Website Hosting]
    F --> G([🚀 Live Website])

    style A fill:#6C5CE7,stroke:#4834d4,color:#fff
    style B fill:#24292F,stroke:#000,color:#fff
    style C fill:#2088FF,stroke:#0b5ed7,color:#fff
    style C1 fill:#74B9FF,stroke:#0984e3,color:#000
    style C2 fill:#74B9FF,stroke:#0984e3,color:#000
    style C3 fill:#74B9FF,stroke:#0984e3,color:#000
    style C4 fill:#74B9FF,stroke:#0984e3,color:#000
    style D fill:#DD344C,stroke:#a61e33,color:#fff
    style E fill:#FF9900,stroke:#cc7a00,color:#000
    style F fill:#00B894,stroke:#00896f,color:#fff
    style G fill:#2EA44F,stroke:#1e7a37,color:#fff
```

## 🧰 Technologies Used

<div align="center">

<img src="https://img.shields.io/badge/AWS%20S3-FF9900?style=for-the-badge&logo=amazons3&logoColor=white"/>
<img src="https://img.shields.io/badge/AWS%20IAM-DD344C?style=for-the-badge&logo=amazonaws&logoColor=white"/>
<img src="https://img.shields.io/badge/GitHub%20Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white"/>
<img src="https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white"/>
<img src="https://img.shields.io/badge/GitHub%20Secrets-181717?style=for-the-badge&logo=github&logoColor=white"/>
<img src="https://img.shields.io/badge/HTML-E34F26?style=for-the-badge&logo=html5&logoColor=white"/>
<img src="https://img.shields.io/badge/YAML-CB171E?style=for-the-badge&logo=yaml&logoColor=white"/>
<img src="https://img.shields.io/badge/AWS%20CLI-232F3E?style=for-the-badge&logo=gnubash&logoColor=white"/>

</div>

## 📂 Project Structure

```text
devops-roadmap/
│
├── 📁 .github/
│   └── 📁 workflows/
│       └── 📄 deploy.yml
│
├── 🌐 DevOps Roadmap (1).html
│
└── 📘 README.md
```

## ☁️ AWS Configuration

### 1️⃣ Create S3 Bucket

| ⚙️ Configuration | 📌 Value |
|---|---|
| Bucket Name | `github-actions-html-deploy-2026` |
| AWS Region | `ap-south-1` (Mumbai) |
| Hosting Type | Static Website Hosting |
| Index Document | `index.html` |

### 2️⃣ Enable Static Website Hosting

1. Open **AWS Management Console**
2. Navigate to **Amazon S3**
3. Select your bucket
4. Open **Properties**
5. Find **Static Website Hosting**
6. Click **Edit**
7. Enable **Static Website Hosting**
8. Select **Host a static website**
9. Set Index Document to `index.html`
10. **Save changes**

### 3️⃣ Configure IAM Permissions

Create an IAM user, or use an appropriately authorized IAM identity, for deployment.

| 🔑 Permission | 📝 Purpose |
|---|---|
| `s3:ListBucket` | List bucket contents |
| `s3:PutObject` | Upload the HTML file |
| `s3:DeleteObject` | Remove / overwrite objects |
| `sts:GetCallerIdentity` | Verify AWS identity in the pipeline |

> 🛡️ Restrict IAM permissions to the deployment bucket wherever possible.

### 4️⃣ Configure GitHub Secrets

Navigate to: **GitHub Repository → Settings → Secrets and variables → Actions → New repository secret**

| 🔐 Secret Name | 📝 Description |
|---|---|
| `AWS_ACCESS_KEY_ID` | AWS Access Key ID |
| `AWS_SECRET_ACCESS_KEY` | AWS Secret Access Key |

> ⚠️ **Never** store AWS credentials directly inside source code or workflow files.

## ⚙️ GitHub Actions CI/CD Pipeline

Create the workflow file: `.github/workflows/deploy.yml`

```yaml
name: HTML Website S3 Deployment

on:
  push:
    branches:
      - main

  workflow_dispatch:

jobs:
  deploy:
    name: Deploy HTML to AWS S3
    runs-on: ubuntu-latest

    steps:
      # Checkout GitHub Repository
      - name: Checkout Code
        uses: actions/checkout@v4

      # Verify HTML File
      - name: Verify Project Files
        run: |
          set -e
          test -f "DevOps Roadmap (1).html"
          echo "HTML file found successfully"

      # Configure AWS Credentials
      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: ap-south-1

      # Verify AWS Identity
      - name: Verify AWS Access
        run: |
          aws sts get-caller-identity

      # Deploy Website to S3
      - name: Deploy Website to S3
        run: |
          aws s3 cp "DevOps Roadmap (1).html" \
            s3://github-actions-html-deploy-2026/index.html \
            --content-type "text/html"

      # Deployment Status
      - name: Deployment Successful
        run: |
          echo "Website deployed successfully!"
```

## 🔍 Pipeline Explanation

<details>
<summary><b>🟦 Stage 1 — Checkout Code</b></summary>

```yaml
- name: Checkout Code
  uses: actions/checkout@v4
```

Downloads the source code from the GitHub repository into the GitHub Actions runner.
</details>

<details>
<summary><b>🟩 Stage 2 — Verify Project Files</b></summary>

```bash
test -f "DevOps Roadmap (1).html"
```

Checks whether the HTML file exists before deployment. If the file is missing, the pipeline **stops**.
</details>

<details>
<summary><b>🟧 Stage 3 — Configure AWS Credentials</b></summary>

```yaml
- name: Configure AWS Credentials
```

Uses GitHub Secrets to authenticate with AWS. The Access Key and Secret Access Key are securely provided to the workflow.
</details>

<details>
<summary><b>🟪 Stage 4 — Verify AWS Access</b></summary>

```bash
aws sts get-caller-identity
```

Verifies that GitHub Actions can successfully authenticate with AWS.
</details>

<details>
<summary><b>🟥 Stage 5 — Deploy Website to S3</b></summary>

```bash
aws s3 cp "DevOps Roadmap (1).html" \
s3://github-actions-html-deploy-2026/index.html \
--content-type "text/html"
```

Uploads the HTML file to the S3 bucket and saves it as `index.html`.
</details>

<details>
<summary><b>✅ Stage 6 — Deployment Successful</b></summary>

Displays a success message after the deployment command completes successfully.
</details>

## 🌐 S3 Static Website Access

After enabling Static Website Hosting, AWS provides a website endpoint.

**Find it here:** `S3 → Bucket → Properties → Static Website Hosting → Bucket Website Endpoint`

The website can be accessed through this endpoint once the required public-read access configuration is in place.

### 🔁 Workflow Trigger

| Trigger | Description |
|---|---|
| 🟢 `push` to `main` | Pipeline runs automatically |
| 🔵 `workflow_dispatch` | Manual execution from the Actions tab |

## ▶️ How to Execute the Project

```bash
# Step 1: Clone the repository
git clone https://github.com/ajaydhadi95-gif/devops-roadmap.git

# Step 2: Enter the project directory
cd devops-roadmap

# Step 3: Edit the HTML file  →  DevOps Roadmap (1).html

# Step 4: Commit your changes
git add .
git commit -m "Update HTML website"

# Step 5: Push to GitHub (triggers the pipeline 🚀)
git push origin main
```

**Step 6 — Verify the pipeline:**

1. Open the GitHub repository
2. Navigate to **Actions**
3. Select **HTML Website S3 Deployment**
4. Check the workflow execution logs
5. Verify that all deployment stages are successful

## ✅ Expected Pipeline Results

| 🔢 Pipeline Stage | 📊 Expected Status |
|---|:---:|
| Checkout Code | ✅ Success |
| Verify Project Files | ✅ Success |
| Configure AWS Credentials | ✅ Success |
| Verify AWS Access | ✅ Success |
| Deploy Website to S3 | ✅ Success |
| Deployment Successful | ✅ Success |

## 🛠️ Troubleshooting

<details>
<summary><b>❌ 1. HTML File Not Found</b></summary>

**Error**
```text
Error: Process completed with exit code 1.
```
**Solution:** Verify the correct HTML filename and repository path.
</details>

<details>
<summary><b>🔑 2. AWS Authentication Failed</b></summary>

**Error**
```text
Unable to locate credentials
```
**Solution:**
- Verify GitHub Secrets
- Check AWS Access Key ID
- Check AWS Secret Access Key
- Verify IAM permissions
</details>

<details>
<summary><b>🚫 3. S3 Access Denied</b></summary>

**Error**
```text
AccessDenied
```
**Solution:** Check IAM permissions and S3 bucket access configuration.
</details>

<details>
<summary><b>📜 4. S3 Bucket Policy Cannot Be Saved</b></summary>

**Check:**
- IAM `s3:PutBucketPolicy` permission
- Account-level Block Public Access settings
- Bucket-level Block Public Access settings
- AWS Organizations restrictions, if applicable
</details>

<details>
<summary><b>🔒 5. Website Shows 403 Forbidden</b></summary>

**Check:**
- Static Website Hosting is enabled
- `index.html` exists in the bucket root
- Bucket policy allows `s3:GetObject`
- Required public access settings permit the policy
- The correct S3 **website endpoint** is being used
</details>

## 🔐 Security Best Practices

- 🔑 Store AWS credentials in **GitHub Secrets**
- 🚫 Never commit AWS credentials to GitHub
- 🛡️ Apply **least-privilege** IAM permissions
- 🪪 Prefer **GitHub OIDC** over long-lived access keys for production
- 🙈 Avoid public access to private or sensitive S3 files
- 🌍 For production, use **CloudFront + private S3 + Origin Access Control**
- 📊 Enable versioning and appropriate monitoring where required

> [!WARNING]
> Public bucket access in this learning project is only for demonstrating S3 static website hosting. **Do not use this configuration for sensitive or production data.**

## 🎓 Key Learning Outcomes

After completing this project, you will understand:

1. ⚙️ How GitHub Actions works
2. 📝 How to create CI/CD pipelines using YAML
3. 🔗 How GitHub connects with AWS
4. 🔐 How AWS IAM authentication works
5. 🗝️ How to manage GitHub Secrets
6. 🪣 How to deploy static websites to Amazon S3
7. 🌐 How to configure S3 Static Website Hosting
8. 🧯 How to troubleshoot deployment failures and S3 Access Denied errors

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%" alt="divider"/>

## 🏁 Project Conclusion

Successfully implemented an automated CI/CD pipeline using **GitHub Actions** to deploy an HTML website to **Amazon S3**. The deployment is triggered automatically whenever new code is pushed to the `main` branch.

<div align="center">

![Status](https://img.shields.io/badge/Project%20Status-Successfully%20Deployed-2EA44F?style=for-the-badge&logo=checkmarx&logoColor=white)
![Cloud](https://img.shields.io/badge/Cloud-Amazon%20Web%20Services-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)
![CI/CD](https://img.shields.io/badge/CI%2FCD-GitHub%20Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white)

<br/>

[![Repository](https://img.shields.io/badge/GitHub-Repository-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/ajaydhadi95-gif/devops-roadmap)

<br/>

⭐ **If you found this project helpful, give it a star!** ⭐

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:2088FF,50:232F3E,100:FF9900&height=120&section=footer" alt="Footer"/>

</div>