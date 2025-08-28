CI/CD Node.js Project with GitHub Actions & EC2 Deployment
Overview

This project demonstrates a CI/CD pipeline for a Node.js application using GitHub Actions.
The application is automatically tested and deployed to an AWS EC2 instance whenever code is pushed to the main branch.

Key features:
Automated build and test using Node.js and Jest
Automatic deployment to EC2 using SSH
Process management using PM2
Easy to extend for any Node.js app

Tech Stack
Node.js – Backend runtime
Express.js – Web server framework
Jest – Testing framework for unit tests
PM2 – Process manager to keep app running
GitHub Actions – CI/CD automation
AWS EC2 – Deployment serve

Getting Started
1. Clone the repository
git clone https://github.com/alishasaiyed7/aws-devops-projects-basic.git
cd "aws-ci-cd"

2. Install dependencies locally (optional)
npm install

3. Run the app locally
node app.js


Visit http://localhost:3000 in your browser to see the app running.

CI/CD Pipeline (GitHub Actions)
Workflow File: .github/workflows/ci-cd.yml
1️⃣ Build Job
Runs on: Ubuntu latest

Steps:
Checkout the repo code
Setup Node.js version 18
Install dependencies
Run unit tests using Jest

2️⃣ Deploy Job

Runs on: Ubuntu latest
Triggered: After build succeeds on main branch

Steps:
Checkout the code
Connect to EC2 using SSH (via appleboy/ssh-action)
Pull the latest code from GitHub
Install dependencies on EC2
Start or restart the app using PM2

Secrets Required for Deployment

Create these secrets in your GitHub repo settings under Settings → Secrets → Actions:

Secret Name	Description
EC2_HOST	Public IP or DNS of your EC2 instance
EC2_USER	EC2 username (e.g., ubuntu)
EC2_SSH_KEY	Private key content for SSH access

App.js Example
const express = require('express');
const app = express();
const port = 3000;

app.get("/", (req, res) => {
  res.send('Hello from GitHub Actions CI/CD Pipeline!<br>Hey, Let\'s test multi-line output.');
});

app.listen(port, () => console.log(`App running on port ${port}`));

Key Tools

Jest: Used for testing Node.js code. Ensures app behaves as expected before deployment.
PM2: Keeps Node.js app running in background and handles restarts automatically.

Deployment Steps Manually (Optional)

SSH into EC2
ssh -i "your-key.pem" ubuntu@<EC2_PUBLIC_IP>


Clone repo (if not already)
git clone https://github.com/alishasaiyed7/aws-devops-projects-basic.git

Navigate to project folder
cd "aws-ci-cd"

Install dependencies

npm install

Start the app
pm2 start app.js --name "ci-cd-app"

To restart after new code
pm2 restart ci-cd-app

ow CI/CD Works

Developer pushes code to GitHub main branch.

GitHub Actions runs:

Install dependencies
Run Jest tests

If build passes, it connects to EC2 and:
Pulls latest code
Installs dependencies
Restarts app using PM2
The latest version of the app is live automatically.

Testing the Pipeline
Update app.js with a new message or HTML.
Push to main.
GitHub Actions will automatically:
Run tests

Deploy new version to EC2
Access the app via http://<EC2_PUBLIC_IP>:3000

Learning Outcomes

Implemented end-to-end CI/CD for Node.js projects.
Learned Jest testing, PM2 process management, and GitHub Actions automation.
Gained hands-on experience deploying Node.js apps to AWS EC2.
Practiced SSH-based automation using GitHub Secrets.
