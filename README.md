## CD-Deploy-Application-from-Jenkins-Pipeline-on-EC2-Instance--automatically-with-docker-compose

### Project Description:

Install Docker Compose on AWS EC2 Instance

Create docker-compose.yml file that deploys our web application image

Configure Jenkins pipeline to deploy newly built image using Docker Compose on EC2 server

Improvement: Extract multiple Linux commands that are executed on remote server into a separate shell script and execute the script from Jenkinsfile

### Here are the steps to complete the project:

### Step 1: Set up an AWS EC2 Instance

Create an AWS account if you don't have one already.

Launch an EC2 instance with Linux AMI installed and open required ports.

SSH into your EC2 instance using a terminal.

### Step 2: Install Docker and Docker Compose on EC2 Instance

Update the package list on your EC2 instance:

  sudo apt-get update
  
Install Docker on your EC2 instance:

  sudo apt-get install docker.io

Install Docker Compose on your EC2 instance:

  sudo apt-get install docker-compose

Step 3: Create docker-compose.yml file

Create a new directory for your project:

  mkdir my_project
  cd my_project

Create a docker-compose.yml file in the project directory:

  touch docker-compose.yml

Edit the docker-compose.yml file to define the services you want to deploy. For example, to deploy a Java web application, your docker-compose.yml file might look like this:

    version: '3'
  services:
    web:
      image: your-docker-hub-username/your-java-web-app-image
      ports:
        - "8080:8080"
        
Save and exit the file.

### Step 4: Push the Docker Image to Docker Hub

Build the Docker image for your application on your local machine:

  docker build -t your-docker-hub-username/your-java-web-app-image .
  
Log in to Docker Hub from your local machine:

  docker login
  
Push the Docker image to Docker Hub:

  docker push your-docker-hub-username/your-java-web-app-image
  
### Step 5: Configure Jenkins Pipeline

Install Jenkins on your EC2 instance.

Create a new Jenkins job and configure it to build your Java application using Maven.

Add the following script to your Jenkins Pipeline to deploy the newly built image using Docker Compose on EC2 server:

    pipeline {
      agent any
      stages {
        stage('Deploy') {
          steps {
            sh 'ssh user@your-ec2-instance "cd /path/to/your/project && docker-compose up -d"'
          }
        }
      }
    }

Run the Jenkins job to build and deploy your application.

### Step 6: Improvement

Create a new shell script deploy.sh on your local machine and copy all the Linux commands that are executed on the remote server from the Jenkinsfile to the deploy.sh file.

Add execute permissions to the script:

  chmod +x deploy.sh

Add the following script to your Jenkins Pipeline to execute the shell script from the Jenkinsfile:

    pipeline {
    agent any
    stages {
      stage('Deploy') {
        steps {
          sh './deploy.sh'
        }
      }
    }
  }

Update your deploy.sh file to include the SSH command to connect to the EC2 instance and run Docker Compose to deploy your application.

Run the Jenkins job to build and deploy your application using the improved Jenkinsfile.





