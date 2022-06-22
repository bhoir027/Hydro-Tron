# STAGE 3A - CREATE STATE MACHINE ROLE
In this stage of the demo you need to create an IAM role which the state machine will use to interact with other AWS services.<br />
Go to `IAM` and click on `Roles` and Select `Custom trust policy`<br />
In Json editor, for *Principal* key, pass the parameter as *states.amazonaws.com*
in double quotations.<br />
Click on `Next`and attach 2 custom Inline policies `cloudwatchlogs` and `invokelambdasandsendSNS` and click `Next`<br />
Enter your `Role Name` as *StateMachineRole*.<br />
This Role will be used by your State machine to get permissions to other AWS services in AWS account.<br />
This Role consists of some permissions :
1) `cloudwatchlogs` : to generate logs
2) `invokelambdasandsendSNS` : State machine can use this permissions to interact with SNS and invoke Lambda functions.
SNS permissions are needed because State machine will be using this role<br />

After the role is created, Click on [https://us-east-1.console.aws.amazon.com/iamv2/home#/roles](https://us-east-1.console.aws.amazon.com/iamv2/home#/roles)<br />
Your role is created as "StateMachineRole"<br />

# STAGE 3B - CREATE STATE MACHINE
Move to the AWS Step Functions Console [https://us-east-1.console.aws.amazon.com/states/home?region=us-east-1#/homepage](https://us-east-1.console.aws.amazon.com/states/home?region=us-east-1#/homepage)<br />
Click the Menu at the top left and click State Machines<br />
Click `Create State Machine`<br />
Select `Write your workflow in code` which will allow you to use Amazon States Language
Scroll down for type select standard<br />
In this Repository under Documents folder, I have attached a statemachine.Json file.<br /> 
this is the Amazon States Language (ASL) file for the `Hydro-tron` state machine<br />
Copy the contents into your clipboard<br />
Move back to the step functions console<br />
Select all of the code snippet and delete it<br />
Paste in your clipboard<br />

Click the Refresh icon on the right side area ... next to the visual map of the state machine.<br />
Look through the visual overview and the ASL .. and make sure you understand the flow through the state machine.<br />

The state machine starts ... and then waits for a certain time period based on the Timer state. This is controlled by the web front end you will deploy soon.<br />
Then the ChoiceState is used, and this is a branching part of the state machine. Depending on the option picked in the UI, it either moves to :-<br />
* EmailOnly : Which sends an email reminder
* SMSOnly : Which sends only an SMS reminder
* EmailandSMS : which is a parallel state which runs both ParallelEmail and ParallelSMS which does both.

The state machine will control the flow through the serverless application.. once stated it will coordinate other AWS services as required.

# STAGE 3C - CONFIGURE STATE MACHINE
In the state machine ASL (the code on the left) locate the `EmailOnly` definition.<br />
Look for `EMAIL_LAMBDA_ARN` which is a placeholder, replace this with the email_reminder_lambda ARN you noted down in the previous step. This is the ARN of the lambda function you created. Next, locate the `ParallelEmail` definition.
Look for the `EMAIL_LAMBDA_ARN` which is a placeholder, replace this with the email_reminder_lambda ARN you noted down in the previous step. This is the ARN of the lambda function you created.

Scroll down to the bottom and click `next` For `State machine name` use `HydroTron`
Scroll down and under `Permissions` select `Choose an existing role` and select `StateMachineRole` from the dropdown.<br />
Scroll down, under `Logging`, change the `Log Level` to `All`<br />
Scroll down to the bottom and click `Create state machine`<br />

Locate the `ARN` for the state machine on the top left... note this down somewhere safe as `State Machine ARN`<br />

# STAGE 3 - FINISH
At this point you have configured the state machine which is the core part of the serverless application.
The state machine controls the flow through the application and is responsible for interacting with other AWS products and services.

