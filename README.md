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
   docker buildx build --builder your-dh-org/your-dh-org --tag your-dh-org/your-image-name:tag 


3. Verify the images via docker desktop by navigate to docker desktop> click images 

b. To verify via cli, Run the command via terminal:
   ```sh
   docker images


Test Locally
1. Run the container locally: 
   ```sh 
   docker compose up --build

b. Alternate command to run the container: 
   ```sh 
   docker run -p 8080:8080 spring-boot-app:1.0

2. Access the application at http://localhost:8080
   ```sh 
   curl localhost:8080

Test Locally using Testcontainers

1. Ensure you have Testcontainers set up in your project.

 
2. Write a test case using Testcontainers to spin up the Docker container and run your tests.

a. Add Testcontainers dependencies to your project: 
   ```sh 
   placeholder for pom.xml dependencies

b. Write a Testcontainer-based integration test: 
   ```sh 
   placeholder for code

3. Run your tests using your preferred test framework, for example: 
   ```sh 
   ./gradlew test or  sh mvn test


Secure using Docker Scout
1. Run the following command to scan your Docker image for vulnerabilities using Docker Scout: 
   ```sh
   docker scout cves your-dh-org/your-image-name:tag

2. Review the output and address any vulnerabilities found.

3. Run the following command to analyze your image CVE using quickview: 
   ```sh
   docker scout quickview your-dh-org/your-image-name:tag

Push to Docker Hub
1. Log in to Docker Hub if you haven't already:
Run the following command: 
   ```sh 
   docker login

2. Tag your Docker image for Docker Hub: 
   ```sh
   docker tag your-image-name:tag your-dockerhub-username/your-image-name:tag

3. Push the Docker image to Docker Hub:
   ```sh 
   docker push your-dockerhub-username/your-image-name:tag

### Create Helm charts and inser
1. Within the 
   ```sh
   placeholder insert some helm charts samples

# Start Kubernetes on Docker Desktop

1. **Open Docker Desktop**:
   - Launch Docker Desktop from your applications menu.

2. **Enable Kubernetes**:
   - Click on the gear icon (⚙️) in the top-right corner to open the settings.
   - In the settings menu, navigate to the "Kubernetes" tab.
   - Check the box labeled "Enable Kubernetes".
   - Click "Apply & Restart" to apply the changes and restart Docker Desktop.

3. **Wait for Kubernetes to Start**:
   - Docker Desktop will take a few minutes to start Kubernetes. You can monitor the progress in the Docker Desktop status bar.
   - Once Kubernetes is running, you will see a green light next to "Kubernetes" in the Docker Desktop settings.

4. **Verify Kubernetes is Running**:
   - Open a terminal and run the following command to check the status of Kubernetes:
     ```sh
     kubectl get nodes
     ```
   - You should see a list of nodes indicating that Kubernetes is up and running.

5. **Deploy an Application to Kubernetes**:
   - You can now deploy your applications to the local Kubernetes cluster using `kubectl` commands or Kubernetes manifests.

Example:
```sh
kubectl apply -f your-kubernetes-manifest.yaml

Note: Replace your-kubernetes-manifest.yaml with the path to your Kubernetes manifest file. ```

 ### Workshop Deliverables
 . Completed Dockerfile, Compose, Ignore and Readme Files
 . Published image in docker hub
 . Testcontainers based integration test
 . Access to workship Github repo for reference
 

 
