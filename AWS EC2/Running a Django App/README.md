
## Step 1: Set Up an EC2 Instance

1.  Launch an EC2 instance using the AWS Management Console or AWS CLI. Choose an appropriate instance type and Amazon Machine Image (AMI) (e.g., Amazon Linux 2).
    
2.  Configure security groups to allow inbound traffic on ports 80 (HTTP) and 443 (HTTPS), as well as any other ports required by your application.
    
3.  Optionally, assign an Elastic IP (EIP) to your EC2 instance to provide a static IP address.
    
4.  Connect to your EC2 instance via SSH using a terminal or SSH client.
    

## Step 2: Install Python and Django

1.  Update the package manager and install Python and pip:

    
    `sudo yum update -y
    sudo yum install python3 python3-pip -y` 
    
2.  Install Django using pip:

    `pip3 install django` 
    

## Step 3: Configure the Django Application

1.  Copy your Django application files to the EC2 instance using SCP, SFTP, or any other file transfer method.
    
2.  Navigate to the directory containing your Django project and install any 
    
    `pip3 install -r requirements.txt` 
    
3.  Configure the Django settings file (`settings.py`) to use the appropriate database settings, static files, and allowed hosts.
    

## Step 4: Set Up a Web Server

1.  Install and configure a web server to serve your Django application. Nginx and Gunicorn are commonly used together for this purpose.
    
    Install Nginx:
  
    `sudo yum install nginx -y` 
    
    Install Gunicorn
    
    `pip3 install gunicorn` 
    
2.  Create a Gunicorn configuration file for your Django application (e.g., `gunicorn_config.py`):

    
    `bind = '0.0.0.0:8000'
    workers = 3` 
    
3.  Create an Nginx configuration file for your Django application (e.g., `/etc/nginx/conf.d/myapp.conf`):

    
    ```
        server {
        listen 80;
        server_name example.com;
    
        location / {
            proxy_pass http://127.0.0.1:8000;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        }
    }
    ```
    
4.  Start Gunicorn to run your Django application:
    
    
    `gunicorn myapp.wsgi:application -c gunicorn_config.py` 
    
5.  Restart Nginx to apply the new configuration:

    `sudo systemctl restart nginx` 
    

## Step 5: Test the Django Application

Visit your EC2 instance's public IP address or domain name in a web browser to see if your Django application is accessible.

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

