 ## Automated Container Deployment on AWS cloud

 Module name: Networks & System Administration

 Student name: Abin Sebastian

 Student ID: 20089590




## Project Overview

- 'This project demonstrates a complete DevOps CI/CD pipeline that automatically deploys a containerized Python Flask web application to an AWS EC2 instance.'

## The system uses:

- 'Terraform → Infrastructure as Code (EC2 + Security Group)'

- 'Ansible → Server configuration (Docker installation)'

- 'Docker → Containerization of Flask application'

- 'GitHub Actions → CI/CD automation'

- 'AWS EC2 → Cloud hosting'

Whenever code is pushed to GitHub, the application is automatically built and deployed to AWS.
System Architecture

Local Machine

⬇

GitHub Repository

⬇

GitHub Actions (CI/CD Pipeline)

⬇ (SSH Connection)

AWS EC2 Instance

⬇

Docker Container (Flask App)

⬇

Access via EC2 Public IP

Project Structure


CA1/

│

├── terraform/

│       

         ├── main.tf

│

├── ansible/

│   

         ├── inventory.ini
      
│  

         ├── install_docker.yml
            
│   

         ├── deploy_app.yml
│
├── app/

│  

          ├── app.py
     
│    

          ├── requirements.txt
         
│ 

          ├── Dockerfile
          
│

├── .github/

│ 
 
          └── workflows/
        
│  

          └── deploy.yml
          
│

          └── README.md
          
## Implementation Steps

### Step 1 – Infrastructure Provisioning (Terraform)

 Terraform is used to create:

- 'EC2 Instance (Ubuntu)'

- 'Security Group (Allow SSH – 22, HTTP – 80)'

**command used:**

-cd terraform

-terraform init

-terraform plan

-terraform apply

Terraform automatically provisions the EC2 instance in AWS.

### Step 2 – Server Configuration (Ansible)

- Ansible installs Docker on the EC2 instance.

**Command Used:**

-ansible-playbook install_docker.yml -i inventory.ini

## Tasks Performed:

- 'Update apt packages'

- 'Install Docker'

- 'Start Docker service'

### Step 3 – Application Development (Flask App)

-Simple Python Flask web application.

- 'app.py'
   Runs on port 5000.

- 'requirements.txt'

- 'Lists Python dependencies (Flask).'

- 'Dockerfile'

Defines how the Docker image is built.

### Step 4 – Containerization (Docker)

- 'Docker builds and runs the Flask app inside a container.'

-docker build -t flask-app . 

-docker run -d -p 80:5000 flask-app

# Port Mapping:

- 'EC2 Port 80 → Container Port 5000'

### Step 5 – Version Control (Git & GitHub)

## Project initialized with Git:

-git init

-git add .

-git commit -m "Initial commit"

-git push -u origin main

### Step 6 – CI/CD Pipeline (GitHub Actions)

- 'Workflow file located at:'

.github/workflows/deploy.yml

- 'Pipeline triggers on:'

push to main branch

- 'Pipeline performs:'

## Connect to EC2 using SSH

- 'Pull latest code'

- 'Build Docker image'

- 'Run container'

- 'Deploy updated application'

- 'GitHub Secrets Used'

### The following secrets were added in GitHub:

- 'EC2_HOST → Public IP of EC2'

- 'EC2_USER → ubuntu'

- 'EC2_SSH_KEY → Private key (.pem file)'

These are securely stored and used by GitHub Actions.

Accessing the Application

After successful deployment:

### Open browser and enter:

http://34.244.46.223

## The Flask webpage will load successfully.

## Challenges Faced & Solutions

- 'Large file push rejected'
  
-Added .terraform/ to .gitignore

- 'GitHub workflow permission error'

-Created PAT with workflow scope

- 'Docker permission denied'

-Used sudo or added user to docker group

 - 'Webpage not accessible'

-Configured Security Group & port mapping

## Key Learnings

- 'Infrastructure as Code using Terraform'

- 'Configuration management with Ansible'

- 'Docker containerization'

- 'CI/CD automation with GitHub Actions'

- 'Secure cloud deployment on AWS'
