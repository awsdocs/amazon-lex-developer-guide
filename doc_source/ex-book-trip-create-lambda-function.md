# Step 3: Create a Lambda function<a name="ex-book-trip-create-lambda-function"></a>

In this section you create a Lambda function using a blueprint \(**lex\-book\-trip\-python**\) provided in the AWS Lambda console\. You also test the Lambda function by invoking it using sample event data provided by the console\.

This Lambda function is written in Python\.

1. Sign in to the AWS Management Console and open the AWS Lambda console at [https://console\.aws\.amazon\.com/lambda/](https://console.aws.amazon.com/lambda/)\.

1. Choose **Create function**\.

1. Choose **Use a blueprint**\. Type **lex** to find the blueprint, choose the `lex-book-trip-python` blueprint\.

1. Configure the Lambda function as follows and then choose **Create Function**\.
   + Type a Lambda function name \(`BookTripCodeHook`\)\.
   + For the role, choose **Create a new role from AWS policy templates** and then type a role name\.
   + Leave the other default values\.

1. Test the Lambda function\. You invoke the Lambda function twice, using sample data for both booking a car and booking a hotel\. 

   1. Choose **Actions**, **Configure test event**\.

   1. Choose **Lex\-Book Hotel \(preview\)** from the **Sample event template** list\. 

      This sample event matches the Amazon Lex request/response model\. For more information, see [Using Lambda Functions](using-lambda.md)\.

   1. Choose **Save and test**\.

   1. Verify that the Lambda function successfully executed\. The response in this case matches the Amazon Lex response model\.

   1. Repeat the step\. This time you choose the **Lex\-Book Car \(preview\)** from the **Sample event template** list\. The Lambda function processes the car reservation\.

**Next Step**  
[Step 4: Add the Lambda Function as a Code Hook](ex-book-trip-create-integrate.md)
