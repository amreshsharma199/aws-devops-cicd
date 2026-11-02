# Module 06 - AWS DevOps & CI/CD - Deep Learning Notes

## 1. Git aur GitHub Fundamentals (Hindi me Deep)
Git ek Distributed Version Control System (DVCS) hai. Iska matlab har developer ke paas code ka pura history hota hai.
- **Repository**: Aapke project ka folder jisme .git hidden folder hota hai, jo saare versions ko track karta hai.
- **Commit**: Ek snapshot. Har commit ka ek unique SHA hash hota hai. Message clear hona chahiye.
- **Branch**: Alag line of development. `main/master` production hota hai, `develop` aur `feature/*` branches par kaam hota hai.
- **GitHub**: Git ko cloud pe host karne ka platform. Collaboration, Pull Request, Issues sab yahan hota hai.

**Important Commands:**
git init, git clone, git add ., git commit -m "feat: add deployment", git push, git pull, git branch, git merge, git rebase

## 2. Version Control Kyu Jaruri Hai?
- Rollback kar sakte ho agar bug aaye
- Kaunsi line kisne kab change ki - blame dekh sakte ho
- Parallel development - bina ek dusre ka code tode
- CI/CD ka base hi version control hai

## 3. CI/CD - Continuous Integration / Continuous Deployment
**CI (Continuous Integration):** Har baar jab developer code push karta hai, to automatically Build + Test chalta hai. Agar test fail to turant pata chalta hai.
**CD ke 2 matlab:**
- Continuous Delivery: Build ke baad staging tak auto jata hai, production me manual approval
- Continuous Deployment: Seedha production tak auto jata hai

Benefits: Human error kam, fast release, chhote-chhote changes, feedback loop tez.

## 4. AWS CI/CD Concepts
AWS ke 4 main services hain:
1. **AWS CodeCommit**: GitHub jaisa, AWS ka private Git repo. (Ab CodeCommit close ho raha hai, isliye GitHub use karna standard hai)
2. **AWS CodeBuild**: Aapka code build karta hai. Yaha `buildspec.yml` file me commands likhte hain - npm install, npm test, docker build etc.
3. **AWS CodeDeploy**: Code ko EC2, Lambda, ya ECS par deploy karta hai. Blue/Green deployment support karta hai.
4. **AWS CodePipeline**: In sab ko jodne wala orchestrator. Source -> Build -> Test -> Deploy stages banate hain.

Alternative Modern Stack: GitHub Actions + AWS (S3 + CloudFront + EC2/Elastic Beanstalk) - Yehi maine is module me use kiya hai kyuki industry me sabse zyada yahi chalta hai.

## 5. Basic Deployment Pipeline Jo Maine Banayi
Pipeline Flow:
Developer Push to GitHub (main) -> GitHub Actions Trigger -> Steps:
1. Checkout Code
2. Setup Node.js / Python
3. Install Dependencies & Run Tests
4. Build Artifact
5. Configure AWS Credentials (IAM Role / Access Keys)
6. Deploy to AWS S3 (Static Hosting) + Invalidate CloudFront / Deploy to EC2 via CodeDeploy

Maine is repo me ek demo static app banayi hai jo S3 par deploy hoti hai. Agar aap EC2 chahte ho to CodeDeploy wala flow bhi README me diya hai.

## 6. Document Deployment Workflow - Key Learnings
- IAM User ko minimum permission do (Principle of Least Privilege)
- Secrets ko kabhi GitHub me hardcode mat karo, GitHub Secrets use karo
- buildspec.yml / workflow.yml me har step ka log rakho
- Deployment ke baad health check jarur lagao

Ye module ka core yahi hai: Version Control -> Automated Testing -> Automated Deployment -> Monitoring.
