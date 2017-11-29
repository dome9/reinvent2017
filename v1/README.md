# DevSecOps in the CI/CD pipeline

This is a stripped down, cleand-up version of the nice work described at:
https://aws.amazon.com/blogs/devops/implementing-devsecops-using-aws-codepipeline/
It provides a full code pipline with DevSecOps approach unsing native AWS technologies:
- CFT static checks via Lambda, DynamoDB and regex
- Provisioning of ephemeral test env + live tests via Lambda and AWS SDK (boto)
- Auto deploy to prod (CFN)

Here are the steps to set up the pipeline and try this sample
1. Create 2 VPCs in your desired account (1 for prod , 1 for test)
1. Create your own S3 bucket in the desired region and enable versioning on the bucket 
1. Review the folder my-app-cft and UPDATE the "test-stack-configuration.json" and "prod-stack-configuration.json" files with your VPC IDs.
1. Review the push___.sh scripts and UPDATE your S3 bucket name
1. Upload (to S3) the pipline validation code: `./push_validation_pipline.sh`
1. Upload (to S3) your 'app' code: `./push_app.sh`
1. Create new stack in the CloudFormation service using `pipeline-cft.json` . Fill our the parameters. Its execution starts automatically!

Go make a coffee - it'll take about 2 minutes for the pipeline to be created and then about 8 minutes for the full deployment cycle to 'production' (you'll need to 'approve' it)
