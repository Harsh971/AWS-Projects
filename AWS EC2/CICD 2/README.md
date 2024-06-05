# AWS CI/CD Pipeline Project

## Project Overview

This project demonstrates the creation of a Continuous Integration and Continuous Deployment (CI/CD) pipeline using AWS CodePipeline and CodeDeploy. The pipeline takes code from a GitHub repository, which contains a simple HTML webpage, and deploys it to an EC2 instance, automating the build and deployment process.

<img src="https://github.com/Harsh971/AWS-Projects/blob/main/AWS%20EC2/CICD%202/architecture.png"></img>

## Architecture Design

### AWS Components

1. **AWS CodePipeline**:
   - A fully managed continuous delivery service that automates the release process.
   - Connects to the GitHub repository to fetch the latest code changes.

2. **AWS CodeDeploy**:
   - A deployment service that automates application deployments to various compute services, including EC2.
   - Ensures smooth, reliable updates with minimal downtime.

3. **EC2 Instance**:
   - Hosts the deployed HTML webpage.
   - Configured to work with CodeDeploy to receive updates from the pipeline.

### GitHub Repository

- Contains the HTML webpage code.
- Includes an `appspec.yml` file to define deployment instructions for CodeDeploy.

## Steps for Implementation

### Step 1: Set Up the EC2 Instance

1. Launch an EC2 instance:
   - Choose an appropriate Amazon Machine Image (AMI) (e.g., Amazon Linux 2).
   - Select an instance type (e.g., t2.micro for free tier).
   - Configure instance details, storage, and add tags as needed.
   - Configure the security group to allow HTTP (port 80) and SSH (port 22) access.
   - Launch the instance and connect to it using SSH.

2. Install necessary software:
   ```sh
   sudo yum update -y
   sudo yum install -y httpd
   sudo systemctl start httpd
   sudo systemctl enable httpd
   ```

3. Install the CodeDeploy agent:
   ```sh
   sudo yum install -y ruby
   cd /home/ec2-user
   wget https://aws-codedeploy-us-east-1.s3.us-east-1.amazonaws.com/latest/install
   chmod +x ./install
   sudo ./install auto
   sudo service codedeploy-agent start
   ```

### Step 2: Create the `appspec.yml` File

Create an `appspec.yml` file in the root of your GitHub repository. This file defines the deployment instructions for CodeDeploy.

```yaml
version: 0.0
os: linux
files:
  - source: /index.html
    destination: /var/www/html/
hooks:
  BeforeInstall:
    - location: scripts/install_dependencies.sh
      timeout: 300
      runas: root
  AfterInstall:
    - location: scripts/start_server.sh
      timeout: 300
      runas: root
```

### Step 3: Create Deployment Scripts

Create the following deployment scripts in a `scripts` directory in your GitHub repository.

#### `install_dependencies.sh`

```sh
#!/bin/bash
sudo yum install -y httpd
sudo systemctl start httpd
sudo systemctl enable httpd
```

#### `start_server.sh`

```sh
#!/bin/bash
sudo systemctl restart httpd
```

### Step 4: Set Up AWS CodePipeline

1. **Create a New Pipeline**:
   - Navigate to the AWS CodePipeline console and create a new pipeline.
   - Name your pipeline and create a new service role.
   - Select "GitHub" as the source provider and connect to your GitHub repository.

2. **Add Build Stage**:
   - Skip the build stage if the application doesn't need to be built. Otherwise, add a build stage using AWS CodeBuild.

3. **Add Deploy Stage**:
   - Select "AWS CodeDeploy" as the deploy provider.
   - Choose the application name and deployment group previously created in CodeDeploy.

### Step 5: Set Up AWS CodeDeploy

1. **Create a New Application**:
   - Navigate to the AWS CodeDeploy console and create a new application.
   - Name your application and choose "EC2/On-premises" as the compute platform.

2. **Create a Deployment Group**:
   - Name the deployment group.
   - Select the service role that allows CodeDeploy to interact with your EC2 instances.
   - Choose the EC2 instances by tags or manually.

### Step 6: Verify the Deployment

1. Push your code to the GitHub repository.
2. Trigger the pipeline in AWS CodePipeline.
3. Monitor the pipeline stages and check for any errors.
4. Once the deployment is complete, access the public IP address of the EC2 instance in a web browser to see the HTML webpage.

