# GitHub Actions Workflow for Docker Image Build, Push, and Vulnerability Scanning

This repository contains a GitHub Actions workflow that automates the process of building a Docker image, pushing it to Docker Hub (or any other container registry), and scanning it for vulnerabilities using [Trivy](https://github.com/aquasecurity/trivy). The Docker image is tagged with the unique GitHub commit SHA for each build.

## How to Use This Workflow

### Step 1: Add the Workflow File

1. Create a new folder called `.github/workflows/` in your repository if it doesn't already exist.
2. Inside that folder, add new file  `file-name.yml`.
3. Copy the content of `github-action-trivy.yaml`.

### Step 2: Add Docker Hub Credentials as GitHub Secrets

To push images to Docker Hub (or another registry), you need to store your credentials securely as GitHub Secrets:

1. Go to your GitHub repository.
2. Navigate to **Settings > Secrets and variables > Actions**.
3. Add the following secrets:
   - **`DOCKER_USERNAME`**: Your Docker Hub username.
   - **`DOCKER_PASSWORD`**: Your Docker Hub password (or personal access token if preferred).

### Step 3: Customize the Workflow

- **Branch**: In the `on: push: branches:` section, replace `<branch-name>` with the branch that will trigger the workflow (e.g., `main` or `develop`).
- **Docker Hub Username and Image Name**: In the `docker buildx build` and `trivy image` steps, replace `<your-dockerhub-username>` with your Docker Hub username and `<your-image-name>` with the name of the image you're building and pushing.

### Workflow Summary

- **Step 1: Checkout Code**  
   The workflow checks out the code from the repository.

- **Step 2: Docker Hub Login**  
   It logs in to Docker Hub using the credentials stored in GitHub Secrets.

- **Step 3: Docker Build and Push**  
   It builds a Docker image using `docker buildx` and pushes the image to Docker Hub. The image is tagged with the unique commit SHA (`github.sha`) to differentiate each build.

- **Step 4: Trivy Scan**  
   It installs Trivy, scans the built image for vulnerabilities, and reports the results.

