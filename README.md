# 🔍 SonarQube Scan Workflow Template

This reusable GitHub Actions workflow is designed to run a **SonarQube scan** on a project’s codebase.  
It’s perfect for teams who want to keep code quality in check with minimal setup across multiple repos.

## 📦 Features
- ✅ Runs SonarQube SAST analysis
- 🧠 Reusable across projects via `workflow_call`
- 💪 Supports custom **self-hosted runners** (e.g. `ubuntu`, `gpu`, `project-specific` runners)
- 🔐 Secure token management using `secrets`

---

## 🛠 Usage

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