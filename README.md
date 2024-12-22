# WhaleOfATime
Unboxing Docker Desktop, DockerScout, Docker Build Cloud, Docker Scout and Testcontainers

### WORKSHOP: Containerizing a Real World Sprint Boot Application

## Workshop Objectives:
1. Understand the basics of containerization and its advantages
2. Learn how to containerize a Sprint boot application using docker desktop
3. Explore the Docker ecosystem (Docker Desktopm Docker Hub, Docker Build Cloud, Docker Scout, Testcontainers)
4. Implement containerization best pracitces for a production-ready Spring Boot Application

## Workshop Agenda:

# Before the workshop
1. Setup docker desktop 4.36
2. Gain access to docker hub organization for workshop {insert org name}
3. Gain access to docker hub (workshop buildaer)
4. Enable access to to docker scout (workshop repo)
5. Gain access to to Testcontainers organization (workshop repo)
6. Enable access to github
7. Docker Desktop Installed and running
8. Docker Hub Account
9. Enable [docker extension for copilot](https://docs.docker.com/copilot/) 

# Setting up the Environment (15 minutes)
1: git clone https://github.com/artofthepossible/WhaleOfATime

2. With Docker Desktop Installed and running. Ensure the output shows Docker version 4.36.x 
docker --version

3. Gain access to Docker Hub organization for workshop:
docker login

4. Ensure Docker Scout is installed and accessible.
docker scout --version

5. Ensure the GitHub CLI (gh) is installed and accessible.
gh --version

### WORKSHOP: Step-By-Step Guide: Containerize ad Spring Boot Application
Note! 

Replace `your-image-name`, `tag`, and `your-dockerhub-username` with your actual image name, tag, and Docker Hub username.
Replace `your-image-name`, `tag`, and `your-dockerhub-username` with your actual image name, tag, and Docker Hub username.

# Using Docker Init to Create the Docker Assets

1. Open a terminal in the root directory of your project.
2. Run the following command to initialize Docker assets:
   ```sh
   docker init

This command will generate the following files:
Dockerfile
compose.yaml
.dockerignore
README.Docker.md

2. Review and customize the generated files as needed for your project.


 # Build the Docker Image with Docker Build Cloud

1. Open a terminal in the root directory of your project.
2. Run the following command to build the Docker image using Docker Build Cloud:
   ```sh
   docker buildx build --platform linux/amd64,linux/arm64 -t your-image-name:tag .

   # Build the Docker Image

# Test Locally using Testcontainers
1. Ensure you have Testcontainers set up in your project.

2. Write a test case using Testcontainers to spin up the Docker container and run your tests.

3. Run your tests using your preferred test framework, for example:

./gradlew test

or

mvn test


# Secure using Docker Scout
Run the following command to scan your Docker image for vulnerabilities using Docker Scout:

docker scout cves your-image-name:tag

Review the output and address any vulnerabilities found.

# Push to Docker Hub
1. Log in to Docker Hub if you haven't already:
Run the following command: ```sh
docker login

2. Tag your Docker image for Docker Hub:
```sh docker tag your-image-name:tag your-dockerhub-username/your-image-name:tag

3. Push the Docker image to Docker Hub:

``` docker push your-dockerhub-username/your-image-name:tag

