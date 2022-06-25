# STAGE 4A - CREATE API LAMBDA FUNCTION WHICH SUPPORTS APIGATEWAY
Move to the Lambda console [https://console.aws.amazon.com/lambda/home?region=us-east-1#/functions](https://console.aws.amazon.com/lambda/home?region=us-east-1#/functions)<br />
Click on `Create Function`<br />
for `Function Name` use `api_lambda`<br />
for `Runtime` use `Python 3.9`<br />
Expand `Change default execution role`<br />
Select `Use an existing role`<br />
Choose the `LambdaRole` from the dropdown<br />
Click `Create Function`<br />

This is the lambda function which will support the API Gateway<br />

# STAGE 4B - CONFIGURE THE LAMBDA FUNCTION
Scroll down, and remove all the code from the `lambda_function` text box<br />
Inside this repository, there is a `documents` folder. In this folder, you can find the api_lambda.py file.<br />
Copy the contents of the file and paste it in the lambda function.<br />
This is the function which will provide compute to API Gateway.<br />
It's job is to be called by API Gateway when its used by the serverless front end part of the application (loaded by S3) It accepts some information from you, via API Gateway and then it starts a state machine execution - which is the logic of the application.<br />

You need to locate the `YOUR_STATEMACHINE_ARN` placeholder and replace this with the State Machine ARN you noted down in the previous step.
Click `Deploy` to save the lambda function and configuration.

# STAGE 4C - CREATE API
Now we have the api_lambda function created, the next step is to create the API Gateway, API and Method which the front end part of the serverless application will communicate with.<br />
Move to the API Gateway console [https://console.aws.amazon.com/apigateway/main/apis?region=us-east-1](https://console.aws.amazon.com/apigateway/main/apis?region=us-east-1)<br />
Click `APIs` on the menu on the left<br />
Locate the `REST API` box, and click `Build`. If you see a popup dialog `Create your first API` dismiss it by clicking `OK`<br />
Under `Create new API` ensure `New API` is selected.<br />

For `API name*` enter Hydrotron<br />
for `Endpoint Type` pick `Regional` Click `create API`<br />

# STAGE 4D - CREATE RESOURCE
Click the `Actions` dropdown and Click `Create Resource`<br />
Under resource name enter `Hydrotron`<br />
make sure that `Configure as proxy resource` is NOT ticked - this forwards everything as is, through to a lambda function, because we want some control, we DONT want this ticked.<br />
Towards the bottom MAKE SURE TO TICK `Enable API Gateway CORS`.<br />
This relaxes the restrictions on things calling on our API with a different DNS name, it allows the code loaded from the S3 bucket to call the API gateway endpoint.
if you DONT check this box, the API will fail<br />
Click `Create Resource`<br />

# STAGE 4E - CREATE METHOD
Ensure you have the `/hydrotron` resource selected, click `Actions` dropdown and click `create method`.<br />
In the small dropdown box which appears below `/hydrotron` select `POST` and click the `tick` symbol next to it.<br />
this method is what the front end part of the application will make calls to.<br />
Its what the api_lambda will provide services for.<br />

Ensure for Integration Type that Lambda Function is selected.<br />
Make sure us-east-1 is selected for Lambda Region<br />
In the Lambda Function box.. start typing api_lambda and it should autocomplete, click this auto complete (Make sure you pick api_lambda and not email reminder lambda)<br />

Make sure that `Use Default Timeout` box IS ticked.<br />
Make sure that `Use Lambda Proxy integration` box IS ticked, this makes sure that all of the information provided to this API is sent on to lambda for processing in the `event` data structure.<br />
if you don't tick this box, the API will fail<br />
Click `Save`<br />
You may see a dialogue stating `You are about to give API Gateway permission to invoke your Lambda function:`. AWS is asking for your OK to adjust the `resource policy` on the lambda function to allow API Gateway to invoke it. This is a different policy to the `execution role policy` which controls the permissions lambda gets.<br />

# STAGE 4F - DEPLOY API
Now the API, Resource and Method are configured - you now need to deploy the API out to API gateway, specifically an API Gateway STAGE.<br />
Click `Actions` Dropdown and `Deploy API`<br />
For `Deployment Stage` select `New Stage`<br />
for stage name and stage description enter `prod`<br />
Click `Deploy`<br />

At the top of the screen will be an `Invoke URL` .. note this down somewhere safe, you will need it in the next STAGE.<br />
This URL will be used by the client side component of the serverless application and this will be unique to you.<br />

# STAGE 4 - FINISH
At this point you have configured the last part of the AWS side of the serveless application.<br />
You now have :-<br />

* SES Configured<br />
* An Email Lambda function to send email using SES<br />
* A State Machine configured which can send EMAIL, SMS or BOTH after a certain time period when invoked.<br />
* An API, Resource & Method, which use a lambda function for backing deployed out to the PROD stage of API Gateway<br />












