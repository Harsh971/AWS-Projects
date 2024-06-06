# AWS Lambda Function Triggered by HTML Button Click

<img src="https://github.com/Harsh971/AWS-Projects/blob/main/AWS%20APIGateway/Lambda%20Trigger%20through%20HTML/architecture.png"></img>

## Project Overview

This project demonstrates how to trigger an AWS Lambda function via an HTML button click. When the button is clicked, the Lambda function returns the current time, which is then displayed in the logs and below the button on the HTML page.

## Architecture Design

### AWS Components

1. **AWS Lambda**:
   - A function that returns the current time when triggered.

2. **Amazon API Gateway**:
   - Exposes the Lambda function as an HTTP endpoint that can be invoked from the HTML page.

3. **HTML Page**:
   - Contains a button that, when clicked, triggers the Lambda function and displays the current time.

## Steps for Implementation

### Step 1: Create the Lambda Function

1. **Navigate to the Lambda Console**:
   - Go to the AWS Management Console and open the Lambda service.

2. **Create a New Lambda Function**:
   - Click "Create function".
   - Choose "Author from scratch".
   - Function name: `GetCurrentTime`.
   - Runtime: Choose your preferred runtime (e.g., Python 3.8).

3. **Add Lambda Function Code**:
   - Use the following Python code for the Lambda function:

```python
import json
from datetime import datetime

def lambda_handler(event, context):
    current_time = datetime.utcnow().isoformat()
    
    # Log the current time
    print(f"Current time: {current_time}")
    
    return {
        'statusCode': 200,
        'body': json.dumps({'currentTime': current_time})
    }
```

4. **Create an IAM Role for Lambda**:
   - Create a new IAM role with basic Lambda execution permissions.
   - Attach the role to the Lambda function.

### Step 2: Set Up API Gateway

1. **Navigate to the API Gateway Console**:
   - Go to the AWS Management Console and open the API Gateway service.

2. **Create a New API**:
   - Choose "Create API".
   - Select "HTTP API" for simplicity.
   - Click "Build".

3. **Configure API Settings**:
   - Name the API (e.g., `LambdaTriggerAPI`).
   - Add an integration with the Lambda function created earlier:
     - Integration type: Lambda
     - Lambda function: `GetCurrentTime`

4. **Create Routes and Deploy API**:
   - Create a route that triggers the Lambda function (e.g., POST method on `/getTime`).
   - Deploy the API and note the endpoint URL.

### Step 3: Create the HTML Page

1. **Write the HTML Code**:
   - Create an HTML file (e.g., `index.html`) with a button that triggers the Lambda function via the API Gateway endpoint.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lambda Trigger</title>
    <script>
        async function getCurrentTime() {
            try {
                const response = await fetch('https://<API_GATEWAY_ID>.execute-api.<REGION>.amazonaws.com/getTime', {
                    method: 'POST'
                });
                const data = await response.json();
                document.getElementById('output').innerText = `Current Time: ${data.currentTime}`;
            } catch (error) {
                console.error('Error fetching current time:', error);
            }
        }
    </script>
</head>
<body>
    <h1>Get Current Time</h1>
    <button onclick="getCurrentTime()">Get Time</button>
    <p id="output"></p>
</body>
</html>
```

   - Replace `<API_GATEWAY_ID>` and `<REGION>` with your actual API Gateway ID and AWS region.

2. **Host the HTML Page**:
   - You can host the HTML page on any web server or service (e.g., Amazon S3 static website hosting, local server).

### Step 4: Testing and Validation

1. **Open the HTML Page**:
   - Open the HTML page in a web browser.

2. **Click the Button**:
   - Click the "Get Time" button.
   - Check that the current time is displayed below the button.

3. **Verify Logs**:
   - Navigate to the AWS Lambda console and check the logs to ensure the current time is being logged correctly.

