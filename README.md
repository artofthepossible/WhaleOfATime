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
10. Setup up helm: brew install helm

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
   docker buildx build --builder your-dbc-builder your-dh-org/your-image-name:tag 

   docker buildx build --builder cloud-demonstrationorg-default demonstrationorg/workshop-prep-demo-alpaquita:v1.0 

   docker build -t demonstrationorg/workshop-prep-demo-alpaquita:v1.0 .


3. Verify the images via docker desktop by navigate to docker desktop> click images 

b. To verify via cli, Run the command via terminal:
   ```sh
   docker images

Verify the images via docker desktop by navigate to docker desktop> click images

c. Base Images
Discussion:
Spend time reviewing images built (size and packages).
Existing base image
FROM eclipse-temurin:21-jre-jammy 

What happens if you switch the base image to something like this:
FROM bellsoft/liberica-native-image-kit-container

What other ways can we optimzie the base images and packages

Using docker desktop and reviewing the base image how does the size and number of packages shift?
Which base images results in less vulnerabilities?

Temurin - eclipse-temurin:21-jdk-jammy: 
Size: 413.95 MB: 221 packages and 0 Critical and High CVEs 

Alpaquita - bellsoft/liberica-openjdk-alpine-musl: 
Size: 1.16 GB: 67 packages and 0 Critical and High CVEs

Alpaquita - bellsoft/liberica-openjdk-alpine:21: 
Size: 227.63 MB: 38 packages and 0 Critical and High CVEs

Bitnami - bitnami/java:21: 
Size: 981.07 MB: 197 packages and 0 Critical and High CVEs


# Reviewing Built Images with the Builds Tab

1. Open Docker Desktop:
   - Launch Docker Desktop from your applications menu.

2. Navigate to the Builds Tab:
   - Click on the "Builds" tab in Docker Desktop to see a list of your recent builds.

3. Select a Built Image:
   - Click on the image you want to review. This will open the details view for that image.

4. Review the Info Section:
   - The "Info" section provides general information about the image, such as the image ID, size, and creation date.

5. Review the Source Section:
   - The "Source" section shows the Dockerfile or build configuration used to create the image. This helps you understand the steps and commands used during the build process.

6. Review the Logs Section:
   - The "Logs" section contains the build logs, which provide detailed information about each step of the build process. You can see the output of each command executed during the build.

7. Review the History Section:
   - The "History" section shows a chronological list of all the layers and commands that were executed to create the image. This includes both cached and non-cached steps.

8. Walkthrough of Build Timing:
   - In the "History" section, you can see the timing for each step of the build process. This helps you identify which steps took the longest and whether they were cached or not.
   - Cached steps are typically faster because Docker reuses the existing layers instead of rebuilding them from scratch.

9. Adding `--sbom=true` and `--provenance=true` to Build Commands:
   - When you add `--sbom=true` and `--provenance=true` to your build commands, Docker includes additional metadata in the resulting image.
   - `--sbom=true` generates a Software Bill of Materials (SBOM) that lists all the components and dependencies included in the image.
   - `--provenance=true` adds provenance information, which provides details about the build environment and process, ensuring the integrity and authenticity of the image.

Example build command with `--sbom=true` and `--provenance=true`:
   ```sh
   docker build -t demonstrationorg/workshop-prep-demo-alpaquita:v1.0 --sbom=true --provenance=true .



This command specifies the use of the faster builder Docker build cloud: cloud-demonstrationorg-default builder and includes the --sbom and --provenance flags for generating SBOM and provenance information.

   docker buildx build --builder cloud-demonstrationorg-default --sbom=true --provenance=true -t demonstrationorg/workshop-prep-demo-alpaquita:v1.0 .

Walkthrough of Build Timing:
   - In the "History" section, you can see the timing for each step of the build process. This helps you identify which steps took the longest and whether they were cached or not.
   - Cached steps are typically faster because Docker reuses the existing layers instead of rebuilding them from scratch.

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



   ```sh
   docker scout cves demonstrationorg/workshop-prep-demo-alpaquita:v1.0
   



2. Review the output and address any vulnerabilities found.

3. Run the following command to analyze your image CVE using quickview: 
   ```sh
   docker scout quickview your-dh-org/your-image-name:tag



   docker scout quickview demonstrationorg/workshop-prep-demo-alpaquita:v1.0



Additional Docker Scout Commands
What's next:
    View vulnerabilities → docker scout cves demonstrationorg/workshop-prep-demo-alpaquita:v1.0

    View base image update recommendations → docker scout recommendations demonstrationorg/workshop-prep-demo-alpaquita:v1.0

    Include policy results in your quickview by supplying an organization → docker scout quickview demonstrationorg/workshop-prep-demo-alpaquita:v1.0 --org <organization>

