# CI/CD Workflow Templates Documentation

# General

## SonarQube Scan Workflow Template

This reusable GitHub Actions workflow is designed to run a **SonarQube scan** on a project’s codebase.
It’s perfect for teams who want to keep code quality in check with minimal setup across multiple repos.

### 📦 Features

* ✅ Runs SonarQube SAST analysis
* 🧠 Reusable across projects via `workflow_call`
* 💪 Supports custom **self-hosted runners** (e.g. `ubuntu`, `gpu`, `project-specific` runners)
* 🔐 Secure token management using `secrets`

---

### 🛠 Usage

To use this workflow in your repo, call it from another workflow like this:

```yaml
# .github/workflows/sonarqube.yaml
name: Run SonarQube Scan

on:
  push:
    branches: [master]

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

## Snyk Scan Workflow Template

This reusable GitHub Actions workflow is designed to run a **Snyk scan** on a project’s codebase.
It’s ideal for identifying vulnerabilities in your dependencies with minimal setup across multiple repos.

### ✅ Prerequisites

You need to enable CodeQL under **Security → Code scanning alerts** in your repo settings.

### 📦 Features

* ✅ Runs Snyk SCA analysis
* 🧠 Reusable across projects via `workflow_call`
* 💪 Supports custom **self-hosted runners** (e.g. `ubuntu`, `gpu`, `project-specific` runners)
* 🔐 Secure token management using `secrets`

---

### 🛠 Usage

To use this workflow in your repo, call it from another workflow like this:

```yaml
# .github/workflows/snyk-scan.yaml
name: Run Snyk Scan

on:
  push:
    branches: [master]

jobs:
  Snyk-assessment:
    uses: astrearider/gh-workflows/.github/workflows/snyk-scan.yml@master
    with:
      RUNNER_LABELS: '"self-hosted", "ubuntu"'
    secrets:
      SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
```

---

## Gitguardian Scan Workflow Template

This job scans the repository for potential secrets (such as API keys, passwords, or other sensitive information).

### 📦 Features

* 🧠 Reusable across projects via `workflow_call`
* 💪 Supports custom **self-hosted runners** (e.g. `ubuntu`, `gpu`, `project-specific` runners)

---

### 🛠 Usage

To use this workflow in your repo, call it from another workflow like this:

```yaml
# .github/workflows/gitguardian-scan.yaml
name: Run GitGuardian Scan

on:
  push:
    branches: [master]
  pull_request:

jobs:
  gitguardian-assessment:
    uses: astrearider/gh-workflows/.github/workflows/gitguardian-scan.yml@master
    with:
      RUNNER_LABELS: '"self-hosted", "ubuntu"'
```
---

## Container Build Workflow Template

This reusable GitHub Actions workflow builds a container image using Docker without pushing it. It leverages docker/metadata-action to generate intelligent and consistent image tags based on Git refs, semantic versions, SHA, and a timestamp.

### 📦 Features
* 🔨 Builds a container image from your source code
* 🧠 Reusable across projects via workflow_call
* 🏷️ Automatically tags images with:
  * branch-latest
  * branch-timestamp (e.g. dev-20250611XXXXXX)
  * Git short SHA (e.g. sha-abc1234)
  * Semantic version (e.g. v1.0.1) if triggered from Git tag
* 💪 Supports custom self-hosted runners
* 🌐 Works with any container registry via CONTAINER_REGISTRY_URL
* 🔐 Secure credentials handling via secrets

### 🛠 Usage
To use this workflow in your repo, call it from another workflow like this:

```yaml
# .github/workflows/build-image.yaml
name: Build Container Image

on:
  push:
    branches: [master]
    tags: ['v*']

jobs:
  build-image:
    uses: astrearider/gh-workflows/.github/workflows/container-build.yml@master
    with:
      RUNNER_LABELS: '"self-hosted", "ubuntu"'
    secrets:
      CONTAINER_REGISTRY_URL: ghcr.io/your-org/your-app
```
### 🧪 Output
This workflow exposes the following output for downstream use:
* tags: Generated list of container tags like:
  * dev-latest
  * dev-20250611123456
  * sha-abc1234
  * v1.0.1 (if triggered from Git tag v1.0.1)


---

# Go Specific

## Gosec Scan Workflow Template

This reusable GitHub Actions workflow runs a **Gosec security scan** on your Go codebase.
It’s ideal for teams aiming to automate static security analysis for Go projects with minimal setup.

### 📦 Features

* ✅ Runs [Gosec](https://github.com/securego/gosec) static analysis for Go code
* 🧠 Reusable across projects via `workflow_call`
* 💪 Supports custom **self-hosted runners** (e.g. `ubuntu`, `gpu`, `project-specific` runners)
* 📄 Uploads scan reports as workflow artifacts

---

### 🛠 Usage

To use this workflow in your repo, call it from another workflow like this:

```yaml
# .github/workflows/gosec-scan.yaml
name: Run Gosec Scan

on:
  push:
    branches: [master]
  pull_request:

jobs:
  Gosec-assessment:
    uses: astrearider/gh-workflows/.github/workflows/gosec-scan.yml@master
    with:
      RUNNER_LABELS: '"self-hosted", "ubuntu"'
    # Add secrets if your workflow requires them
```

---

## Gofmt Check Workflow Template

This reusable GitHub Actions workflow checks that Go files are properly formatted using `gofmt`. It will **fail** the build if any files are not formatted.

### 📦 Features

* ✅ Fails pipeline on unformatted Go files
* 📦 Uploads list of unformatted files as an artifact for debugging
* 🧠 Reusable across projects via `workflow_call`
* 💪 Supports custom **self-hosted runners** (e.g. `ubuntu`, `gpu`, `project-specific` runners)

---

### 🛠 Usage

To use this workflow in your repo, call it from another workflow like this:

```yaml
# .github/workflows/gofmt-check.yaml
name: Go Code Format Check

on:
  push:
    branches: [master]
  pull_request:

jobs:
  gofmt:
    uses: astrearider/gh-workflows/.github/workflows/gofmt.yml@master
    with:
      RUNNER_LABELS: '"self-hosted", "ubuntu", "gpu", "project_a"'
```

---

*© 2025 Rizki Ramadhan Al-Mubaraq*
