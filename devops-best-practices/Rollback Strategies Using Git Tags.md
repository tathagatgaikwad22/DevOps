# 馃攣 Rollback Strategies Using Git Tags in Production Pipelines

## 馃 Overview
In production environments, rolling back to a stable release is critical when something goes wrong after deployment.  
**Git tags** make this process reliable and traceable 鈥� acting as "restore points" for your production code.

This guide explains how Git tags can be used effectively for versioning, release management, and safe rollbacks.

---

## 馃摌 What Are Git Tags?
Git tags are references that point to specific commits. They鈥檙e often used to mark **release versions** such as `v1.0`, `v2.3.1`, etc.

There are two types:
- **Lightweight Tag** 鈥� A simple pointer to a commit.
- **Annotated Tag** 鈥� Contains metadata (author, message, date) 鈥� ideal for production releases.

```bash
# Annotated Tag Example
git tag -a v2.3.0 -m "Production release v2.3.0"
git push origin v2.3.0
```

---

## 鈿欙笍 How Tags Help in CI/CD Pipelines

Many CI/CD tools like **Jenkins**, **GitHub Actions**, and **GitLab CI** can automatically trigger builds or deployments when a tag is pushed.

### 鉁� Example: GitHub Actions Workflow

```yaml
name: Deploy on Tag
on:
  push:
    tags:
      - 'v*'

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Deploy to Production
        run: |
          echo "Deploying version ${GITHUB_REF#refs/tags/} to production"
          # Insert deployment commands here
```

### 鉁� Example: Jenkins Pipeline Snippet

```groovy
pipeline {
  agent any
  triggers { pollSCM('* * * * *') } // Example trigger

  stages {
    stage('Deploy on Tag') {
      when { expression { env.GIT_TAG != null } }
      steps {
        echo "Deploying ${env.GIT_TAG} to production"
        // Deployment logic here
      }
    }
  }
}
```

---

## 馃毃 Rollback Process

### 1锔忊儯 Identify the last stable release tag
```bash
git tag
# Example output: v2.1.0 v2.2.0 v2.3.0
```

### 2锔忊儯 Checkout the previous stable version
```bash
git checkout v2.2.0
```

### 3锔忊儯 Redeploy the older version
Redeploy your application using your CI/CD pipeline or manual deployment command.

### 4锔忊儯 (Optional) Create a rollback tag
```bash
git tag -a rollback-v2.2.0 -m "Rollback to version v2.2.0"
git push origin rollback-v2.2.0
```

---

## 馃З Best Practices

鉁� Always use **annotated tags** for production releases.  
鉁� Follow **Semantic Versioning** (`vMAJOR.MINOR.PATCH`) for clarity.  
鉁� Protect your `main` or `prod` branch from direct commits 鈥� only tag merged, tested code.  
鉁� Automate tagging and deployment triggers through CI/CD.  
鉁� Maintain a changelog linked to tags for transparency.  

---

## 鈿� Common Mistakes to Avoid

馃毇 Deleting or renaming production tags 鈥� breaks traceability.  
馃毇 Using local-only tags 鈥� always push tags to remote.  
馃毇 Skipping version documentation 鈥� makes debugging harder.  

---

## 馃 Pro Tip: Automate Tagging

You can generate tags dynamically from your CI/CD pipeline:
```bash
VERSION=$(date +'%Y.%m.%d.%H%M')
git tag -a "v$VERSION" -m "Automated release $VERSION"
git push origin "v$VERSION"
```

---

## 馃弫 Conclusion

Git tags bring stability and traceability to your production releases.  
They enable **version-controlled deployments, instant rollbacks, and release clarity** across your DevOps pipelines.

> 馃挕 Always tag what you deploy 鈥� it might save your production one day!

---

**Author:** Tathagat Gaikwad   
**Topic:** Rollback Strategies Using Git Tags in Production Pipelines  
