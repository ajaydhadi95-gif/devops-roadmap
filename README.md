# GitHub Actions CI/CD Pipeline – Deploy HTML Website on AWS S3

## Project Overview

This project demonstrates an end-to-end CI/CD pipeline using **GitHub Actions and AWS S3** to automatically deploy a static HTML website.

Whenever a developer pushes code to the `main` branch, GitHub Actions automatically triggers the deployment pipeline, authenticates with AWS, and uploads the HTML website to an S3 bucket.

## Architecture

```text
Developer
    |
    | Git Push
    v
GitHub Repository
    |
    v
GitHub Actions
    |
    | Checkout Code
    | Verify HTML File
    | Configure AWS Credentials
    | Verify AWS Identity
    |
    v
AWS IAM Authentication
    |
    v
Amazon S3 Bucket
    |
    | Upload HTML as index.html
    v
S3 Static Website Hosting
    |
    v
Live Website
```

## Technologies Used

- AWS S3
- AWS IAM
- GitHub Actions
- Git
- GitHub Secrets
- HTML
- YAML
- AWS CLI

## Project Structure

```text
devops-roadmap/
│
├── .github/
│   └── workflows/
│       └── deploy.yml
│
├── DevOps Roadmap (1).html
│
└── README.md
```

## AWS Configuration

### 1. Create S3 Bucket

Create an S3 bucket with the following configuration:

| Configuration | Value |
|---|---|
| Bucket Name | github-actions-html-deploy-2026 |
| AWS Region | ap-south-1 (Mumbai) |
| Hosting Type | Static Website Hosting |
| Index Document | index.html |

### 2. Enable Static Website Hosting

1. Open AWS Management Console.
2. Navigate to Amazon S3.
3. Select your bucket.
4. Open Properties.
5. Find Static Website Hosting.
6. Click Edit.
7. Enable Static Website Hosting.
8. Select Host a static website.
9. Set Index Document to `index.html`.
10. Save changes.

### 3. Configure IAM Permissions

Create an IAM user or use an appropriately authorized IAM identity for deployment.

Required permissions for this pipeline:

- `s3:ListBucket`
- `s3:PutObject`
- `s3:DeleteObject`

For AWS identity verification, `sts:GetCallerIdentity` is also used.

The IAM permissions should be restricted to the deployment bucket wherever possible.

### 4. Configure GitHub Secrets

Navigate to:

GitHub Repository → Settings → Secrets and variables → Actions → New repository secret.

Add the following secrets:

| Secret Name | Description |
|---|---|
| AWS_ACCESS_KEY_ID | AWS Access Key ID |
| AWS_SECRET_ACCESS_KEY | AWS Secret Access Key |

Never store AWS credentials directly inside source code or workflow files.

## GitHub Actions CI/CD Pipeline

Create the workflow file:

`.github/workflows/deploy.yml`

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

## Pipeline Explanation

### Stage 1: Checkout Code

```yaml
- name: Checkout Code
  uses: actions/checkout@v4
```

Downloads the source code from the GitHub repository into the GitHub Actions runner.

### Stage 2: Verify Project Files

```bash
test -f "DevOps Roadmap (1).html"
```

Checks whether the HTML file exists before deployment.

If the file is missing, the pipeline stops.

### Stage 3: Configure AWS Credentials

```yaml
- name: Configure AWS Credentials
```

Uses GitHub Secrets to authenticate with AWS.

AWS Access Key and Secret Access Key are securely provided to the workflow.

### Stage 4: Verify AWS Access

```bash
aws sts get-caller-identity
```

Verifies that GitHub Actions can successfully authenticate with AWS.

### Stage 5: Deploy Website to S3

```bash
aws s3 cp "DevOps Roadmap (1).html" \
s3://github-actions-html-deploy-2026/index.html \
--content-type "text/html"
```

Uploads the HTML file to the S3 bucket and saves it as `index.html`.

### Stage 6: Deployment Successful

