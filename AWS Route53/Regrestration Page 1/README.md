# AWS Project: Registration Form Application

<img src="https://github.com/Harsh971/AWS-Projects/blob/main/AWS%20Route53/Regrestration%20Page%201/architecture.png"></img>

## Project Overview
This project involves creating a registration form application using multiple AWS services: Route 53, EC2, S3, and RDS (SQL). The application is a Python script that hosts a web-based registration form where users can fill in their details and upload a PDF file. The text data from the form is stored in an RDS database, and the uploaded PDF files are stored in an S3 bucket.

## Architecture Design
### AWS Services Used
Route 53:

- Domain registration and DNS routing for the application.
- Provides a user-friendly URL to access the registration form.

EC2:

- Hosts the Python web application that serves the registration form.
- Configured with necessary security groups to allow HTTP and SSH access.

S3:

- Stores the uploaded PDF files securely.
- Configured with appropriate bucket policies to manage access.

RDS (SQL):

- Stores user registration details in a relational database.
- Configured with appropriate security settings and database schema.

## Application Workflow
User Interaction:

- Users access the registration form through a URL provided by Route 53.
- Users fill in their details (e.g., name, email) and upload a PDF file.

Data Handling:

- The Python script processes the form data.
- Text data is inserted into the RDS database.
- The uploaded PDF is stored in the S3 bucket.

## System Components
Python Web Application:

- Uses a web framework (e.g., Flask or Django) to create the registration form.
- Handles form submissions and integrates with AWS services.

RDS Database:

- Schema includes a table for user details with columns for name, email, and other relevant fields.
- Stores metadata about the uploaded PDF files (e.g., file name, S3 URL).

S3 Bucket:

- Stores the uploaded PDF files.
- Organized with folders or prefixes based on user IDs or other criteria.

Route 53 Configuration:

- Manages DNS settings to route traffic to the EC2 instance hosting the application.

## Steps for Implementation
Set Up Route 53:

- Register a domain or use an existing domain.
- Configure DNS settings to route traffic to the EC2 instance.

Launch EC2 Instance:

- Launch an EC2 instance using an appropriate AMI (e.g., Amazon Linux 2).
- Configure security groups to allow HTTP (port 80) and SSH (port 22) access.
- SSH into the instance to set up the Python web application.

Configure S3 Bucket:

- Create an S3 bucket to store PDF files.
- Set bucket policies and permissions to manage access.

Set Up RDS Database:

- Launch an RDS instance with a SQL database (e.g., MySQL, PostgreSQL).
- Configure the database schema to store user details and PDF metadata.

Develop the Python Application:

- Create a web application using Flask or Django.
- Implement a registration form for user input.
- Write logic to handle form submissions, store text data in RDS, and upload PDF files to S3.

Example Flask app structure:
```
from flask import Flask, request, redirect, url_for
import boto3
import pymysql

app = Flask(__name__)

# S3 and RDS configuration
S3_BUCKET = 'your-s3-bucket'
RDS_HOST = 'your-rds-endpoint'
RDS_USER = 'your-db-username'
RDS_PASSWORD = 'your-db-password'
RDS_DB = 'your-db-name'

s3_client = boto3.client('s3')
db_conn = pymysql.connect(host=RDS_HOST, user=RDS_USER, password=RDS_PASSWORD, db=RDS_DB)

@app.route('/', methods=['GET', 'POST'])
def register():
    if request.method == 'POST':
        name = request.form['name']
        email = request.form['email']
        pdf = request.files['pdf']

        # Upload PDF to S3
        s3_client.upload_fileobj(pdf, S3_BUCKET, pdf.filename)

        # Store user details and PDF metadata in RDS
        with db_conn.cursor() as cursor:
            sql = "INSERT INTO registrations (name, email, pdf_url) VALUES (%s, %s, %s)"
            cursor.execute(sql, (name, email, f'https://{S3_BUCKET}.s3.amazonaws.com/{pdf.filename}'))
            db_conn.commit()

        return redirect(url_for('register'))

    return '''
        <form method="post" enctype="multipart/form-data">
            Name: <input type="text" name="name"><br>
            Email: <input type="text" name="email"><br>
            PDF: <input type="file" name="pdf"><br>
            <input type="submit" value="Register">
        </form>
    '''

if __name__ == '__main__':
    app.run(host='0.0.0.0')
```

Deploy and Test:

- Deploy the application on the EC2 instance.
- Access the application through the Route 53 URL.
- Test the registration form by submitting data and verifying entries in RDS and S3.