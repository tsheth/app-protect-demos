# app-protect-lambda
Sample Cloud Formation Template to deploy a basic Lambda Function for App Protect demos
## Detailed Description
This CFT deploys a sample Lambda Function for usage with Deep Security App Protect demos.

Currently, this CFT **only works in the US West (Oregon) region!!!**

## Pre-Requisites for Usage
* An AWS Account (Full Access)
* A Deep Security App Protect account

### Usage Instructions

1. Clone the repository
```
git clone https://gitlab.com/howiehowerton/app-protect-lambda.git
```
2. Change into the app-protect-lambda directory
```
cd app-protect-lambda
```
3. In your AWS Console, go to the CloudFormation Service

4. Click on "Create stack"

5. Select "Upload a template file" and browse to the template.yaml file in your app-protect-lambda directory.  Then, click 'Next'

6. Give the Stack a name (ie: app-protect-lambda) and paste in the values for your Key + Secret.  Then, click 'Next'.  Specify any additional configs you'd like and then create the stack.

Note: To obtain your Key and Secret, you'll need to:
* Log into your App Protect account
* Add a new group
* Copy your Key and Secret

The App Protect (immunio) library (which is added via a custom layer/runtime for Lambda in the CFT) uses the Key and Secret to identify the App Protect group to which the application belongs.

### Attacking the Lambda Function
The function deployed via the CFT is a fairly basic "hello world" application.  However, it has a command injection / "Illegal File Access" vulnerability that can be exploited by passing a malicious value for the 'file' query parameter key.
```
http://<YOUR_LAMBDA_URL_HERE>/?file=../../proc/self/environ
```
The above will cause the function to attempt to read a file from the underlying file system.  In this case.. from /proc/self/environ



