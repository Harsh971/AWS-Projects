# Simple Lambda and API Gateway Project

This project demonstrates how to create a simple API using AWS Lambda and API Gateway. The API will return some random text, and the output will be displayed in the Lambda function logs.

<img src="https://github.com/Harsh971/AWS-Projects/blob/main/AWS%20APIGateway/Returns%20random%20text%20from%20API%20to%20Lambda/architecture.png"></img>

## Architecture Overview

1. **AWS Lambda**: Executes the function logic to generate random text.
2. **Amazon API Gateway**: Provides the HTTP endpoint for accessing the Lambda function.
3. **CloudWatch Logs**: Displays the output of the Lambda function, including the generated random text.

## Services Used

1. **AWS Lambda**: Runs the function to generate random text.
2. **Amazon API Gateway**: Provides the API endpoint to trigger the Lambda function.
3. **Amazon CloudWatch Logs**: Displays the output logs of the Lambda function.

## Steps to Implement

### 1. Create Lambda Function

1. Navigate to the **Lambda** service in the AWS Management Console.
2. Click on **Create function**.
3. Choose **Author from scratch**.
4. Enter a **Function name** (e.g., `RandomTextFunction`).
5. Choose an appropriate **Runtime** (e.g., Python 3.8).
6. Set the execution role with permissions to write logs to CloudWatch.
7. Click **Create function**.

### Lambda Function Code

```python
import json
import random

def lambda_handler(event, context):
    random_text = "Random text: " + ''.join(random.choices('abcdefghijklmnopqrstuvwxyz', k=10))
    print(random_text)  # Output will be displayed in CloudWatch Logs
    return {
        'statusCode': 200,
        'body': json.dumps(random_text)
    }
```

### 2. Create API Gateway

1. Navigate to the **API Gateway** service in the AWS Management Console.
2. Click on **Create API**.
3. Choose the **REST API** option and click **Build**.
4. Enter an **API name** and description.
5. Click **Create API**.

### 3. Create Resource and Method

1. In the API Gateway console, select your API.
2. Click on **Resources**.
3. Click on **Actions** and select **Create Resource**.
4. Enter a **Resource Name** (e.g., `random`) and **Resource Path** (e.g., `/random`).
5. Click **Create Resource**.
6. With the resource selected, click **Actions** and choose **Create Method**.
7. Select **GET** and click the checkmark.
8. Choose **Lambda Function** as the integration type.
9. Select the region and enter the name of your Lambda function (`RandomTextFunction`).
10. Click **Save** and confirm the dialog.

### 4. Deploy API

1. In the API Gateway console, select your API.
2. Click on **Actions** and choose **Deploy API**.
3. Create a new stage by entering a **Stage Name** (e.g., `prod`).
4. Click **Deploy**.
5. Note the **Invoke URL** displayed after deployment.

### 5. Invoke the API

Use a tool like `curl`, Postman, or a web browser to send a request to the invoke URL.

#### Example using `curl`:

```sh
curl -X GET "https://your-invoke-url/random"
```

## Example using Postman:

1. Open Postman.
2. Enter the invoke URL with the resource path.
3. Select the **GET** method.
4. Click **Send**.

### Viewing Output in CloudWatch Logs

1. Navigate to the **CloudWatch** service in the AWS Management Console.
2. In the left-hand navigation pane, click on **Logs**.
3. Look for the log group associated with your Lambda function.
4. Click on the log group to view the log streams.
5. Select a log stream to view the output of the Lambda function, including the generated random text.

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
