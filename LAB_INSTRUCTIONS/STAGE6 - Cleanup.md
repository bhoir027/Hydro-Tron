# Resources Clean UP
Move to the S3 console [https://s3.console.aws.amazon.com/s3/home?region=us-east-1](https://s3.console.aws.amazon.com/s3/home?region=us-east-1) Select the bucket you created<br />
Click `Empty`, type or copy/paste the bucket name and click `Empty`, Click `Exit`<br />
Click `Delete`, type or copy/paste the bucket name and click `Delete`, Click `Exit`<br />

Move to the API Gateway console [https://console.aws.amazon.com/apigateway/main/apis?region=us-east-1](https://console.aws.amazon.com/apigateway/main/apis?region=us-east-1)<br />
Check the box next to the hydrotron API<br />
Click `Actions` and then `Delete`<br />
Click `Delete`<br />

Move to the lambda console [https://console.aws.amazon.com/lambda/home?region=us-east-1#/functions](https://console.aws.amazon.com/lambda/home?region=us-east-1#/functions)
Check the box next to `email_reminder_lambda`, click `Actions`, Click `Delete`, Click `Delete`
Check the box next to `api_lambda`, click `Actions`, Click `Delete`, Click `Delete`.

Move to the Step Functions console [https://console.aws.amazon.com/states/home?region=us-east-1#/statemachines](https://console.aws.amazon.com/states/home?region=us-east-1#/statemachines)
Check the box next to HydrOTron, CLick `Delete`, then `Delete state machine`.

Move to the Pinpoint console [https://us-east-1.console.aws.amazon.com/pinpoint/home?region=us-east-1#/sms-account-settings/phoneNumbers](https://us-east-1.console.aws.amazon.com/pinpoint/home?region=us-east-1#/sms-account-settings/phoneNumbers)<br />
Check the box next to the origination number you created in stage 1.<br />
Click `Remove Phone Number`, conform and click `Delete`<br />

Go to the SES console and verified identities [https://us-east-1.console.aws.amazon.com/ses/home?region=us-east-1#/verified-identities](https://us-east-1.console.aws.amazon.com/ses/home?region=us-east-1#/verified-identities)<br />
Select one of the indentities, Click `Delete`, then click `Confirm`<br />
Pick the other verified identity, Click `Delete`, then click `Confirm`<br />

At this point you have removed all infrastructure used for this Mini-project and have completed the project itself.
