# Hosting a Node.js App on AWS EC2

## Project Overview

This project involves hosting a sample Node.js application on an AWS EC2 instance. The Node.js code is stored in a GitHub repository, and the EC2 instance is used to deploy and run the application, making it accessible over the internet.

## Architecture Design

### AWS Components

1. **EC2 Instance**:
   - An Amazon EC2 instance is provisioned to host the Node.js application.
   - The instance is configured with the necessary security groups and network settings to allow web traffic.

2. **Security Group**:
   - A security group is created and associated with the EC2 instance to control inbound and outbound traffic.
   - The security group is configured to allow HTTP (port 80) and SSH (port 22) access.

### Node.js Application

1. **GitHub Repository**:
   - The Node.js application code is stored in a GitHub repository.
   - The repository contains all the necessary files, including `package.json` and the main application file (e.g., `app.js`).

## Steps for Implementation

1. **Provision EC2 Instance**:
   - Launch an EC2 instance using the AWS Management Console.
   - Choose an appropriate Amazon Machine Image (AMI) (e.g., Amazon Linux 2).
   - Select an instance type (e.g., t2.micro for free tier).
   - Configure the instance details, storage, and add tags as needed.
   - Configure the security group to allow HTTP (port 80) and SSH (port 22) access.
   - Launch the instance and connect to it using SSH.

2. **Install Node.js and Git**:
   - Update the package lists:
     ```sh
     sudo yum update -y
     ```
   - Install Node.js and npm:
     ```sh
     curl -sL https://rpm.nodesource.com/setup_14.x | sudo -E bash -
     sudo yum install -y nodejs
     ```
   - Install Git:
     ```sh
     sudo yum install -y git
     ```

3. **Clone the GitHub Repository**:
   - Navigate to the desired directory and clone the repository:
     ```sh
     git clone https://github.com/yourusername/your-repo.git
     ```
   - Change to the application directory:
     ```sh
     cd your-repo
     ```

4. **Install Application Dependencies**:
   - Install the dependencies specified in `package.json`:
     ```sh
     npm install
     ```

5. **Run the Node.js Application**:
   - Start the Node.js application:
     ```sh
     node app.js
     ```
   - Optionally, use a process manager like PM2 to manage the application:
     ```sh
     sudo npm install -g pm2
     pm2 start app.js
     ```

6. **Access the Application**:
   - Retrieve the public IP address of the EC2 instance from the AWS Management Console.
   - Open a web browser and navigate to `http://<EC2_PUBLIC_IP>` to see the running Node.js application.

