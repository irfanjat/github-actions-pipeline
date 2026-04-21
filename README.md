# 🚀 CI/CD Pipeline with GitHub Actions & Docker

![CI/CD Pipeline](https://img.shields.io/badge/CI%2FCD-GitHub%20Actions-2088FF?style=for-the-badge&logo=github-actions&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-18-339933?style=for-the-badge&logo=node.js&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

An automated CI/CD pipeline that builds, tests, and deploys a Dockerized Node.js application to Docker Hub on every push to the `main` branch — powered by GitHub Actions.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Pipeline Workflow](#pipeline-workflow)
- [Prerequisites](#prerequisites)
- [Setup & Configuration](#setup--configuration)
- [Project Structure](#project-structure)
- [Secrets Configuration](#secrets-configuration)
- [Usage](#usage)
- [Contributing](#contributing)

---

## 🔍 Overview

This repository demonstrates a fully automated CI/CD pipeline using **GitHub Actions**. On every push to the `main` branch, the pipeline automatically:

1. Checks out the latest code
2. Sets up a Node.js 18 environment
3. Installs project dependencies
4. Runs the test suite
5. Builds a Docker image
6. Pushes the image to **Docker Hub**

---

## ⚙️ Pipeline Workflow

```yaml
name: CI-CD Pipeline
on:
  push:
    branches: [main]
```

### Jobs

#### `build-test`
Runs on `ubuntu-latest` and executes the following steps:

| Step | Action | Description |
|------|--------|-------------|
| 1 | `actions/checkout@v3` | Checks out the repository code |
| 2 | `actions/setup-node@v3` | Sets up Node.js v18 |
| 3 | `npm install` | Installs all dependencies |
| 4 | `echo "..."` | Runs the test suite |
| 5 | `docker build` | Builds the Docker image locally |
| 6 | `mr-smithers-excellent/docker-build-push@v4` | Builds & pushes image to Docker Hub |

---

## ✅ Prerequisites

Before getting started, make sure you have the following:

- A [GitHub](https://github.com) account
- A [Docker Hub](https://hub.docker.com) account
- A `Dockerfile` in the root of your project
- Node.js project with a valid `package.json`

---

## 🛠️ Setup & Configuration

### 1. Clone the Repository

```bash
git clone https://github.com/irfanjat/github-action.git
cd github-action
```

### 2. Add Your Dockerfile

Make sure a `Dockerfile` exists in the root of your project. Example:

```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["node", "index.js"]
```

### 3. Configure GitHub Secrets

Navigate to your repository → **Settings** → **Secrets and variables** → **Actions**, and add the following secrets:

| Secret Name | Description |
|-------------|-------------|
| `DOCKER_USERNAME` | Your Docker Hub username |
| `DOCKER_PASSWORD` | Your Docker Hub password or access token |

### 4. Push to Main

```bash
git add .
git commit -m "Trigger CI/CD pipeline"
git push origin main
```

The pipeline will trigger automatically! 🎉

---

## 📁 Project Structure

```
├── .github/
│   └── workflows/
│       └── ci-cd.yml       # GitHub Actions workflow file
├── Dockerfile               # Docker build instructions
├── package.json             # Node.js dependencies & scripts
├── app.js                 # Application entry point
└── README.md                # You are here
```

---

## 🔐 Secrets Configuration

> ⚠️ **Never hardcode credentials** in your workflow files. Always use GitHub Secrets.

To create a Docker Hub access token (recommended over password):

1. Log in to [Docker Hub](https://hub.docker.com)
2. Go to **Account Settings** → **Security** → **New Access Token**
3. Copy the token and add it as `DOCKER_PASSWORD` in GitHub Secrets

---

## 🐳 Docker Image

The built image is published to Docker Hub at:

```
docker.io/irfanjat/github-action:latest
```

To pull and run the image locally:

```bash
docker pull irfanjat/github-action
docker run -p 3000:3000 irfanjat/github-action
```

---

## 🚦 Pipeline Status

The pipeline runs on every push to `main`. You can monitor runs in the **Actions** tab of this repository.

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a new branch: `git checkout -b feature/your-feature`
3. Commit your changes: `git commit -m 'Add some feature'`
4. Push to the branch: `git push origin feature/your-feature`
5. Open a Pull Request

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

---

<p align="center">Made with ❤️ using GitHub Actions & Docker</p>
