# Laboratory Work 5: CI/CD

This project contains a simple HTML/CSS application, Dockerfile, and GitHub
Actions workflow for building and publishing a Docker image to Docker Hub.

## Local formatting

```powershell
npx --yes prettier@3.3.3 --write "app/**/*.{html,css}"
```

## Docker image

```bash
docker build -t lab5-cicd-app .
docker run -d --name lab5-cicd-app -p 80:80 lab5-cicd-app
```

## Required GitHub repository secrets

```text
DOCKERHUB_USERNAME
DOCKERHUB_TOKEN
```

## Azure VM deployment

```bash
docker pull <DOCKERHUB_USERNAME>/lab5-cicd-app:latest
docker run -d --name lab5-cicd-app --restart always -p 80:80 <DOCKERHUB_USERNAME>/lab5-cicd-app:latest
docker run -d --name watchtower --restart always -e DOCKER_API_VERSION=1.44 -v /var/run/docker.sock:/var/run/docker.sock containrrr/watchtower lab5-cicd-app --interval 30
```
