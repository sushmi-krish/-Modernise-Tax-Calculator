# Modernise Tax Calculator
# Project Overview
This project modernizes the Tax Calculator web application by containerizing it with Docker and automating deployment using a Tekton CI/CD pipeline on IBM Cloud.

# Key Features

* Containerized application using Docker with Nginx web server
* Automated build, test, and deploy pipeline using Tekton
* Unit tests run automatically with Jasmine
* Deployment to IBM Cloud Container Registry and IBM Cloud Code Engine
* Secure credentials stored using Kubernetes Secrets

# Prerequisites
* Docker installed
* Access to IBM Cloud account
* Kubernetes cluster with Tekton Pipelines installed
* kubectl CLI configured
* IBM Cloud CLI installed
* Git installed

#SetUP & Usage
1. Clone the repository
   
     git clone https://github.com/sushmi-krish/-Modernise-Tax-Calculator.git
     cd -Modernise-Tax-Calculator

2. Build and run Docker image locally

  ```bash   docker build -t tax-calculator .
         docker run -p 8080:80 tax-calculator

Access the app at http://localhost:8080.

4. Create Kubernetes secret for IBM Cloud Container Registry
```bash
     kubectl create secret docker-registry docker-reg-creds \
  --docker-server=us.icr.io \
  --docker-username=iamapikey \
  --docker-password=<IBM_CLOUD_API_KEY> \
  --docker-email=<your-email>
  
4. Deploy Tekton pipeline and start PipelineRun
```bash kubectl apply -f pipeline/tasks/npm.yaml
kubectl apply -f pipeline/pipelines/tc-pipeline.yaml
kubectl apply -f pipeline/pipelineruns/tc-pipeline-run.yaml

5. Monitor pipeline execution
```bash
tkn pipelinerun logs -f

# Pipeline Stages

 * init: Cleans workspace
 * clone: Clones source code
 * npminstall: Installs Node.js dependencies
 * tests: Runs Jasmine unit tests
 * build: Builds Docker image and pushes to IBM Cloud

# Troubleshooting
* Ensure IBM Cloud API key is valid for Docker registry secret
* Verify PVC is bound for workspace storage
* Check pipeline logs for test failures or build errors

# Author
Sushmi-Krish






     




