# PROJECT 1: SECURE DIGITAL BANKING APPLICATION DEPLOYMENT ON AZURE

## Project Objective

**Deploy a secure two-tier digital banking application on Microsoft Azure using private networking and Azure DevOps CI/CD.**

~~High-Level Requirements~~

<!-- Blockquote -->
> **Note:** Make sure you have Node.js installed before running the project.

<!-- Table -->

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `api_key` | `string` | **Required**. Your API key |

1.	Create a Resource Group, Virtual Network and separate subnets for the web VM, database VM, private endpoints and App Service integration.
2.	Deploy:
o	Windows web VM for application testing
o	Windows database VM for SQL administration
o	Ubuntu VM as a self-hosted Azure DevOps agent
3.	Create an Azure SQL Database with public access disabled, a Private Endpoint and Private DNS. Allow access only from the database VM and Azure App Service.
4.	Create a Linux Azure App Service with Java 21. Configure a Private Endpoint for inbound access and VNet Integration for private connectivity to SQL and Key Vault.
5.	Configure NSG rules so that:
o	Web VM can access the Web App
o	Database VM cannot access the Web App
o	Database VM and App Service can access SQL
o	Web VM and local computer cannot access SQL
6.	Create Azure Key Vault with RBAC, Private Endpoint and Private DNS. 
7.	Enable Managed Identity for the Web App and grant minimum Key Vault access.
8.	Configure Azure DevOps with:
o	Azure Resource Manager Service Connection
o	Self-hosted Linux agent
o	Required Java, Maven, Node.js, npm, Git and Azure CLI tools
9.	Create a YAML pipeline to build the frontend, package the Spring Boot application, run tests, generate the JAR and deploy it to Azure App Service.
Expected Result
The banking application should be deployed successfully, accessible only through the approved private network, connected privately to Azure SQL, and able to retrieve secrets securely from Key Vault using Managed Identity.

Optional: Azure Monitoring


PROJECT 2: CI/CD PIPELINE FOR A .NET WEB APPLICATION USING AZURE DEVOPS AND BLUE-GREEN DEPLOYMENT
Project Objective

Build an end-to-end CI/CD pipeline for a .NET web application using Azure DevOps. Provision the required Azure infrastructure with Terraform and deploy the application to Development, Staging and Production environments.

High-Level Requirements
1.	Use Terraform to create:
o	Resource Groups
o	App Service Plans
o	Development App Service
o	Staging App Service
o	Production App Service
o	Green deployment slot for Production
2.	Run Terraform initialization, validation, planning and deployment to create the Azure resources.
3.	Create a Service Principal in Microsoft Entra ID and configure an Azure Resource Manager Service Connection in Azure DevOps.
4.	Create an Azure DevOps project and import the application repository.
5.	Create a CI pipeline to:
o	Install the required .NET SDK
o	Restore NuGet packages
o	Build the application
o	Run unit tests
o	Publish the application
o	Generate the deployment artifact
6.	Create a CD pipeline or multi-stage YAML pipeline to:
o	Deploy the artifact to Development
o	Deploy the same artifact to Staging
o	Deploy the new version to the Production Green slot
o	Validate the Green deployment
o	Swap Green with Production

Blue-Green Deployment Flow
The current Production application acts as Blue, while the Green slot receives the new release. After successful validation, perform a slot swap to make Green live. The previous Production version should remain available for rollback.

Expected Result
The application should be deployed successfully across Development, Staging and Production, with Production releases completed through Azure App Service slot swaps for minimal downtime and easy rollback.


PROJECT 3: DEVSECOPS PIPELINE FOR NODE.JS APPLICATION DEPLOYMENT TO AKS

Project Objective

Build an automated DevSecOps pipeline for a Node.js shopping cart application using Jenkins, Docker, Azure Container Registry, Azure Kubernetes Service, Helm and security scanning tools.

High-Level Requirements

1.	Create an Ubuntu VM for Jenkins and install Java, Jenkins, Docker, Node.js, Azure CLI, kubectl, Helm and Trivy.
2.	Integrate Jenkins with GitHub using a webhook so that every code push triggers the pipeline automatically.
3.	Configure SonarQube with a Quality Gate to scan the source code and stop the pipeline when quality or security checks fail.
4.	Configure Snyk to scan Node.js dependencies and block high-risk vulnerable packages.
5.	Build the Docker image and scan it using Trivy. Only approved images should continue to deployment.
6.	Create an Azure Service Principal and store all Azure and security tool credentials securely in Jenkins Credentials.
7.	Create an Azure Container Registry and push images using unique tags such as the build number or Git commit ID.
8.	Create an AKS cluster, integrate it with ACR and configure Jenkins to access the cluster.
9.	Create a Helm chart containing:
o	Deployment
o	Service
o	Ingress
o	Health checks
o	Resource requests and limits
o	Environment variables
o	Horizontal Pod Autoscaler
10.	Configure an Ingress Controller to expose the application and use HTTPS where possible.
11.	Configure HPA using CPU or memory utilization, with minimum and maximum replica limits.

Jenkins Pipeline Flow

The Jenkins pipeline should:
•	Check out the source code
•	Install npm dependencies
•	Run application tests
•	Run SonarQube analysis and verify the Quality Gate
•	Run Snyk dependency scanning
•	Build the Docker image
•	Run Trivy image scanning
•	Push the approved image to ACR
•	Connect to AKS
•	Validate the Helm chart
•	Deploy or upgrade the application using Helm
•	Verify pods, deployments, services, ingress and application availability

Expected Result

A GitHub code push should automatically trigger Jenkins. The pipeline should build, test and scan the application, publish the approved Docker image to ACR, and deploy it to AKS using Helm. The pipeline must stop whenever testing, security scanning or deployment fails.


PROJECT 4: DEPLOY A JAVA SPRING BOOT APPLICATION TO AKS USING MAVEN, DOCKER, ACR, SONAR TRIVY VIA JENKINS PIPELINE.
Repo: https://github.com/spring-projects/spring-petclinic
Set up a Build Pipeline (CI) using Jenkins to:
●	Clone the source code from GitHub.
●	Build the Spring Boot application using Maven.
●	Run unit tests to ensure code quality.
●	Package the application as a JAR file.
●	Run sonar analysis and publish the report
●	Create a Docker image from the packaged application.
●	Push the Docker image to Azure Container Registry (ACR).
●	Scan the Docker image for vulnerabilities using Trivy.

Set up a Release Pipeline (CD) using Jenkins to:
●	Connect to the Azure Kubernetes Service (AKS) cluster.
●	Apply Kubernetes deployment manifests for the application.
●	Expose the application using Kubernetes service or ingress.
●	Monitor deployment statatus

Project 5: Deploy a Node.js + MongoDB application to Azure App Service using Jenkins.

Repo: https://github.com/Azure-Samples/msdocs-nodejs-mongodb-azure-sample-app 

Pre-requisite or once Your pipeline set you can provision:
Deploy a Node.js-based Azure Web App using Terraform for infrastructure provisioning.

Set up a Build Pipeline (CI) using Jenkins to:
●	Clone the source code from GitHub.
●	Install project dependencies.
●	Build the Node.js application.
●	Run basic tests to validate functionality.
●	Package the application for deployment.
●	Publish the build artifacts to a shared location for the CD pipeline.

Set up a Release Pipeline (CD) using Jenkins to:
●	Retrieve the published artifact from the build pipeline.
●	Authenticate with Azure using a service principal.
●	Deploy the artifact to the previously provisioned Azure Web App.
●	Verify the deployment by checking the application health endpoint.
