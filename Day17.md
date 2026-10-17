# Ansible- Auto-healing for web server

-name: Configure Auo-healing for web server
 hosts: all
 become: yes
 tasks: 
   - name: Ensure nginx service is running
     service: 
       name: nginx
       state: started
       enabled: yes
   - name: Setup auto-restart for nginx service
     lineinfile: 
       path: /etc/systemd/system/nginx.service.d/override.conf
       line: "Restart=always"
       create: yes
   - name: Reload systemd
     command: systemctl daemon-reload
     
# Terraform - Multi-Cloud Infrastructure with Aws and azure

# Aws Vpc

resource "aws_vpc""main" {

  cidr_block = "10.0.0.0/16"
  

} 

# Azure Vnet

resource "azurerm_virtual_network" "main" {
  name = "pathnex-vnet"
  location = "East US"
  address_space = ["10.0.0.0/16"]
  resource_group_name = azurerm_resource_group.main.name

}

# Ec2 instance in aws

resource "aws_instance" "pathnex_ec2" {

ami = "ami-3tettefeggdh"
instance_type = "t2.micro"
region = "us-east-1"

}

# Virtual machine  

resource "azurerm_linux_virtual_machine" "pathnex_vm" {

  name                = "pathnex-azure-vm"
  resource_group_name = "azurerm_resource_group.main.name"
  location            = "azurerm_resource_group.main.location"
  size                = "Standard_B1s"
  admin_username      = "azureuser"
  admin_password      = "P@ssword123!"

} 


 # Kubernetes - Self-Healing with Liveness and Readiness Probes
   
apiVersion: apps/v1
kind: Deployment
metadata: 
  name: pathnex-web-app
spec: 
  replicas: 3
  selector: 
    matchlabels: 
      app: pathnex-web-app
  template: 
    metadata: 
      labels: 
        app: pathnex-web-app
    spec: 
      containers: 
        - name: nginx
          image: nginx
          ports: 
            - containerPort: 80
          livenessProbe:
            httpGet: 
              path: /healthz
              port: 80
            intialDelaySeconds: 5
            periodSeconds: 10
          readinessProbe: 
            httpGet: 
              path: /healthz
              port: 80
            intialDelaySeconds: 5
            periodSeconds: 10

# Jenkinsfile - Rolling Deployments with Kubernetes

 pipeline {

     agent any
     environment {
        IMAGE_NAME = 'pathnex-web-app'
      

}
stages {
    stage('Build') {
        steps{
            echo 'Building Docker image...'
            docker.build("${env.IMAGE_NAME}")
            


}



}
  stage('Test') {
      steps {
        echo 'Running tests....'

}


}
stage ('Deploy to Kubernetes'){
    steps {
        script {
            sh 'kubectl apply -f kubernetes/deployment.yaml'
            sh 'kubectl rollout status deployment/pathnex-web-app'

}



}


}
}


}

 

# Gitlab CI/CD - Multi-Cloud Deployment
 
stages: 
  - build
  - push
  - deploy

build: 
  stage: build
  script: 
    - docker build -t pathnex-web-app .

push: 
  stage: push
  script: 
    - docker login -u "$CI_REGISTRY_USER" -p "$CI_REGISTRY_PASSWORD"
    - docker push pathnex-web-app 

deploy_aws:
  stage: deploy
  script: 
    - kubectl --context=aws-cluster apply -f kubernetes/deployment.yaml

deploy_azure:
  stage: deploy
  script: 
    - kubectl --context=azure-cluster apply -f kubernetes/deployment.yaml


# Docker

# MySQL container (Note - Here " \ " means to be continue - it can be written in a single line" 

docker run -d \
--name pathnex-mysql \
- e MYSQL_ROOT_PASSWORD=root \
mysql:8


# Real Path 

/var/lib/mysql




 