Displays a success message after the deployment command completes successfully.

## S3 Static Website Access

After enabling Static Website Hosting, AWS provides a website endpoint.

Open:

S3 → Bucket → Properties → Static Website Hosting → Bucket Website Endpoint.

The website can be accessed through this endpoint after the required public-read access configuration is in place.

## GitHub Actions Workflow Trigger

The pipeline automatically runs whenever code is pushed to the `main` branch.

Manual execution is also supported through `workflow_dispatch`.

## How to Execute the Project

### Step 1: Clone Repository

```bash
git clone https://github.com/ajaydhadi95-gif/devops-roadmap.git
```

### Step 2: Enter Project Directory

```bash
cd devops-roadmap
```

### Step 3: Make Changes

Update the HTML file:

`DevOps Roadmap (1).html`

### Step 4: Commit Changes

```bash
git add .
git commit -m "Update HTML website"
```

### Step 5: Push to GitHub

```bash
git push origin main
```

### Step 6: Verify Pipeline

1. Open GitHub Repository.
2. Navigate to Actions.
3. Select HTML Website S3 Deployment.
4. Check the workflow execution logs.
5. Verify that all deployment stages are successful.

## Expected Pipeline Results

| Pipeline Stage | Expected Status |
|---|---|
| Checkout Code | Success |
| Verify Project Files | Success |
| Configure AWS Credentials | Success |
| Verify AWS Access | Success |
| Deploy Website to S3 | Success |
| Deployment Successful | Success |

## Troubleshooting

### 1. HTML File Not Found

Error:

```text
Error: Process completed with exit code 1.
```

Solution:

Verify the correct HTML filename and repository path.

### 2. AWS Authentication Failed

Error:

```text
Unable to locate credentials
```

Solution:

- Verify GitHub Secrets.
- Check AWS Access Key ID.
- Check AWS Secret Access Key.
- Verify IAM permissions.

### 3. S3 Access Denied

Error:

```text
AccessDenied
```

Solution:

Check IAM permissions and S3 bucket access configuration.

### 4. S3 Bucket Policy Cannot Be Saved

Check:

- IAM `s3:PutBucketPolicy` permission.
- Account-level Block Public Access settings.
- Bucket-level Block Public Access settings.
- AWS Organizations restrictions, if applicable.

### 5. Website Shows 403 Forbidden

Check:

- Static Website Hosting is enabled.
- `index.html` exists in the bucket root.
- Bucket policy allows `s3:GetObject`.
- Required public access settings permit the policy.
- The correct S3 website endpoint is being used.

## Security Best Practices

- Store AWS credentials in GitHub Secrets.
- Never commit AWS credentials to GitHub.
- Apply least-privilege IAM permissions.
- Prefer GitHub OIDC authentication over long-lived access keys for production.
- Avoid public access to private or sensitive S3 files.
- For production websites, use CloudFront with a private S3 bucket and Origin Access Control.
- Enable versioning and appropriate monitoring where required.

**Note:** Public bucket access in this learning project is only for demonstrating S3 static website hosting. Do not use this configuration for sensitive or production data.

## Key Learning Outcomes

After completing this project, you will understand:

1. How GitHub Actions works.
2. How to create CI/CD pipelines using YAML.
3. How GitHub connects with AWS.
4. How AWS IAM authentication works.
5. How to manage GitHub Secrets.
6. How to deploy static websites to Amazon S3.
7. How to configure S3 Static Website Hosting.
8. How to troubleshoot deployment failures and S3 Access Denied errors.

## Project Conclusion

Successfully implemented an automated CI/CD pipeline using GitHub Actions to deploy an HTML website to Amazon S3.

The deployment process is triggered automatically whenever new code is pushed to the GitHub `main` branch.

**Project Status: Successfully Deployed**

**GitHub Repository:** https://github.com/ajaydhadi95-gif/devops-roadmap

**Cloud Platform:** Amazon Web Services (AWS)

**CI/CD Tool:** GitHub Actions
