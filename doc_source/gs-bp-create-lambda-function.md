# Step 3: Create a Lambda Function \(Console\)<a name="gs-bp-create-lambda-function"></a>

Create a Lambda function \(using the **lex\-order\-flowers\-python** blueprint\) and perform test invocation using sample event data in the AWS Lambda console\. 

You return to the Amazon Lex console and add the Lambda function as the code hook to fulfill the `OrderFlowers` intent in the `OrderFlowersBot` that you created in the preceding section\.

**To create the Lambda function \(console\)**

1. Sign in to the AWS Management Console and open the AWS Lambda console at [https://console\.aws\.amazon\.com/lambda/](https://console.aws.amazon.com/lambda/)\.

1. Choose **Create a Lambda function**\.

1. On **Select blueprint**, type **lex** in the filter text box to find the blueprint, choose the `lex-order-flowers-python` blueprint\. 

   Lambda function blueprints are provided in both Node\.js and Python\. For this exercise, use the Python\-based blueprint\.

1. Choose **Next** on the **Configure Triggers** page\.

1. On the **Configure function** page, do the following, and then choose **Next**\. 

   + Type a Lambda function name \(`OrderFlowersCodeHook`\)\.

   + For the IAM role, choose **Create a new role from template\(s\)**\.

   + Type a role name\.

   + Leave the other default values\.

1. On the **Review** page, choose **Create function**\.

1. Test the Lambda function\.

   1. Choose **Actions**, **Configure test event**\.

   1. Choose **Lex\-Order Flowers \(preview\)** from the **Sample event template** list\. This sample event matches the Amazon Lex request/response model \(see [Using Lambda Functions](using-lambda.md)\)\.

   1. Choose **Save and test**\.

   1. Verify that the Lambda function successfully executed\. The response in this case matches the Amazon Lex response model\.

**Next Step**  
[Step 4: Add the Lambda Function as Code Hook \(Console\)](gs-bp-create-integrate.md)