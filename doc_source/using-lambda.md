# Using Lambda Functions<a name="using-lambda"></a>

You can create AWS Lambda functions to use as code hooks for your Amazon Lex bot\. You can identify Lambda functions to perform initialization and validation, fulfillment, or both in your intent configuration\.

We recommend that you use a Lambda function as a code hook for your bot\. Without a Lambda function, your bot returns the intent information to the client application for fulfillment\. 

**Topics**
+ [Lambda Function Input Event and Response Format](lambda-input-response-format.md)
+ [Amazon Lex and AWS Lambda Blueprints](lex-lambda-blueprints.md)