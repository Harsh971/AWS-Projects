
## Running a Flask App on an EC2 Instance

### Step 1: Set Up an EC2 Instance

1.  **Launch an EC2 Instance**: Use the AWS Management Console to launch an EC2 instance. Choose an appropriate AMI, instance type, configure security groups to allow HTTP (port 80) and HTTPS (port 443) traffic, and optionally assign an Elastic IP address.
    
2.  **Connect to the Instance**: Once the instance is running, connect to it via SSH using a terminal or SSH client.
    

### Step 2: Install Dependencies

1.  **Update Packages**: Run the following commands to update the package manager and install essential packages:
    ```
    sudo yum update -y
    sudo yum install python3 python3-pip nginx git -y
    ``` 
    
2.  **Install Flask**: Install Flask and other project dependencies using pip:
    
 
    
    ```sudo pip3 install flask gunicorn``` 
    

### Step 3: Configure Flask Application

1.  **Clone Your Flask App**: Clone your Flask application repository from Git or transfer your project files to the EC2 instance.
    
2.  **Install Requirements**: Navigate to your project directory and install the required Python packages:
 
    
    ```
    pip3 install -r requirements.txt
    ```  
    
4.  **Run Your Flask App**: Start your Flask app using Gunicorn:
    

    
    ```
    gunicorn --bind 0.0.0.0:8000 your_app_name:app
    ``` 
    
    Replace `your_app_name` with the name of your Flask application file and `app` with the name of the Flask application instance.
    

### Step 4: Configure Nginx

1.  **Install and Configure Nginx**: Install Nginx and configure it to act as a reverse proxy to Gunicorn:
    
    -   Create a new Nginx configuration file in ```
      /etc/nginx/sites-available/your_project_name```:
        
 
        
        ```
        server {
            listen 80;
            server_name your_domain.com www.your_domain.com;
        
            location / {
                proxy_pass http://127.0.0.1:8000;
                include proxy_params;
                proxy_redirect off;
            }
        }
        ``` 
        
    -   Enable the configuration by creating a symlink to the `sites-enabled` directory:

        
        ```
        sudo ln -s /etc/nginx/sites-available/your_project_name /etc/nginx/sites-enabled
        ``` 
        
    -   Test the Nginx configuration and restart Nginx:

        
        ```
        sudo nginx -t
        sudo systemctl restart nginx
        ``` 
        

### Step 5: Test Your Flask App

Visit your EC2 instance's public IP address or domain name in a web browser. If everything is configured correctly, you should see your Flask application running.