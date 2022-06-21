# STAGE 2A - CREATE THE Lambda Execution Role for Lambda
In this stage you need to create an IAM role which the email_reminder_lambda will use to interact with other AWS services.<br />
You could create this manually.<br />
Steps are as follows to create a role which can be assumed by Lambda function.<br />
Creating the Custom policies beforehand creating the role<br />
Go to `IAM` service and click on `Policies` and then click `Create Policy`<br />
Inside the Documents folder in this repository, I have provided a Json file named *cloudwatchlogs.json* and *snsandsespermissions.json*<br />
Paste the content from *cloudwatchlogs.json* and *snsandsespermissions.json* files in the inline policy json editor respectively<br/>
Click on `create policy`<br />
Now click on `create role` and select `AWS service` and under Use Case select `Lambda` as it allows Lambda function to call other AWS services<br />
Click on `Next` and attach your inline policies `cloudwatchlogs` and `snsandsespermissions` to the role<br />
Under `Role Name` mention *"LambdaRole"* and under `Description` mention that this will allow Lambda functions to call AWS services on your behalf<br />
Click on `Create Role` and hence the Lambda assumable role will be created which can be called by lambda function.

