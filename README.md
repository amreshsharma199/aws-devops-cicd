# AWS DevOps & CI/CD - Module 06

**Module:** 06 | Day 25 - Day 27 | AWS DevOps & CI/CD
**Objective:** Learn Git, GitHub, Version Control, CI/CD and create a basic deployment pipeline on AWS.

## Key Objectives Covered
1. Git and GitHub fundamentals
2. Version control workflow (branching, merging, PR)
3. Continuous Integration & Continuous Deployment
4. AWS CI/CD concepts (CodeBuild, CodeDeploy, CodePipeline / GitHub Actions alternative)
5. Created basic deployment pipeline
6. Documented deployment workflow

## Project Structure
```
/app - Sample static web app (HTML/CSS/JS)
/.github/workflows/deploy.yml - CI/CD pipeline using GitHub Actions
buildspec.yml - For AWS CodeBuild (if using CodePipeline)
appspec.yml - For AWS CodeDeploy (if deploying to EC2)
deployment-workflow.md - Detailed documentation
```

## Pipeline Implemented
**Stack Used:** GitHub -> GitHub Actions -> AWS S3 + CloudFront (Static) / EC2 via CodeDeploy

**Flow:**
1. Developer pushes code to `main` branch on GitHub
2. GitHub Actions workflow `deploy.yml` triggers
3. Jobs: Checkout, Setup Node, Lint & Test, Build
4. AWS Credentials configured via OIDC (Recommended) / IAM Keys stored in GitHub Secrets
5. Sync build to S3: `aws s3 sync ./app s3://your-bucket-name --delete`
6. Invalidate CloudFront cache
7. Deployment success notification

## How to Setup Your Own
1. Create S3 bucket and enable static website hosting
2. Create IAM User with S3FullAccess & CloudFrontFullAccess (for demo) - In production use least privilege
3. Add secrets in GitHub: `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, `AWS_REGION`, `S3_BUCKET`, `CLOUDFRONT_DISTRIBUTION_ID`
4. Push code - pipeline will auto-deploy

## AWS CodePipeline Alternative (Traditional)
If using pure AWS:
Source: GitHub (via CodeStar Connection) -> CodeBuild (buildspec.yml) -> CodeDeploy (appspec.yml to EC2) -> Manual Approval -> Production

Both approaches documented in `deployment-workflow.md`

## Deliverables for Module 06
- [x] GitHub Repo: This repository
- [x] Learning Notes: learning-notes-hindi.md + deployment-workflow.md
- [x] LinkedIn Post: See linkedin-post.txt

Author: Amresh Sharma | ATS Module 06
