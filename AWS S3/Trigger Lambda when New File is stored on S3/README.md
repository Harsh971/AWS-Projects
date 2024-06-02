# Trigger AWS Lambda Function on S3 File Upload

This project demonstrates how to configure an AWS Lambda function to be triggered automatically whenever a new file is uploaded to an S3 bucket. The setup involves configuring an event notification on the S3 bucket to trigger the Lambda function.

<img src="https://github.com/Harsh971/AWS-Projects/blob/main/AWS%20S3/Trigger%20Lambda%20when%20New%20File%20is%20stored%20on%20S3/architecture.png"></img>

## Architecture Overview

1. **S3 Bucket**: Stores the files.
2. **AWS Lambda Function**: The function to be triggered when a new file is uploaded.
3. **S3 Event Notification**: Configured to trigger the Lambda function on file upload events.

## Services Used

1. **AWS Lambda**: Executes the custom logic in response to S3 events.
2. **Amazon S3**: Stores the files and triggers the Lambda function on file upload events.

## Steps to Implement

### 1. Create Lambda Function

1. Navigate to the **Lambda** service in the AWS Management Console.
2. Click on **Create function**.
3. Choose **Author from scratch**.
4. Enter a **Function name** (e.g., `S3FileUploadTriggerFunction`).
5. Choose an appropriate **Runtime** (e.g., Python 3.8).
6. Set the execution role with permissions to access S3. If a suitable role does not exist, create one.
7. Click **Create function**.

### 2. Configure S3 Event Notification

1. Navigate to the **S3** service in the AWS Management Console.
2. Select the bucket where you want to enable the event notification.
3. Click on **Properties**.
4. Scroll down to the **Event notifications** section and click **Create event notification**.
5. Enter a **Name** for the notification.
6. Under **Events**, select **All object create events** or specify specific prefixes/suffixes.
7. Under **Send to**, choose **Lambda function**.
8. Select the Lambda function you created earlier (`S3FileUploadTriggerFunction`).
9. Click **Save**.

## Viewing Invocation Logs in CloudWatch

Once the Lambda function is triggered by an S3 event, you can view the invocation logs in Amazon CloudWatch Logs.

### Steps:

1. Navigate to the **CloudWatch** service in the AWS Management Console.
2. In the left-hand navigation pane, click on **Logs**.
3. Look for the log group associated with your Lambda function.
4. Click on the log group to view the log streams.
5. Select a log stream to view detailed logs of Lambda function invocations.

## Benefits

- **Real-time Processing**: Lambda function is triggered immediately upon file upload events.
- **Scalability**: Serverless architecture automatically scales to handle varying loads.
- **Event-driven Architecture**: Enables decoupling of services and efficient handling of events.
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
