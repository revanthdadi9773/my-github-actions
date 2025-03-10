# GitHub Actions CI/CD Pipeline Guide

## Introduction
GitHub Actions is a powerful tool that allows developers to automate workflows for building, testing, and deploying applications. This document explains how to configure a CI/CD pipeline using GitHub Actions with a step-by-step breakdown of YAML syntax.

---

## 1️⃣ What is a CI/CD Pipeline?
A CI/CD pipeline automates the process of **building, testing, security checking, and deploying code** whenever a change is made. The key stages include:

- **Build**: Install dependencies and compile the code (if needed).
- **Test**: Run unit and integration tests.
- **Security Check**: Scan for vulnerabilities.
- **Deploy**: Release the application to production.

---

## 2️⃣ YAML Syntax for GitHub Actions
GitHub Actions uses YAML files to define workflows. These files are stored in the `.github/workflows/` directory.

### Basic Structure:
```yaml
name: Python CI/CD Pipeline  # 1️⃣ Workflow Name

on: [push, pull_request]  # 2️⃣ Triggers for the workflow

jobs:  # 3️⃣ Defines the jobs in the pipeline
  build:  # 4️⃣ Job Name
    runs-on: ubuntu-latest  # 5️⃣ Runner Environment

    steps:  # 6️⃣ List of steps for this job
      - name: Checkout Code  # 7️⃣ Step Name
        uses: actions/checkout@v3  # 8️⃣ GitHub Action to fetch code
      
      - name: Set up Python
        uses: actions/setup-python@v3
        with:
          python-version: '3.9'  # 9️⃣ Passing inputs to the action

      - name: Install Dependencies
        run: pip install -r requirements.txt  # 🔟 Running a shell command

      - name: Run Tests
        run: pytest tests/
```

---

## 3️⃣ Explanation of YAML Headings
| **Heading** | **Purpose** | **Example** |
|------------|------------|------------|
| `name:` | Workflow name for identification | `name: Python CI/CD Pipeline` |
| `on:` | Defines when the workflow should run | `on: [push, pull_request]` |
| `jobs:` | Specifies different tasks (build, test, deploy) | `jobs: build:` |
| `runs-on:` | Defines the OS environment for the runner | `runs-on: ubuntu-latest` |
| `steps:` | Lists actions or commands to execute | `steps:` |
| `uses:` | Calls a pre-built GitHub Action | `uses: actions/setup-python@v3` |
| `run:` | Runs shell commands inside the workflow | `run: pip install -r requirements.txt` |
| `with:` | Passes inputs to an action | `with: python-version: '3.9'` |
| `if:` | Runs a step only if a condition is met | `if: github.ref == 'refs/heads/main'` |

---

## 4️⃣ Common CI/CD Steps with GitHub Actions
### 🔹 **Build Step (Install Dependencies)**
```yaml
- name: Install Dependencies
  run: pip install -r requirements.txt
```
### 🔹 **Test Step (Run Unit Tests)**
```yaml
- name: Run Tests
  run: pytest tests/
```
### 🔹 **Linting (Code Quality Check)**
```yaml
- name: Lint Code
  run: flake8 .
```
### 🔹 **Security Check (Scan for Vulnerabilities)**
```yaml
- name: Security Scan with Bandit
  run: bandit -r .
```
### 🔹 **Deploy to AWS (Example Deployment Step)**
```yaml
- name: Deploy to AWS
  uses: aws-actions/configure-aws-credentials@v2
  with:
    aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
    aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
    aws-region: us-east-1
```

---

## 5️⃣ Best Practices for Writing Workflows
✅ Use **small and modular jobs** for better performance.  
✅ Run **tests before deployment** to avoid broken code in production.  
✅ Use **environment variables** and **secrets** to store sensitive information.  
✅ Implement **caching** to speed up workflow execution.  

Example:
```yaml
- name: Cache Dependencies
  uses: actions/cache@v3
  with:
    path: ~/.cache/pip
    key: ${{ runner.os }}-pip-${{ hashFiles('**/requirements.txt') }}
    restore-keys: |
      ${{ runner.os }}-pip-
```

---

## 6️⃣ How to Use This Pipeline in Your Project?
1. Create a `.github/workflows/ci.yml` file in your repository.
2. Copy the sample YAML file into it.
3. Commit and push your code to GitHub.
4. Check the **Actions tab** in your repository to see the workflow running.

---

## 7️⃣ Conclusion
GitHub Actions simplifies the CI/CD process by automating **building, testing, security scanning, and deployment**. Mastering these concepts will help you in **DevOps** and **software development** roles.

🔹 **Next Steps:** Try modifying the pipeline to include **custom deployment steps** or **additional security checks**!

