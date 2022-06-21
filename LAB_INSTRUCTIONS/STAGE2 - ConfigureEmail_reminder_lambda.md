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

# STAGE 2B - Create the email_reminder_lambda function
Next You're going to create the lambda function which will will be used by the serverless application to create an email and then send it using `SES`<br />
Move to the lambda console [https://us-east-1.console.aws.amazon.com/lambda/home?region=us-east-1#/functions](https://us-east-1.console.aws.amazon.com/lambda/home?region=us-east-1#/functions)<br />
Click on `Create Function`
Select `Author from scratch`
For `Function name` enter `email_reminder_lambda`
and for runtime click the dropdown and pick `Python 3.9`
Expand `Change default execution role`
Pick to `Use an existing Role`
Click the `Existing Role` dropdown and pick `LambdaRole`
Click `Create Function`

# STAGE 2C - Configure the email_reminder_lambda function
Scroll down, to `Function code`
in the `lambda_function` code box, select all the code and delete it

Paste in this code

```
import boto3, os, json

FROM_EMAIL_ADDRESS = 'REPLACE_ME'

ses = boto3.client('ses')

def lambda_handler(event, context):
    # Print event data to logs .. 
    print("Received event: " + json.dumps(event))
    # Publish message directly to email, provided by EmailOnly or EmailPar TASK
    ses.send_email( Source=FROM_EMAIL_ADDRESS,
        Destination={ 'ToAddresses': [ event['Input']['email'] ] }, 
        Message={ 'Subject': {'Data': 'HydroTron is at your Service !'},
            'Body': {'Text': {'Data': event['Input']['message']}}
        }
    )
    return 'Success!'
```
This function will send an email to an address it's supplied with (by step functions) and it will be FROM the email address we specify.<br />
Select REPLACE_ME and replace with the HydroTron Sending Address which you noted down in STAGE1<br />
Click Deploy to configure the lambda function<br />
Scroll all the way to the top, and click the copy icon next to the lambda function ARN.<br />
Note this ARN down somewhere same as the email_reminder_lambda ARN<br />

# STAGE 2 - FINISH
At this point you have configured the lambda function which will be used eventually to send emails on behalf of the serverless application.
You can go ahead and move onto stage 3
