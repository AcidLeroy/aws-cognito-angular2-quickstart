IoT-Fronted Quickstart  
===================================================

## What does this app do?
![QuickStart Angular2 Cognito App](/aws/meta/Cognito-Angular2-QuickStart.png?raw=true)

## Tech Stack
### Required Tools
* [aws cli](http://docs.aws.amazon.com/cli/latest/userguide/installing.html)
* [eb cli](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-install.html)
* [npm](https://www.npmjs.com/)
* [angular-cli](https://github.com/angular/angular-cli)

### Frameworks
* [AWS JavaScript SDK](http://docs.aws.amazon.com/AWSJavaScriptSDK/guide/browser-intro.html)
* [Angular 2](https://angular.io/docs/ts/latest/quickstart.html)
    * [TypeScript](https://www.typescriptlang.org/docs/tutorial.html)
* [Bootstrap](http://getbootstrap.com/)

## AWS Setup
##### Install the required tools
* Create an AWS account
* Install [npm](https://www.npmjs.com/)
* [Install or update your aws cli](http://docs.aws.amazon.com/cli/latest/userguide/installing.html)
* [Install or update your eb cli](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-install.html)
* [Install angular-cli](https://github.com/angular/angular-cli)


## Getting the code and running it locally
_This uses the pre-configured AWS resources hosted by AWS_

```
# Clone it from github
git clone --depth 1 git@github.com:awslabs/iot-frontend.git
```
```
# Install the NPM packages
cd iot-frontend
npm install
```
```
# Run the app in dev mode
npm start
```

## Creating AWS Resources
This sample application can be deployed to either Elastic Beanstalk or S3. S3 will host this application as a static site
while Elastic Beanstalk gives you the capability of adding backend operations to the application.

* [What is Elastic Beanstalk](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/Welcome.html)
* [What is S3](http://docs.aws.amazon.com/AmazonS3/latest/dev/Welcome.html)

** createResources.sh requires your [aws cli to be configured](http://docs.aws.amazon.com/cli/latest/userguide/controlling-output.html) for JSON output.  **

```
# Install the AWS resources and deploy your application to either Elastic Beanstalk or S3
cd aws
./createResources.sh
```

Running the above command will create the necessary AWS resources and build & deploy your code to AWS.
It will prompt you to choose your deployment target (S3 or Elastic Beanstalk). Choosing 'S3' makes your deployment
completely serverless, while choosing Elastic Beanstalk will create an EC2 instance that will host this NodeJS app.

*Caution:* You might incur AWS charges after running the setup script

## After initially running the ```createResources.sh``` script, use the below commands to rebuild and redeploy

### _S3:_ Update, Build and Deploy
```
# Build the project and sync the output with the S3 bucket
npm run build; cd dist; aws s3 sync . s3://[BUCKET_NAME]/
```
```
# Test your deployed application
curl –I http://[BUCKET_NAME].s3-website-[REGION].amazonaws.com/
```
*or*

### _Beanstalk:_ Update, Build and Deploy
```
# Commit your changes in order to deploy it to your environment
git add .
git commit
eb deploy
```
```
# View your deployed application in a browser
eb open
```
