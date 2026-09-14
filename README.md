# 🛒 Java Spring Boot E-Commerce Application

A hands-on **Java Spring Boot e-commerce application** used to practice **Maven-based builds, Jenkins Continuous Integration (CI), GitHub integration, and AWS EC2 deployment**.

This repository demonstrates the application build and deployment workflow from source code to a runnable JAR artifact on an AWS EC2 instance.

> **DevOps Workflow:**
> GitHub → Jenkins → Maven Build → JAR Artifact → AWS EC2 → Running Application

---

## 📋 Table of Contents

* [📖 Project Overview](#-project-overview)
* [🏗️ Architecture & Workflow](#️-architecture--workflow)
* [🛠️ Technology Stack](#️-technology-stack)
* [📋 Prerequisites](#-prerequisites)
* [🚀 Application Setup](#-application-setup)
* [🔨 Maven Build](#-maven-build)
* [⚙️ Jenkins CI Pipeline](#️-jenkins-ci-pipeline)
* [☁️ AWS EC2 Deployment](#️-aws-ec2-deployment)
* [🔍 Application Verification](#-application-verification)
* [🛠️ Troubleshooting](#️-troubleshooting)
* [📚 Key Learnings](#-key-learnings)
* [📸 Implementation Screenshots](#-implementation-screenshots)
* [📄 License](#-license)
* [🙏 Acknowledgements](#-acknowledgements)

---

## 📖 Project Overview

This project is based on a **Spring Boot e-commerce application** and was used as a practical DevOps learning project.

The application provides an e-commerce-style structure with components for products, users, authentication, administration, and related application functionality.

From the DevOps perspective, the project focuses on:

* Source code management using GitHub
* Java application build management using Maven
* Continuous Integration using Jenkins
* Jenkins and GitHub integration
* JAR artifact generation
* Linux-based application deployment
* AWS EC2 application hosting

The original repository structure includes `src`, `pom.xml`, Maven Wrapper files, `README.md`, and `LICENSE`.

---

## 🏗️ Architecture & Workflow

The practical CI and deployment workflow used in this project is:

```text
              Developer
                  |
                  v
             GitHub Repository
                  |
                  v
                Jenkins
                  |
                  v
           Source Code Checkout
                  |
                  v
               Maven
                  |
        +---------+---------+
        |         |         |
      Compile    Test     Package
        |         |         |
        +---------+---------+
                  |
                  v
             JAR Artifact
                  |
                  v
              AWS EC2
                  |
                  v
            java -jar
                  |
                  v
        Spring Boot Application
               Port 3000
```

### CI Flow

```text
GitHub
   ↓
Jenkins
   ↓
Checkout Source Code
   ↓
Maven Build
   ↓
Generate JAR
   ↓
Build Result
```

### Deployment Flow

```text
JAR Artifact
    ↓
AWS EC2 Ubuntu
    ↓
java -jar application.jar
    ↓
Application Running
    ↓
Port 3000
```

---

## 🛠️ Technology Stack

| Technology   | Purpose                         |
| ------------ | ------------------------------- |
| Java         | Application development         |
| Spring Boot  | Application framework           |
| Maven        | Build and dependency management |
| Git          | Version control                 |
| GitHub       | Source code management          |
| Jenkins      | Continuous Integration          |
| AWS EC2      | Application hosting             |
| Ubuntu Linux | Server operating system         |

---

## 📋 Prerequisites

Before building and running the application, make sure the required environment is available.

### Required Tools

* Java
* Maven
* Git
* Jenkins
* AWS EC2 instance
* Ubuntu Linux

### Verify Java

```bash
java -version
```

### Verify Maven

```bash
mvn -version
```

### Verify Git

```bash
git --version
```

> Use the Java, Maven, and Ubuntu versions configured in your actual environment.

---

## 🚀 Application Setup

### 1. Clone the Repository

```bash
git clone https://github.com/avneeshagarwal014/javaspringboot-ecommerce.git
```

### 2. Navigate to the Project

```bash
cd javaspringboot-ecommerce
```

### 3. Verify the Project Structure

The project contains the main application source and Maven configuration:

```text
javaspringboot-ecommerce/
│
├── src/
├── pom.xml
├── mvnw
├── mvnw.cmd
├── README.md
└── LICENSE
```

---

## 🔨 Maven Build

Maven is used to manage the Java application's build lifecycle.

### Compile

```bash
mvn compile
```

Compiles the application source code.

### Test

```bash
mvn test
```

Runs the available test cases.

### Package

```bash
mvn package
```

Packages the application and generates the JAR artifact.

### Install

```bash
mvn install
```

Runs the Maven lifecycle through the `install` phase and installs the generated artifact into the local Maven repository.

### Generated Artifact

After a successful build, the generated JAR file is available inside:

```text
target/
```

Example:

```text
target/
└── <application-name>.jar
```

> The exact JAR filename depends on the version and artifact configuration defined in `pom.xml`.

---

## ⚙️ Jenkins CI Pipeline

Jenkins was configured to integrate with the GitHub repository and execute the application build process.

### Jenkins Job

A **Jenkins Freestyle Job** was created for the project.

The job configuration included:

* GitHub repository integration
* Source Code Management using Git
* Source code checkout
* Build execution
* Build status monitoring
* Console output for troubleshooting

### Jenkins Workflow

```text
GitHub Repository
       ↓
Jenkins Job
       ↓
Git Checkout
       ↓
Maven Build
       ↓
Compile / Test / Package
       ↓
JAR Artifact
       ↓
Build Success / Failure
```

### Build Verification

Jenkins Console Output was used to verify:

* Source code checkout
* Workspace execution
* Build commands
* Application output
* Final build status

A successful build ends with:

```text
Finished: SUCCESS
```

---

## ☁️ AWS EC2 Deployment

The application was deployed and tested on an **AWS EC2 instance running Ubuntu Linux**.

### Deployment Steps

#### 1. Provision AWS EC2

Create an EC2 instance with Ubuntu Linux.

#### 2. Connect to the Instance

Connect to the EC2 instance using SSH.

```bash
ssh -i <key-file.pem> ubuntu@<EC2-PUBLIC-IP>
```

#### 3. Verify the Environment

```bash
java -version
mvn -version
```

#### 4. Build the Application

```bash
mvn install
```

#### 5. Locate the JAR

```bash
ls -lh target/
```

#### 6. Run the Application

```bash
java -jar target/<application-name>.jar
```

The Spring Boot application can then be verified on the configured application port.

---

## 🔐 AWS Security Group

If the application is intended to be accessed externally on **Port 3000**, the EC2 Security Group must allow the required inbound traffic.

Example:

```text
Type: Custom TCP
Port: 3000
Source: <your-required-source>
```

> For learning purposes, avoid exposing application ports to `0.0.0.0/0` unless you specifically understand the security implications. Restrict the source where possible.

---

## 🔍 Application Verification

After starting the application, verify that the process is running successfully.

Example:

```bash
ps -ef | grep java
```

Check whether the application is listening on Port 3000:

```bash
sudo ss -lntp | grep 3000
```

The application can then be accessed using:

```text
http://<EC2-PUBLIC-IP>:3000
```

> Do not permanently store your actual EC2 public IP address in this README because the public IP can change when the instance is stopped and started unless an Elastic IP is used.

---

## 🛠️ Troubleshooting

During the implementation, several practical issues were encountered and investigated.

### Maven Installation Issues

Verified Maven installation and environment configuration using:

```bash
mvn -version
```

### Jenkins Workspace Issues

Jenkins workspace paths were checked while troubleshooting build execution and source-code checkout.

### Jenkins Login / Restart Issues

Jenkins login delays were investigated after plugin installation and restart operations.

### Build Troubleshooting

Jenkins Console Output was used to identify build execution details, source-code checkout information, command execution, and final build status.

### Troubleshooting Approach

```text
Identify the Problem
        ↓
Check Logs / Console Output
        ↓
Verify Configuration
        ↓
Test the Environment
        ↓
Apply the Fix
        ↓
Re-run the Build
        ↓
Verify the Result
```

---

## 📚 Key Learnings

Through this hands-on project, I gained practical understanding of:

* Jenkins and GitHub integration
* Jenkins Freestyle Jobs
* Maven build lifecycle
* Java JAR generation
* Jenkins workspace
* Git-based source code checkout
* AWS EC2 application hosting
* Ubuntu Linux server environment
* Application execution using `java -jar`
* Build and console-output analysis
* Practical CI troubleshooting

---

## 📸 Implementation Screenshots

Screenshots demonstrating the hands-on implementation can be added below.

### 1. GitHub Repository

![GitHub Repository](screenshots/github-repository.png)

### 2. Jenkins Job Configuration

![Jenkins Job Configuration](screenshots/jenkins-configuration.png)

### 3. Jenkins Dashboard

![Jenkins Dashboard](screenshots/jenkins-dashboard.png)

### 4. Jenkins Build History

![Jenkins Build History](screenshots/jenkins-build-history.png)

### 5. Jenkins Console Output

![Jenkins Console Output](screenshots/jenkins-console-output.png)

### 6. AWS EC2 Application

![AWS EC2 Application](screenshots/aws-ec2-application.png)

> Add only screenshots that are actually available in the repository. Remove any unused image references.

---

## 📁 Recommended Repository Structure

For better portfolio presentation, the repository can follow this structure:

```text
javaspringboot-ecommerce/
│
├── src/
│
├── screenshots/
│   ├── github-repository.png
│   ├── jenkins-configuration.png
│   ├── jenkins-dashboard.png
│   ├── jenkins-build-history.png
│   ├── jenkins-console-output.png
│   └── aws-ec2-application.png
│
├── pom.xml
├── mvnw
├── mvnw.cmd
├── README.md
└── LICENSE
```

---

## 🎯 Project Outcome

This project helped me connect multiple DevOps concepts into one practical workflow:

```text
GitHub
  ↓
Jenkins
  ↓
Maven
  ↓
Build & Test
  ↓
JAR Artifact
  ↓
AWS EC2
  ↓
Running Application
```

The project strengthened my understanding of **Continuous Integration, Maven-based Java builds, Jenkins automation, Linux server operations, and AWS EC2 deployment**.

---

## 📄 License

This project includes the existing project license. Refer to the [`LICENSE`](LICENSE) file for details.

---

## 🙏 Acknowledgements

This hands-on implementation was completed as part of my **Cloud & DevOps learning journey**.

Special thanks to **Vikas Ratnawat Sir** and the **CloudDevOpsHub Community** for the practical guidance and industry-focused learning sessions.

---

## 👨‍💻 Author

**Avneesh Agarwal**

Cloud & DevOps Learner

GitHub: [@avneeshagarwal014](https://github.com/avneeshagarwal014)

---

⭐ If you find this project useful, feel free to explore the repository and the implementation details.
