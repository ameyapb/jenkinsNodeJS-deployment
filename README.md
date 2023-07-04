# Todo Node App

This repository contains the source code and configurations for a Todo Node App built with Node.js. The application is deployed and managed using Jenkins and Docker.

## Prerequisites

Before running the application, ensure that you have the following components set up:

- An EC2 instance with Ubuntu as the operating system.
- Java 11 installed on the EC2 instance.
- Jenkins installed and running on the EC2 instance.
- Docker installed on the EC2 instance.
- Node.js and npm (Node Package Manager) installed on the EC2 instance.

## Jenkins Setup

To set up Jenkins on your EC2 instance, follow these steps:

1. Update the package list and install Java 11:

   ```bash
   sudo apt update
   sudo apt install openjdk-11-jre
   
2. Install Jenkins:
    ```bash
    curl -fsSL https://pkg.jenkins.io/debian/jenkins.io.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
    echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
    sudo apt-get update
    sudo apt-get install jenkins

3. Enable and start Jenkins:
    ```bash
    sudo systemctl enable jenkins
    sudo systemctl start jenkins

4. Retrieve the initial admin password for Jenkins:
    ```bash
    sudo cat /var/lib/jenkins/secrets/initialAdminPassword

Access Jenkins through your browser by navigating to http://<EC2_INSTANCE_PUBLIC_IP>:8080, and enter the initial admin password when prompted.

Follow the instructions to set up Jenkins, including installing recommended plugins.

## Project Setup

Once Jenkins is set up, follow these steps to configure and deploy the Todo Node App:

1. Generate an SSH key pair on the EC2 instance:

   ```bash
    ssh-keygen
    Install Node.js and npm:

    sudo apt install nodejs
    sudo apt install npm

2. Clone this repository:
    ```bash
    git clone https://github.com/<YOUR_USERNAME>/<REPO_NAME>.git
    cd <REPO_NAME>
    
3. Install the project dependencies:
    ```bash
    npm install

4. Build the project:
    ```bash
    node app.js

5. Verify that the application is running correctly by accessing it at http://<EC2_INSTANCE_PUBLIC_IP>:8000.

## Docker Setup

To containerize the Todo Node App using Docker, perform the following steps:

1. Install Docker:
    ```bash
    sudo apt install docker.io

2. Build the Docker image:
    ```bash
    docker build . -t todo-node-app
    
3. Add the current user to the Docker group:
    ```bash
    sudo usermod -a -G docker $USER

4. Reboot the EC2 instance:
5. After rebooting, navigate to the project directory:
    ```bash
    cd /var/lib/jenkins/workspace/todo-node-app

6. Build the Docker image again:
    ```bash
   docker build . -t todo-node-app

7. Start a Docker container with the Todo Node App:
    ```bash
    docker run -d --name node-todo-app
