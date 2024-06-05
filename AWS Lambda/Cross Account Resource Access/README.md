# AWS Cross-Account Lambda to S3 Project

## Project Overview

This project demonstrates how to set up a Lambda function in one AWS account (Account 1) that writes its output to an S3 bucket in another AWS account (Account 2). This involves configuring the Lambda function, setting up the S3 bucket, and establishing the necessary cross-account permissions using bucket policies.


<img src="https://github.com/Harsh971/AWS-Projects/blob/main/AWS%20Lambda/Cross%20Account%20Resource%20Access/architecture.png"></img>


## Architecture Design

### AWS Components

1. **Account 1**:
   - AWS Lambda: A function that generates some output and writes it to an S3 bucket.
   
2. **Account 2**:
   - Amazon S3: A bucket that receives the output from the Lambda function in Account 1.

## Steps for Implementation

### Step 1: Set Up the S3 Bucket in Account 2

1. **Create an S3 Bucket**:
   - Navigate to the S3 service in the AWS Management Console.
   - Create a new bucket (e.g., `account2-bucket`).
   - Configure the bucket as needed and create it.

2. **Configure Bucket Policy**:
   - Go to the permissions tab of the bucket.
   - Add a bucket policy to allow the Lambda function from Account 1 to put objects into the bucket. The bucket policy might look like this:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::<Account1_ID>:role/<LambdaExecutionRole>"
      },
      "Action": "s3:PutObject",
      "Resource": "arn:aws:s3:::account2-bucket/*"
    }
  ]
}
```

Replace `<Account1_ID>` with the AWS account ID of Account 1 and `<LambdaExecutionRole>` with the name of the IAM role used by the Lambda function.

### Step 2: Set Up the Lambda Function in Account 1

1. **Create the Lambda Function**:
   - Navigate to the Lambda service in the AWS Management Console.
   - Create a new Lambda function (e.g., `CrossAccountLambda`).
   - Choose the runtime (e.g., Python, Node.js) and configure the function.

2. **Add Permissions to the Lambda Execution Role**:
   - Attach a policy to the Lambda execution role to allow it to put objects in the S3 bucket in Account 2. The policy might look like this:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:PutObject",
      "Resource": "arn:aws:s3:::account2-bucket/*"
    }
  ]
}
```

3. **Write Lambda Function Code**:
   - Add code to the Lambda function that generates output and writes it to the S3 bucket in Account 2. An example in Python:

```python
import boto3
import json
import os

def lambda_handler(event, context):
    s3_client = boto3.client('s3')
    
    # Generate output (e.g., a simple text message)
    output_text = "Hello from Account 1 Lambda"
    
    # Define the S3 bucket and the file name
    bucket_name = "account2-bucket"
    file_name = "output.txt"
    
    # Upload the file to the S3 bucket
    s3_client.put_object(
        Bucket=bucket_name,
        Key=file_name,
        Body=output_text
    )
    
    return {
        'statusCode': 200,
        'body': json.dumps('Output successfully stored in Account 2 S3 bucket')
    }
```

### Step 3: Testing and Validation

1. **Test the Lambda Function**:
   - Navigate to the Lambda function in the AWS Management Console.
   - Create a test event and invoke the function.
   - Check the execution result to ensure the function runs successfully.

2. **Verify the S3 Bucket in Account 2**:
   - Navigate to the S3 bucket in Account 2.
   - Verify that the `output.txt` file has been created and contains the expected content.

## Security Considerations

- Ensure the bucket policy in Account 2 grants the minimum necessary permissions.
- Use IAM roles and policies to manage permissions securely and follow the principle of least privilege.
- Regularly review and update policies to address any security concerns.
