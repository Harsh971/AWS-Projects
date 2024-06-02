# Upload and Download Files Using Presigned URL

This project demonstrates how to upload and download files from S3 using presigned URLs. The process involves an API Gateway, a Lambda function to generate presigned URLs, and direct interactions between the user and S3.

## Architecture Overview

1. **User**: Initiates a request to the API Gateway.
2. **API Gateway**: Forwards the request to the Lambda function.
3. **Lambda Function**: Requests a presigned URL from S3.
4. **S3**: Returns the presigned URL to the Lambda function.
5. **Lambda Function**: Forwards the presigned URL to API Gateway.
6. **API Gateway**: Shares the presigned URL with the user.
7. **User**: Uses the presigned URL to directly upload or download files from S3.

<img src="https://github.com/Harsh971/AWS-Projects/blob/main/AWS%20S3/Upload%20and%20Download%20Files%20using%20Presigned%20URL/architecture.png"></img>

## Services Used

1. **AWS Lambda**: Generates presigned URLs for S3 operations.
2. **Amazon API Gateway**: Provides the API endpoints.
3. **Amazon S3**: Stores the files.
4. **Python Boto3**: AWS SDK for Python, used in the Lambda function to interact with S3.

## Steps to Implement

### 1. Set Up S3 Bucket

1. Log in to the [AWS Management Console](https://aws.amazon.com/console/).
2. Navigate to the **S3** service.
3. Create a new bucket or use an existing bucket to store your files.

### 2. Create the Lambda Function

1. Navigate to the **Lambda** service in the AWS Management Console.
2. Click on **Create function**.
3. Choose **Author from scratch**.
4. Enter a **Function name** (e.g., `GeneratePresignedURLFunction`).
5. Choose an appropriate **Runtime** (e.g., Python 3.8).
6. Set the execution role with permissions to access S3. If a suitable role does not exist, create one.
7. Click **Create function**.

### Lambda Function Code

```python
import json
import boto3

def lambda_handler(event, context):
    s3 = boto3.client('s3')
    bucket_name = 'your-bucket-name'
    operation = event['queryStringParameters']['operation']
    file_key = event['queryStringParameters']['fileKey']
    
    if operation == 'upload':
        url = s3.generate_presigned_url('put_object', Params={'Bucket': bucket_name, 'Key': file_key}, ExpiresIn=3600)
    elif operation == 'download':
        url = s3.generate_presigned_url('get_object', Params={'Bucket': bucket_name, 'Key': file_key}, ExpiresIn=3600)
    else:
        return {
            'statusCode': 400,
            'body': json.dumps('Invalid operation')
        }
    
    return {
        'statusCode': 200,
        'body': json.dumps({'url': url})
    }
```

## 3. Create API Gateway

### Steps:

1. Navigate to the **API Gateway** service in the AWS Management Console.
2. Click on **Create API**.
3. Choose the **REST API** option and click **Build**.
4. Enter an **API name** and description.
5. Click **Create API**.

## 4. Create Resource and Method

### Steps:

1. In the API Gateway console, select your API.
2. Click on **Resources**.
3. Click on **Actions** and select **Create Resource**.
4. Enter a **Resource Name** (e.g., `presigned-url`) and **Resource Path** (e.g., `/presigned-url`).
5. Click **Create Resource**.
6. With the resource selected, click **Actions** and choose **Create Method**.
7. Select **GET** and click the checkmark.
8. Choose **Lambda Function** as the integration type.
9. Select the region and enter the name of your Lambda function (`GeneratePresignedURLFunction`).
10. Click **Save** and confirm the dialog.

## 5. Deploy API

### Steps:

1. In the API Gateway console, select your API.
2. Click on **Actions** and choose **Deploy API**.
3. Create a new stage by entering a **Stage Name** (e.g., `prod`).
4. Click **Deploy**.
5. Note the **Invoke URL** displayed after deployment.

## 6. Invoke the API

Use a tool like `curl`, Postman, or a web browser to send a request to the invoke URL.

### Example using `curl`:

```sh
curl -X GET "https://your-invoke-url/presigned-url?operation=upload&fileKey=your-file-key"
```

### Example using Postman:

1. Open Postman.
2. Enter the invoke URL with the resource path and query parameters.
3. Select the **GET** method.
4. Click **Send**.

## Viewing API Responses in CloudWatch

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

- **Scalability**: Serverless architecture scales automatically to handle varying loads.
- **Security**: Supports authentication and authorization mechanisms such as AWS IAM, Cognito, and API keys.
- **Monitoring and Logging**: Integrated with CloudWatch for monitoring and logging API requests and responses.
- **Cost-Effectiveness**: Pay only for the compute time and resources consumed.

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
