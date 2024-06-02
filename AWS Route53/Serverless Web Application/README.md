# Serverless Web Application

This project aims to create a simple serverless web application using various AWS services to track and display page visit counts upon page refresh.

<img src="https://github.com/Harsh971/AWS-Projects/blob/main/AWS%20Route53/Serverless%20Web%20Application/architecture.png"></img>

## Architecture Overview

The architecture of the serverless web application involves the following AWS services:

1. **AWS Lambda**: Compute service to handle HTTP requests, update page visit counts, and return updated counts.

2. **Amazon DynamoDB**: Fully managed NoSQL database service to store and manage page visit count data.

3. **Amazon CloudFront**: Content delivery network (CDN) service to cache static content globally, improving performance.

4. **Amazon Route 53**: Scalable DNS web service to route user requests to CloudFront distributions.

5. **Amazon S3**: Object storage service to host static web content like HTML, CSS, and JavaScript files.

## Architecture Flow

- User accesses the web application via URL, and Route 53 routes the request to the nearest CloudFront edge location.
- CloudFront checks cache for requested static content; if cached, delivers directly to user; if not, forwards request to Lambda.
- Lambda retrieves current page visit count from DynamoDB, increments it, updates the count in the database, and returns it to CloudFront.
- CloudFront delivers the updated count to the user's browser and caches dynamic content for subsequent requests.
- Process repeats for each user request, ensuring real-time tracking and display of page visit counts.

## Benefits

- **Scalability**: Leveraging serverless computing and managed services for scalability.
- **Low Latency**: CloudFront CDN reduces latency by caching content globally.
- **Cost-Effectiveness**: Pay only for the resources used, with no upfront costs or long-term commitments.

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
