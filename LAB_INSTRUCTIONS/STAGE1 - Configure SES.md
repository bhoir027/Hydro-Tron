# STAGE 1A - VERIFY SES APPLICATION SENDING EMAIL ADDRESS
The Hydro-Tron application is going to send reminder messages via SMS and Email. It will use the simple email service or SES. In production, it could be configured to allow sending from the application email, to any users of the application. SES starts off in sandbox mode, which means you can only sent to verified addresses (to avoid you spamming).<br />

Ensure you are logged into an AWS account, have admin privileges and are in the `us-east-1` / `N. Virginia` Region<br />
Move to the `SES` console [https://us-east-1.console.aws.amazon.com/ses/home?region=us-east-1#](https://us-east-1.console.aws.amazon.com/ses/home?region=us-east-1#)<br />
Click on `Verified Identities` under Configuration Click `Create Identity`<br />
Check the *Email Address* checkbox
Ideally you will need a `sending` email address for the application and a `receiving email address` for your test customer. But you can use the same email for both.<br />

For my application email ... the email the app will send from i'm going to use `thekaranbhoir+hydrotron@gmail.com`<br />
Enter whatever email you want to use to send in the box (it needs to be a valid address as it will be checked)<br />
Click `Create Identity`<br />
You will receive an email to this address containing a link to click<br />
Click that link<br />
You should see a `Congratulations!` message<br />
Return to the SES console and `Refresh` your browser, the verification status should now be `verified`<br />
Record this address somewhere save as the `HydroTron Sending Address`<br />

# STAGE 1B - VERIFY SES APPLICATION CUSTOMER EMAIL ADDRESS
If you want to use a different email address for the test customer (recommended), follow the steps below<br />
Click `Create Identity`<br />
Check the *Email Address* checkbox For my application email ... the email for my test customer is `thekaranbhoir+customer@gmail.com`<br />
Enter whatever email you want to use to send in the box (it needs to be a valid address as it will be checked)<br />
Click `Create Identity`<br />
You will receive an email to this address containing a link to click<br />
Click that link<br />
You should see a `Congratulations!` message<br />
Return to the SES console and refresh your browser, the verification status should now be `verified`<br />
Record this address somewhere save as the `HydroTron Customer Address`<br />

# STAGE 1C - Verify an SMS number
Move to the SNS Console [https://us-east-1.console.aws.amazon.com/sns/v3/home?region=us-east-1#/dashboard](https://us-east-1.console.aws.amazon.com/sns/v3/home?region=us-east-1#/dashboard)<br />
Click the menu icon on the left.<br />
Click `Text Messaging (SMS)` under `Mobile`.<br />
Scroll down and in `Sandbox destination phone numbers` click `Add phone number`.<br />
Enter the international number format of a phone number you control.<br />
Pick the `verification message language` you want to use. Click `Add phone Number`.<br />
you will recieve a verification number on your phone, enter it onto the `Verification code` box and click `Verify phone number`.<br />

# STAGE 1D - Verify an SMS Number (US and other countries requiring an origination number)
Click `Origination numbers` under `Mobile` or move to `Pinpoint` console in a new tab, and click `phone numbers` under `SMS and Voice`. <br />
Click `Request phone number`.<br />
Choose the country of your phone number in the `Country` dropdown.<br />
Select `Toll-free` from `number type`.<br />
for `Default message type` pick `Transactional`.<br />
Scroll down, click `Next` then `Request`.<br />

Move back to the `SNS Console` [https://us-east-1.console.aws.amazon.com/sns/v3/home?region=us-east-1#/dashboard](https://us-east-1.console.aws.amazon.com/sns/v3/home?region=us-east-1#/dashboard)<br />
Click the menu icon on the left.<br />
Click `Text Messaging (SMS)` under `Mobile`.<br />
Scroll down and in `Sandbox destination phone numbers` click `Add phone number`.<br />
Enter the international number format of a phone number you control.<br />
Pick the `verification message language` you want to use.<br />
Click `Add phone Number`.<br />
you will recieve a verification number on your phone, enter it onto the `Verification code` box and click `Verify phone number`.<br />

# STAGE 1 - FINISH
At this point you have whitelisted 2 email addresses for use with SES.<br />
* the `HydroTron Sending Address`.<br />
* the `HydroTron Customer Address`.<br />
You have also configured an SMS number within SNS.<br />

These will be configured and used by the application in later stages. At this point you have finished all the tasks needed in this STAGE.
