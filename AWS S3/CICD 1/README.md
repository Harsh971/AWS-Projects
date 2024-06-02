# AWS CI/CD Pipeline Setup

This project demonstrates the setup of a full CI/CD pipeline using AWS DevOps services, including AWS CodeCommit, AWS CodeBuild, AWS CodeDeploy, and AWS CodePipeline. The pipeline facilitates automatic deployment of changes to an EC2 instance.

<img src="https://github.com/Harsh971/AWS-Projects/blob/main/AWS%20S3/CICD%201/architecture.png"></img>

## Services Used

- **Authorization**: IAM (Identity and Access Management)
- **Storage**: S3 (Simple Storage Service)
- **Compute**: EC2 (Elastic Compute Cloud)
- **CI/CD**: AWS CodeCommit, AWS CodeBuild, AWS CodeDeploy, AWS CodePipeline

## Workflow

1. **User Authentication**: User accesses AWS services through IAM.
2. **Code Management**: Code files are stored in CodeCommit.
3. **Build Process**: CodeCommit triggers CodeBuild, which builds the application.
4. **Artifact Storage**: Build artifacts are stored in S3.
5. **Deployment**: CodeDeploy deploys the artifacts to the EC2 instance.

## Steps to Implement

### 1. Setup IAM

Ensure appropriate IAM roles and permissions are set up for accessing and managing AWS services.

### 2. Configure CodeCommit

1. Create a CodeCommit repository to store your code files.
2. Clone the repository to your local machine.
3. Push your code changes to the CodeCommit repository.

### 3. Configure CodeBuild

1. Create a CodeBuild project to build your application.
2. Configure build settings and specify the source location (CodeCommit repository).
3. Define build specifications in the `buildspec.yml` file.
4. Trigger CodeBuild automatically on code changes in CodeCommit.

### 4. Configure S3

1. Create an S3 bucket to store build artifacts.
2. Configure CodeBuild to upload build artifacts to the S3 bucket.

### 5. Configure CodeDeploy

1. Set up CodeDeploy to deploy your application to EC2 instances.
2. Create an application and deployment group in CodeDeploy.
3. Configure deployment settings and specify the S3 bucket and build artifacts.

### 6. Configure CodePipeline

1. Create a CodePipeline pipeline to orchestrate the CI/CD workflow.
2. Define pipeline stages and actions:
   - Source: CodeCommit
   - Build: CodeBuild
   - Deploy: CodeDeploy
3. Configure triggers to automatically start the pipeline on code changes.

## Benefits

- **Automation**: Automatic deployment of code changes without manual intervention.
- **Scalability**: Easily scale the pipeline to handle various application and deployment scenarios.
- **Reliability**: Ensures consistency and reliability in the deployment process.
- **Visibility**: Provides visibility into the entire CI/CD workflow through CodePipeline.


## Reference Source : 

TrainWithShubham : Part 1 : <a href="https://www.youtube.com/watch?v=p5i3cMCQ760&list=PLlfy9GnSVerTB0twnC5eaGD-oiHprpnW-">Click Here</a>
<br>
TrainWithShubham : Part 2 : <a href="https://youtu.be/IUF-pfbYGvg?si=lZtsHtLbD6o49Y99">Click Here</a>

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