Push to Docker Hub
1. Log in to Docker Hub if you haven't already:
Run the following command: 
   ```sh 
   docker login



2. Tag your Docker image for Docker Hub: 
   ```sh
   docker tag your-image-name:tag your-dockerhub-username/your-image-name:tag
   docker tag demonstrationorg/workshop-prep-demo-alpaquita:v1.0



3. Push the Docker image to Docker Hub:
   ```sh 
   docker push your-dockerhub-username/your-image-name:tag
   docker push demonstrationorg/workshop-prep-demo-alpaquita:v1.0



# Review Docker Scout Health Score on Docker Hub
Find Your Repository:
   - Navigate to your repository by searching for `your-dockerhub-username/your-image-name`.

4. Open the Repository:
   - Click on the repository to open its details page.

5. Review the Docker Scout Health Score:
   - On the repository page, you will see the Docker Scout health score. This score provides an overview of the security and quality of your image.
   - The health score is based on several factors, including vulnerabilities, outdated dependencies, and best practices.

6. Understand the Policies:
   - Click on the "Policies" tab to see the policies attached to your image. These policies may include:
     - Vulnerability Scanning: Checks for known vulnerabilities in the image layers.
     - Best Practices: Ensures the image follows Docker best practices, such as using a minimal base image and reducing the number of layers.
     - License Compliance: Verifies that all included software components comply with open-source licenses.
7. Enhance the Image Quality:
   - To improve the health score and enhance the image quality, consider the following steps:
     - Update Dependencies: Ensure all dependencies are up-to-date and free from known vulnerabilities.
     - Use a Minimal Base Image: Choose a minimal base image to reduce the attack surface and image size.
     - Optimize Layers: Combine commands in the Dockerfile to reduce the number of layers and improve build efficiency.
     - Add Metadata: Include labels and metadata in the Dockerfile to provide additional information about the image.
     - Enable SBOM and Provenance: Use `--sbom=true` and `--provenance=true` in your build commands to include a Software Bill of Materials and provenance information.

8. Rebuild and Push the Enhanced Image:
After making the necessary improvements, rebuild your Docker image:

   ```docker buildx build --builder your-dbc-builder --sbom=true --provenance=true -t your-dockerhub-username/your-image-name:tag .

Push the enhanced image to Docker Hub:
   ```docker push your-dockerhub-username/your-image-name:tag
Review the Updated Health Score:

Return to Docker Hub and review the updated Docker Scout health score to see the improvements.


### Create Helm chart
1. Initialize a helm chart for the app

   ```sh
   helm create spring-boot-app



This command will generate the following files:
   ```sh
   spring-boot-app/
├── .helmignore   # Contains patterns to ignore when packaging Helm charts.
├── Chart.yaml    # Information about your chart
├── values.yaml   # The default values for your templates
├── charts/       # Charts that this chart depends on
└── templates/    # The template files
    └── tests/    # The test files
   

 
1. Using the enhanced helm chart for the app deploy the app to the local k8 cluster

### Using Deploy app to local k8 cluster using
Steps to deploy your Spring Boot application to a local kind cluster using the provided Helm charts.

# Start Kubernetes on Docker Desktop

1. Open Docker Desktop:
   - Launch Docker Desktop from your applications menu.

2. Enable Kubernetes:
   - Click on the gear icon (⚙️) in the top-right corner to open the settings.
   - In the settings menu, navigate to the "Kubernetes" tab.
   - Check the box labeled "Enable Kubernetes".
   - Click "Apply & Restart" to apply the changes and restart Docker Desktop.

3. Wait for Kubernetes to Start:
   - Docker Desktop will take a few minutes to start Kubernetes. You can monitor the progress in the Docker Desktop status bar.
   - Once Kubernetes is running, you will see a green light next to "Kubernetes" in the Docker Desktop settings.

4. Verify Kubernetes is Running:
   - Open a terminal and run the following command to check the status of Kubernetes:
     ```sh
     kubectl get nodes
     ```
   - You should see a list of nodes indicating that Kubernetes is up and running.



5. Deploy an Application to Kubernetes:
   - You can now deploy your applications to the local Kubernetes cluster using `kubectl` commands or Kubernetes manifests.

Example:
```sh
kubectl apply -f your-kubernetes-manifest.yaml

Note: Replace your-kubernetes-manifest.yaml with the path to your Kubernetes manifest file. ```



Using KIND with Docker Desktop 
Steps to deploy your Spring Boot application to a local kind cluster using the provided Helm charts.

Configure kubectl to Use the kind Cluster:


```sh kubectl cluster-info --context docker-desktop
Kubernetes control plane is running at https://127.0.0.1:59872
CoreDNS is running at https://127.0.0.1:59872/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy



Navigate to the Helm Chart Directory:

Change directory to the Helm chart location:

Deploy the Application Using Helm:

Use Helm to deploy the application:

