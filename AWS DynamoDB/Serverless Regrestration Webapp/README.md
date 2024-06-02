# Serverless Registration Web Application

This project implements a serverless registration web application using AWS Lambda, API Gateway, DynamoDB, and Python Boto3 in Lambda functions. The registration form, hosted locally, is connected to a DynamoDB table via API Gateway for storing all registration data.

<img src="https://github.com/Harsh971/AWS-Projects/blob/main/AWS%20DynamoDB/Serverless%20Regrestration%20Webapp/architecture.png"></img>

## Services Used

1. **AWS Lambda**: Compute service to execute code in response to HTTP events, handling registration form submissions and database interactions.

2. **Amazon API Gateway**: Fully managed service to create, publish, maintain, monitor, and secure APIs at any scale, acting as a bridge between the registration form and DynamoDB.

3. **Amazon DynamoDB**: NoSQL database service for storing registration data, providing high scalability and performance with low latency.

4. **Python Boto3**: AWS SDK for Python, utilized within Lambda functions to interact with AWS services, particularly DynamoDB for database operations.

## Architecture Overview

1. **Registration Form (index.html)**: The registration form is hosted locally on the user's machine. Upon submission, it sends data to API Gateway endpoints.

2. **Amazon API Gateway**: Serves as the interface between the registration form and AWS Lambda functions. API Gateway receives HTTP requests from the form and triggers Lambda functions.

3. **AWS Lambda Functions**: Handles incoming HTTP requests from API Gateway, processes registration form data, and interacts with DynamoDB using Boto3 to store registration information.

4. **Amazon DynamoDB Table**: Stores registration data received from Lambda functions. The table schema is designed to accommodate registration form fields.

## Flow of Operation

- User fills out the registration form (index.html) with necessary details.
- Upon submission, the form sends an HTTP POST request to the corresponding API Gateway endpoint.
- API Gateway triggers the associated Lambda function.
- Lambda function receives the HTTP request, extracts registration data, and validates it.
- Using Boto3, Lambda function interacts with DynamoDB to insert the registration data into the designated table.
- DynamoDB stores the registration data securely.
- Optionally, Lambda function returns a response to the client indicating the success or failure of the registration process.

## Benefits

- **Scalability**: Serverless architecture scales automatically to handle varying loads.
- **Cost-Effectiveness**: Pay only for the compute time and resources consumed.
- **Low Maintenance**: AWS manages infrastructure, allowing focus on application logic.
- **High Availability**: AWS services are designed for high availability and reliability.

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

