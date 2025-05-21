### Docker (10 Questions)

1. **What is Docker, and how does it differ from a VM?**
   - **Answer**: Docker is a containerization platform that packages apps with dependencies in lightweight containers, sharing the host OS kernel. VMs include a full OS, making them heavier. Example: Run a container with `docker run nginx`.
   - **DevOps Context**: Enables consistent, portable deployments.

2. **How do you write an optimized Dockerfile?**
   - **Answer**: Use a slim base image, minimize layers, and leverage multi-stage builds. Example:
     ```Dockerfile
     FROM python:3.9-slim AS builder
     WORKDIR /app
     COPY requirements.txt .
     RUN pip install --no-cache-dir -r requirements.txt
     COPY . .
     FROM python:3.9-slim
     WORKDIR /app
     COPY --from=builder /app .
     CMD ["python", "app.py"]
     ```
   - **DevOps Context**: Reduces image size and attack surface.

3. **How do you build and push a Docker image?**
   - **Answer**: Build with `docker build` and push to a registry. Example:
     ```bash
     docker build -t myrepo/my-app:1.0 .
     docker login myrepo
     docker push myrepo/my-app:1.0
     ```
   - **DevOps Context**: Integrates with CI/CD pipelines.

4. **How do you troubleshoot a container that exits immediately?**
   - **Answer**: Check logs (`docker logs`), inspect configuration (`docker inspect`), and verify CMD/ENTRYPOINT. Example:
     ```bash
     docker logs my-container
     docker run -it my-container /bin/sh  # Debug
     ```
     Fix issues like missing dependencies or incorrect commands.
   - **DevOps Context**: Ensures application reliability.

5. **What are Docker volumes, and how do you use them?**
   - **Answer**: Volumes persist data outside containers. Example:
     ```bash
     docker volume create my-volume
     docker run -v my-volume:/data my-app
     ```
     Use in Kubernetes with PersistentVolumes.
   - **DevOps Context**: Critical for stateful apps.

6. **How do you secure Docker containers?**
   - **Answer**: Run as non-root, limit capabilities, and use read-only filesystems. Example:
     ```bash
     docker run --user 1000 --cap-drop=ALL --read-only my-app
     ```
     Scan images with `docker scan` or Trivy.
   - **DevOps Context**: Enhances production security.

7. **What is Docker Compose, and how do you use it?**
   - **Answer**: Docker Compose defines multi-container apps. Example:
     ```yaml
     version: '3'
     services:
       web:
         image: my-app:1.0
         ports:
           - "8080:8080"
       redis:
         image: redis:7.0
     ```
     Run with `docker-compose up`.
   - **DevOps Context**: Simplifies local development and testing.

8. **How do you implement multi-stage builds in Docker?**
   - **Answer**: Use multiple `FROM` stages to separate build and runtime environments. Example:
     ```Dockerfile
     FROM node:18 AS builder
     WORKDIR /app
     COPY package.json .
     RUN npm install
     COPY . .
     RUN npm run build
     FROM nginx:alpine
     COPY --from=builder /app/build /usr/share/nginx/html
     ```
   - **DevOps Context**: Reduces image size.

9. **How do you network containers in Docker?**
   - **Answer**: Use bridge networks for isolation. Example:
     ```bash
     docker network create my-network
     docker run --network my-network --name web my-app
     docker run --network my-network --name db redis
     ```
     Containers communicate via service names.
   - **DevOps Context**: Prepares for Kubernetes networking.

10. **How do you integrate Docker with CI/CD?**
    - **Answer**: Build and push images in CI/CD pipelines. Example (GitHub Actions):
      ```yaml
      name: Build and Push Docker
      on:
        push:
          branches: [ main ]
      jobs:
        build:
          runs-on: ubuntu-latest
          steps:
            - uses: actions/checkout@v3
            - name: Build and Push
              run: |
                docker build -t myrepo/my-app:${{ github.sha }} .
                docker login -u ${{ secrets.DOCKER_USER }} -p ${{ secrets.DOCKER_PASS }}
                docker push myrepo/my-app:${{ github.sha }}
      ```
    - **DevOps Context**: Automates deployments.