```sh
helm install spring-boot-app .




NAME: spring-boot-app
LAST DEPLOYED: Sun Dec 22 17:12:48 2024
NAMESPACE: default
STATUS: deployed
REVISION: 1
NOTES:
1. Get the application URL by running these commands:
  export POD_NAME=$(kubectl get pods --namespace default -l "app.kubernetes.io/name=spring-boot-app,app.kubernetes.io/instance=spring-boot-app" -o jsonpath="{.items[0].metadata.name}")
  export CONTAINER_PORT=$(kubectl get pod --namespace default $POD_NAME -o jsonpath="{.spec.containers[0].ports[0].containerPort}")
  echo "Visit http://127.0.0.1:8080 to use your application"
  kubectl --namespace default port-forward $POD_NAME 8080:$CONTAINER_PORT

Verify the Deployment:
Check the Helm Release: Verify that the Helm release is deployed successfully.
```sh
helm list



Check the status of the deployment:
```sh
kubectl get pods



Check the Pods: Ensure that the pods are running.

```sh
kubectl get services



Check the Logs: View the logs of the application pod to ensure it is running correctly.

```sh
kubectl logs <pod-name>




Access the Application:
Forward a local port to the service to access the application:

```sh
kubectl port-forward svc/spring-boot-app 8080:80



Forward a local port to the service to access the application:
kubectl port-forward svc/spring-boot-app 8080:80

Open your browser and navigate to http://localhost:8080 to access the Spring Boot application.

 ### Workshop Deliverables
 . Completed Dockerfile, Compose, Ignore and Readme Files
 . Published image in docker hub
 . Testcontainers based integration test
 . Access to workship Github repo for reference
 

 
###Common Errors
InvalidImageName

Workarounds
##
Redeploy the Application:

After updating the image name, redeploy the application using Helm:

helm upgrade --install spring-boot-app .

Check the Pod Status:

Verify the status of the pods to ensure they are running:
kubectl get pods

Check the Logs Again:

Once the pods are running, check the logs again:

kubectl logs spring-boot-app-5598c996f-rnpt7

## Troubleshooting Image Pull Errors

spring-boot-app-5955589b69-rn85w   0/1     ImagePullBackOff   0          16s


If you encounter an `ErrImagePull` or `ImagePullBackOff` error, follow these steps:

spring-boot-app-5955589b69-rn85w   0/1     ErrImagePull   0          65s
The error ErrImagePull and ImagePullBackOff indicates that Kubernetes is trying and failing to pull the specified Docker image. This usually happens due to an incorrect image name, tag, or lack of access to the Docker registry.

Workarounds
Verify Image Name and Tag:

Ensure the image name and tag specified in the deployment are correct.

Example:
```sh
image:
  repository: your-dockerhub-username/your-image-name
  tag: tag



Check Image Availability:

Verify that the image is available in the Docker registry:

```sh
docker pull your-dockerhub-username/your-image-name:tag



Authenticate Docker Registry:

Ensure that the Kubernetes cluster has access to the Docker registry. If the image is private, create a Kubernetes secret for Docker registry authentication:

kubectl create secret docker-registry regcred \
  --docker-server=https://index.docker.io/v1/ \
  --docker-username=your-dockerhub-username \
  --docker-password=your-dockerhub-password \
  --docker-email=your-email@example.com

  Update Deployment to Use the Secret:

Update the deployment to use the created secret:

spec:
  containers:
    - name: spring-boot-app
      image: your-dockerhub-username/your-image-name:tag
  imagePullSecrets:
    - name: regcred

    Redeploy the Application:

Redeploy the application using Helm:

helm upgrade --install spring-boot-app .

Verify Pod Status:

Check the status of the pods to ensure they are running:

kubectl get pods

Check Logs:

Once the pods are running, check the logs to ensure the application is starting correctly:

kubectl logs spring-boot-app-5955589b69-rn85w

CrashLoopBackOff
spring-boot-app-754b5d687f-68tp6   0/1     CrashLoopBackOff   3 (18s ago)   64s

Check Resource Limits:

Verify that the resource limits specified in the Helm chart values file or Kubernetes deployment YAML file are appropriate for the application:

resources:
  limits:
    cpu: "500m"
    memory: "512Mi"
  requests:
    cpu: "250m"
    memory: "256Mi"

Check Liveness and Readiness Probes: Ensure that the liveness and readiness probes are correctly configured. Misconfigured probes can cause the pod to be killed and restarted.

livenessProbe:
  httpGet:
    path: /
    port: http
  initialDelaySeconds: 30
  periodSeconds: 10

readinessProbe:
  httpGet:
    path: /
    port: http
  initialDelaySeconds: 30
  periodSeconds: 10


Check for Application-Specific Issues: If the application requires specific environment variables, configuration files, or dependencies, ensure they are correctly set up in the Helm chart.

Check Kubernetes Events:

kubectl get events

Error:  bind: address already in use]

lsof -i :port
kill -9 port