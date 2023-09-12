# Library Management System

Library Management System developed in Spring Boot, JPA, Hibernate, MySQL HTML, CSS, JavaScript.
What does it offer?

It allows user to manage Members, Categories, Books and Issueing Books.
Setup project
Setup database and run the project

    Project requires MySql database. Use Xampp
    Create a database and name it "sparklmsdb".
    Run the backend from SparkLmsApplication class.
    After running the backend just hit http://localhost:8080 to access the software.

Login

for login you may use username as 'admin' and password as 'admin'.

# AWS Server Provision and Deployment using CI/CD Pipeline

A complete CI/CD project with Jenkins pipeline to build and deploy a GitLab repository in AWS cloud.

## Project Description

Prepare EC2 Launch template to run with Auto-scaling. Configure a Route 53 domain and TLS certificate with a Load balancer for the application. Prepare RDS database for the VPC network. Configure a Jenkins CI/CD pipeline to build and run a Java application in an EC2 instance.

### Architecture Diagram

![AWS cloud deployment architecture diagram](./images/aws-deoloyment-diagram.png)

## Project Setup

### Pre-requisites

Prepare one virtual machines in RHEL 9 equivalent environment.

### Setup AWS services

- Create VPC, subnets, and route tables
- Create EC2 instance launch template
- Create SSL/TLS Certificate for Load balancer
- Create Auto scaling group and Load balancer
- Create RDS database
- Create Route 53 domain

### Setup Github repository

- Create Github repository
- Configure SSH key with developer and Gitlab.

### Prepare Jenkins server

#### Install Jenkins by Ansible

Follow this [jenkins-docker-setup-playbook](./ansible-playbook/docker-jenkins-installation) to setup Jenkins server by running Ansible playbook.
#### Configure Jenkins server tools and credentials

Tools setup:

- JDK - Name: `Java_11`, JAVA_HOME: `/usr/lib/jvm/java-11-openjdk`
- Git - Name: `Git`, Path executable: `/usr/bin/git`
- Maven - Name: `Maven_3`, MAVEN_HOME: `/usr/share/maven`

Credentials setup:

- Kind: 'SSH Username with private key', ID: `aws_ssh_key`, Username: `<username>`, Private key: Enter directly `<ssh-private-key>`.
- Kind: 'SSH Username with private key', ID: `gitlab_ssh_key`, Username: `<username>`, Private key: Enter directly `<ssh-private-key>`.

#### Configure new pipeline from dashboard

- Create New Item > Enter name (aws-deploy) > Select 'Pipeline' type.
- Goto 'Your pipeline' > Configure > Select Poll SCM > Set schedule `H/2 * * * *` > Select Pipeline script from SCM > Repository URL > Select your branch to build > Script Path (Jenkinsfile) > Save.
- Goto 'Your pipeline' > Build Now.

### Update application.properties for database host

Update RDS database host name in [application.properties](src/main/resources/application.properties) file.

## Deploy new update with CI/CD pipeline

Creating new commit in the repository will trigger a new build with following stages:

- Git Clone
- Build Artifact
- Push app to EC2
- [Run app using java service](./ansible-playbook/java-project-deploy-to-ec2)
- Update Running App
## PIPELINE WORKFLOW
In this module, we will configure a Jenkins Pipeline job to automate the build, test, and deployment process. The pipeline will integrate with Git, use Maven for building the project, and deploy the application to an EC2 instance using Ansible.

![AWS pipeline](./images/aws-pipeline.png)

## Browse the application from a browser

- Visit https://your-domain.com from your local browser.
- Use username 'admin' and password 'admin' to login to the dashboard.
