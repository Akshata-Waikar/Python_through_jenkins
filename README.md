# Automated Deployment of Flask-Based Student Registration App Using Jenkins on AWS EC2

## 🎯 Objective

The objective of this project is to develop and deploy a simple Flask-based **Student Registration Web Application** on an AWS EC2 live server using a **Jenkins CI/CD pipeline**. The application allows users to submit student details through a web form, which are then stored in a **MySQL database** hosted on **Amazon RDS**.

This project demonstrates:

- Web development using Flask (Python)
- Backend integration with MySQL
- DevOps practices using Jenkins for Continuous Deployment
- Full automation of deployment via Jenkins to a production EC2 server

---

## 📚 Introduction

This project demonstrates the **end-to-end automation** and deployment of a Flask-based Student Registration Web Application using Jenkins. The CI/CD pipeline pulls the latest code from GitHub and deploys it to a live EC2 instance via SSH.

Key integrations include:

- **Cloud infrastructure** (AWS EC2, RDS)
- **DevOps tools** (Jenkins, Git)
- **Web application stack** (Python, Flask, MySQL)

---

## 🛠️ Technology Stack

| Layer            | Tools/Services                           |
|------------------|------------------------------------------|
| Frontend         | HTML (Form-based)                        |
| Backend          | Python (Flask Framework)                 |
| Database         | MySQL (AWS RDS)                          |
| CI/CD            | Jenkins (Pipeline Job)                   |
| Version Control  | Git & GitHub                             |
| Deployment       | AWS EC2 (Live server)                    |
| Secure Access    | SSH Agent Plugin (Jenkins to EC2)        |
| Cloud Platform   | Amazon Web Services (EC2, RDS)           |

---

🚀 Implementation Steps

🔹 Step 1: Launch EC2 Instances
Instance 1: Jenkins Server
Instance 2: Live Web Server

🔹 Step 2: Setup Jenkins Server
-  sudo yum update -y
-  sudo yum install docker -y
-  sudo systemctl start docker
-  sudo systemctl enable docker
-  sudo usermod -aG docker ec2-user
-  docker run -d --name jenkins -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts

🔹 Step 3: Setup Jenkins Job
-  Create a Pipeline Job
-  Configure GitHub repo and Jenkinsfile
-  Use SSH Credentials to connect to the live EC2 server

🔹 Step 4: Setup Live EC2 Web Server
-  sudo yum update -y
-  sudo yum install git python3 -y
-  pip3 install flask mysql-connector-python
-  git clone https://github.com/Akshata-Waikar/Python_through_jenkins.git
-  cd Python_through_jenkins

Update db_config in app.py with your RDS endpoint and credentials.

🔹 Step 5: Setup RDS MySQL Database
-  Create an Amazon RDS (MySQL) instance
-  Database Name: studentsdb
-  Table: students (as shown above)

🔹 Step 6: Jenkinsfile Pipeline
-  The Jenkinsfile handles:
-  SSH to the live server
-  Cloning the latest code
-  Killing any existing Flask process
-  Restarting the application

🔹 Step 7: Trigger Jenkins Build
-  Automatically deploys updated Flask app to the live server

🔹 Step 8: Test Application
-  Visit: http://<Live_EC2_Public_IP>:5000
-  Submit form and check if data is stored in RDS.

✅ Conclusion
This project successfully implements a CI/CD pipeline using Jenkins to automate deployment of a Flask web application on AWS EC2, backed by an RDS MySQL database.
It demonstrates core DevOps practices:
- Git-based version control
- Jenkins-based automation
- Secure remote deployments via SSH
- Web application deployment in a production-like environment

Project Completed By : Akshata Waikar
