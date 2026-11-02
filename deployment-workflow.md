# Deployment Workflow Documentation - Module 06

## 1. Overview
This document explains the complete deployment workflow implemented for Module 06.

## 2. Tools & Services
- Git & GitHub for Version Control
- GitHub Actions for CI/CD
- AWS S3 for hosting
- AWS CloudFront for CDN
- AWS IAM for security

## 3. Version Control Strategy
- `main` branch is production-ready and protected
- `develop` for integration
- `feature/*` branches for new work
- Conventional Commits: feat, fix, docs, chore
- Pull Request requires 1 review (simulated)

## 4. CI/CD Pipeline Definition (GitHub Actions)

File: `.github/workflows/deploy.yml`

Stages:
1. **CI - Continuous Integration**
   - Trigger on push to main / pull_request
   - Run `npm install` (or no-op for static)
   - Run linting & unit tests
   - Build artifact (dist folder)

2. **CD - Continuous Deployment**
   - Authenticate to AWS using OIDC
   - Sync artifact to S3
   - Invalidate CloudFront
   - Health check via curl on live URL

## 5. Security & Permissions
- No hardcoded AWS keys in repo
- Used GitHub Encrypted Secrets
- S3 bucket policy: Public Read only for website, Write only via IAM
- CloudFront OAC (Origin Access Control) enabled
- IAM Policy follows Least Privilege

## 6. Buildspec for CodeBuild (Alternative)
```yaml
version: 0.2
phases:
  install:
    commands:
      - echo Installing...
  build:
    commands:
      - echo Building static app...
      - cp -r app/* dist/
artifacts:
  files:
    - '**/*'
  base-directory: dist
```

## 7. Deployment Verification
- Check S3 sync logs
- Verify CloudFront deployment status: Deployed
- Curl live URL expecting HTTP 200
- Rollback plan: Revert Git commit and re-push, or restore previous S3 version (versioning enabled)

## 8. Learnings & Best Practices
- Keep pipeline fast (<3 mins)
- Fail fast - test before build
- Infrastructure as Code next step: Use Terraform/CloudFormation
- Monitoring: Add CloudWatch alarms for S3/CloudFront errors

## 9. Future Improvements
- Add Blue/Green deployment for EC2/ECS
- Integrate AWS CodePipeline for fully managed AWS-native flow
- Add automated E2E tests with Cypress
