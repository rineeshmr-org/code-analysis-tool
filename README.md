# AWS Bedrock Code Analysis

A secure, serverless app that connects S3-stored code with Claude 3 Sonnet through a simple chat interface. Ask questions about your code and get intelligent insights—deployed with one click via CloudFormation with enterprise-grade security.

## Prerequisites

1. **AWS Account** with permissions to create:
   - CloudFormation stacks
   - IAM roles
   - Lambda functions
   - S3 buckets
   - API Gateway resources

2. **Region Selection**
   - Deploy in `us-east-1` (N. Virginia) region
   - Claude 3 Sonnet is currently only available in specific regions

3. **Bedrock Model Access**
   - Enable access to Claude 3 Sonnet model before deployment
   - See instructions below

## Enabling Bedrock Model Access

1. Navigate to [Amazon Bedrock Console](https://console.aws.amazon.com/bedrock/home)
2. Ensure you're in the `us-east-1` region
3. Click on "Model access" in the left sidebar
4. Find "Anthropic Claude 3 Sonnet"
5. Check the box next to it
6. Click "Manage model access"
7. Select "Enable"
8. Wait for model status to show as "Available"

## Deployment Instructions

### Option 1: One-Click Deployment
1. Click the "Deploy to AWS" button below-
   [![Deploy to AWS](https://d2908q01vomqb2.cloudfront.net/f1f836cb4ea6efb2a0b1b99f41ad8b103eff4b59/2017/02/10/launchdark.gif)](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=code-analysis&templateURL=https://your-template-url.com)

2. Enter required parameters:
   - **AWSAccountId**: Your 12-digit AWS account ID
   - **S3BucketName**: Unique name for code storage bucket

3. Click "Next" through the remaining screens
4. Check "I acknowledge that AWS CloudFormation might create IAM resources"
5. Click "Create stack"

### Option 2: Manual Deployment
1. Download the CloudFormation template from this repository
2. Sign in to [AWS CloudFormation Console](https://console.aws.amazon.com/cloudformation/)
3. Select the `us-east-1` region
4. Click "Create stack" → "With new resources (standard)"
5. Choose "Upload a template file" and upload the template
6. Enter stack name and required parameters
7. Follow on-screen instructions to complete deployment

## Using the Application

1. Once deployment completes, find these URLs in CloudFormation outputs:
   - **ChatInterface**: URL for the web interface
   - **ApiEndpoint**: API endpoint URL

2. To analyze code:
   - Upload your code file to the created S3 bucket
   - Open the chat interface URL
   - Enter the S3 file key (e.g., `example.py` or `folder/script.js`)
   - Type your question about the code
   - Click "Send"

3. File key format:
   - For file `s3://your-bucket-name/folder/file.py`, enter `folder/file.py`
   - For file at bucket root, enter just the filename

## Troubleshooting

### Common Issues

1. **Access Denied Error**
   - Verify Bedrock model access is enabled
   - Check that you're using the correct region (us-east-1)

2. **File Not Found**
   - Confirm the S3 file key is correct
   - Verify file has been uploaded to the bucket

3. **CORS Issues**
   - Access chat interface via provided URL
   - Don't use S3 website URL directly

## Security Considerations

- All code remains within your AWS account
- S3 bucket has server-side encryption enabled
- IAM roles use least-privilege permissions
- API Gateway has resource policies for access control

## Cleanup

To remove all created resources:
1. Navigate to CloudFormation console
2. Select the stack you created
3. Click "Delete"
4. Wait for stack deletion to complete
5. Empty and delete the S3 buckets manually if needed

## Support

For issues or questions, please create a GitHub issue or contact rineeshmr@gmail.com.

