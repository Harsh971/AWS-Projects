# Hosting a Static Website on an EC2 Instance

Hosting a static website on an EC2 instance involves setting up a web server software like Apache HTTP Server or Nginx, configuring it to serve static files, uploading your website files to the server, and making your website accessible via a public IP address or domain name.

## Step 1: Set Up an EC2 Instance

1. Launch an EC2 instance using the AWS Management Console or AWS CLI. Choose an Amazon Machine Image (AMI) based on your preference (e.g., Amazon Linux, Ubuntu, etc.), and select an appropriate instance type (e.g., t2.micro for low traffic websites).

2. Configure security groups to allow inbound traffic on port 80 (HTTP) and port 443 (HTTPS if needed). This allows HTTP requests to reach your web server.

3. Optionally, assign an Elastic IP (EIP) to your EC2 instance to provide a static IP address that doesn't change every time the instance is stopped or started.

4. Connect to your EC2 instance via SSH using a terminal or SSH client.

## Step 2: Install and Configure Web Server Software

For this example, let's install Apache HTTP Server on an Amazon Linux EC2 instance:

```bash
sudo yum update -y
sudo yum install httpd -y
sudo service httpd start
sudo chkconfig httpd on
```

This installs Apache HTTP Server and starts the service. The `chkconfig` command ensures that Apache starts automatically on system boot.

## Step 3: Upload Static Website Files

1. Create a directory to store your website files. By default, Apache serves files from `/var/www/html`.

2. Upload your website files to the server using SCP, SFTP, or any other file transfer method. You can use tools like FileZilla or WinSCP for graphical file transfer.

For example, to upload a file named `index.html` to the server:

```bash
scp -i your-key.pem index.html ec2-user@your-ec2-instance-ip:/var/www/html/
```

## Step 4: Test the Website

Visit your EC2 instance's public IP address in a web browser to see if your website is accessible. If you've set up a domain name, you can use that instead.

For example, if your EC2 instance's public IP address is `1.2.3.4`, you can enter `http://1.2.3.4` into your web browser's address bar.

## Benefits

- **Flexibility**: You have full control over the server environment and can customize it to your needs.
- **Cost-Effectiveness**: You pay only for the resources you use, making it a cost-effective option for small websites.
- **Scalability**: EC2 instances can scale horizontally and vertically to accommodate changes in traffic.

## Feedback

Your feedback is valuable! If you have suggestions for improving existing content or ideas for new additions, please open an issue or reach out to the repository maintainers. If you have any other feedbacks, you can reach out to us at harsh.thakkar0369@gmail.com


## Connect with Me
<p>

 <a href="https://twitter.com/HarshThakkar971" target="blank"><img align="center" src="https://img.freepik.com/premium-vector/vector-new-twitter-x-white-logo-black-background_744381-866.jpg" alt="HarshThakkar971" height="40" width="50" /></a>
  &nbsp;&nbsp;
  	<a href="https://linkedin.com/in/harsh-thakkar-7764bb1a4" target="blank"><img align="center" src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/ca/LinkedIn_logo_initials.png/800px-LinkedIn_logo_initials.png" alt="harsh-thakkar-7764bb1a4" height="40" width="40" /></a>
  &nbsp;&nbsp;
 <a href="https://instagram.com/harsh_thakkar09" target="blank"><img align="center" src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/e7/Instagram_logo_2016.svg/768px-Instagram_logo_2016.svg.png" alt="harsh_thakkar09" height="40" width="40" /></a>
</p>


