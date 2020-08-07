# Step 2: Create a Lambda Function<a name="ex1-sch-appt-create-lambda-function"></a>

In this section, you create a Lambda function using a blueprint \(lex\-make\-appointment\-python\) that is provided in the Lambda console\. You also test the Lambda function by invoking it using sample Amazon Lex event data that is provided by the console\.

1. Sign in to the AWS Management Console and open the AWS Lambda console at [https://console\.aws\.amazon\.com/lambda/](https://console.aws.amazon.com/lambda/)\.

1. Choose **Create a Lambda function**\.

1. For **Select blueprint**, type **lex** to find the blueprint, and then choose the **lex\-make\-appointment\-python** blueprint\.

1. Configure the Lambda function as follows, and then choose **Create Function**\.
   + Type the Lambda function name \(`MakeAppointmentCodeHook`\)\.
   + For the role, choose **Create a new role from template\(s\)**, and then type a role name\.
   + Leave other default values\.

1. Test the Lambda function\.

   1. Choose **Actions**, and then choose**Configure test event**\.

   1. From the **Sample event template** list, choose **Lex\-Make Appointment \(preview\)**\. This sample event uses the Amazon Lex request/response model, with values set to match a request from your Amazon Lex bot\. For information about the Amazon Lex request/response model, see [Using Lambda Functions](using-lambda.md)\.

   1. Choose **Save and test**\.

   1. Verify that the Lambda function ran successfully\. The response in this case matches the Amazon Lex response model\.

**Next Step**  
[Step 3: Update the Intent: Configure a Code Hook](ex1-sch-appt-create-integrate.md)