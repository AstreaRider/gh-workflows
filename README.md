# General
## 🔍 SonarQube Scan Workflow Template

This reusable GitHub Actions workflow is designed to run a **SonarQube scan** on a project’s codebase.  
It’s perfect for teams who want to keep code quality in check with minimal setup across multiple repos.

### 📦 Features
- ✅ Runs SonarQube SAST analysis
- 🧠 Reusable across projects via `workflow_call`
- 💪 Supports custom **self-hosted runners** (e.g. `ubuntu`, `gpu`, `project-specific` runners)
- 🔐 Secure token management using `secrets`

---

### 🛠 Usage

To use this workflow in your repo, call it from another workflow like this:

```yaml
# .github/workflows/sonarqube.yaml
name: Run SonarQube Scan

on:
  push:
    branches: [main]

jobs:
  SAST-assessment:
    uses: astrearider/gh-workflows/.github/workflows/sonarqube-scan.yml@master
    with:
      SONAR_HOST_URL: "http://your-sonarqube-server:9000"
      RUNNER_LABELS: '"self-hosted", "ubuntu"'
    secrets:
      SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
```
---
## 🛡️ Snyk Scan Workflow Template

This reusable GitHub Actions workflow is designed to run a **Snyk scan** on a project’s codebase.  
It’s ideal for identifying vulnerabilities in your dependencies with minimal setup across multiple repos.

### ✅ Prerequisites
You need to enable Codeql, check Security → Code scanning alerts

### 📦 Features
- ✅ Runs Snyk SCA analysis
- 🧠 Reusable across projects via `workflow_call`
- 💪 Supports custom **self-hosted runners** (e.g. `ubuntu`, `gpu`, `project-specific` runners)
- 🔐 Secure token management using `secrets`

---

### 🛠 Usage

To use this workflow in your repo, call it from another workflow like this:

```yaml
# .github/workflows/snyk-scan.yaml
name: Run Snyk Scan

on:
  push:
    branches: [main]

jobs:
  Snyk-assessment:
    uses: astrearider/gh-workflows/.github/workflows/snyk-scan.yml@master
    with:
      RUNNER_LABELS: '"self-hosted", "ubuntu"'
    secrets:
      SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
```

---
# Go specific

## 🔒 Gosec Scan Workflow Template

This reusable GitHub Actions workflow runs a **Gosec security scan** on your Go codebase.  
It’s ideal for teams aiming to automate static security analysis for Go projects with minimal setup.

### 📦 Features
- ✅ Runs [Gosec](https://github.com/securego/gosec) static analysis for Go code
- 🧠 Reusable across projects via `workflow_call`
- 💪 Supports custom **self-hosted runners** (e.g. `ubuntu`, `gpu`, `project-specific` runners)
- 📄 Uploads scan reports as workflow artifacts

---

### 🛠 Usage

To use this workflow in your repo, call it from another workflow like this:

```yaml
# .github/workflows/gosec-scan.yaml
name: Run Gosec Scan

on:
  push:
    branches: [main]
  pull_request:

jobs:
  Gosec-assessment:
    uses: astrearider/gh-workflows/.github/workflows/gosec-scan.yml@master
    with:
      RUNNER_LABELS: '"self-hosted", "ubuntu"'
    # Add secrets if your workflow requires them
```
---
