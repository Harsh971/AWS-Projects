# AWS API Gateway Project

This project demonstrates the process of creating, deploying, and invoking an API using AWS API Gateway. It includes the steps to create API endpoints, define resources and methods, and deploy the API for invocation.

## Project Steps

1. **Create API Endpoint**
2. **Create Resources and Methods**
3. **Deploy and Invoke API**

## 1. Create API Endpoint

### Steps:
1. Log in to the [AWS Management Console](https://aws.amazon.com/console/).
2. Navigate to the **API Gateway** service.
3. Click on **Create API**.
4. Choose the API type (e.g., REST API) and click **Build**.
5. Enter an **API Name** and a **Description**.
6. Click **Create API**.

## 2. Create Resources and Methods

### Steps:
1. In the API Gateway console, select the newly created API.
2. Click on **Resources**.
3. Click on **Actions** and select **Create Resource**.
4. Enter a **Resource Name** and a **Resource Path**.
5. Click **Create Resource**.
6. With the resource selected, click **Actions** and choose **Create Method**.
7. Select the HTTP method (e.g., GET, POST) and click the checkmark.
8. Configure the method settings, such as integration type (e.g., Lambda Function, HTTP), and enter necessary details.
9. Click **Save** and confirm the settings.

## 3. Deploy and Invoke API

### Steps:
1. In the API Gateway console, select the API.
2. Click on **Actions** and choose **Deploy API**.
3. Create a new stage by entering a **Stage Name** (e.g., `dev`, `prod`).
4. Click **Deploy**.
5. Note the **Invoke URL** displayed after deployment.

### Invoking the API:
- Use a tool like `curl`, Postman, or a web browser to send a request to the invoke URL.
- Example using `curl`:
  ```sh
  curl -X GET https://your-invoke-url/resource-path

### Example using Postman:
- Open Postman.
- Enter the invoke URL with the resource path.
- Select the appropriate HTTP method.
- Click Send.

## 4. View API Responses in AWS CloudWatch

### Steps:

1. Navigate to the **CloudWatch** service in the AWS Management Console.
2. In the left-hand navigation pane, click on **Logs**.
3. Look for the log group associated with your API Gateway. It will typically follow the pattern `API-Gateway-Execution-Logs_{rest-api-id}/{stage-name}`.
4. Click on the log group to view the log streams.
5. Select a log stream to view detailed logs of API requests and responses.

### Log Details:

- **Request Details**: Includes HTTP method, resource path, query parameters, and request headers.
- **Response Details**: Includes status code, response headers, and response body.
- **Execution Information**: Includes latency, integration latency, and request IDs.

## Benefits

- **Scalability**: API Gateway scales automatically to handle varying traffic loads.
- **Security**: Supports authentication and authorization mechanisms such as AWS IAM, Cognito, and API keys.
- **Monitoring and Logging**: Integrated with CloudWatch for monitoring and logging API requests and responses.
- **Cost-Effectiveness**: Pay only for the API requests you receive.

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
