# Service Permissions<a name="howitworks-service-permissions"></a>

Amazon Lex uses AWS Identity and Access Management \(IAM\)[ service\-linked roles](https://docs.aws.amazon.com/console/iam/service-linked-role)\. Amazon Lex assumes these roles to call AWS services on behalf of your bots and bot channels\. The roles exist within your account, but are linked to Amazon Lex use cases and have predefined permissions\. Only Amazon Lex can assume these roles, and you can't modify their permissions\. You can delete them after deleting their related resources using IAM\. This protects your Amazon Lex resources because you can't inadvertently remove necessary permissions\. 

Amazon Lex uses two IAM service\-linked roles:
+ **AWSServiceRoleForLexBots**—Amazon Lex uses this service\-linked role to invoke Amazon Polly to synthesize speech responses for your bot and to call Amazon Comprehend for sentiment analysis\.
+ **AWSServiceRoleForLexChannels**—Amazon Lex uses this service\-linked role to post text to your bot when managing channels\.

You don't need to manually create either of these roles\. When you create your first bot using the console, Amazon Lex creates the **AWSServiceRoleForLexBots** role for you\. When you first associate a bot with a messaging channel, Amazon Lex creates the **AWSServiceRoleForLexChannels** role for you\. 

## Creating Resource\-Based Policies for AWS Lambda<a name="howitworks-lambda"></a>

When invoking Lambda functions, Amazon Lex uses resource\-based policies\. A *resource\-based policy* is attached to a resource; it lets you specify who has access to the resource and which actions they can perform on it\. This enables you to narrowly scope permissions between Lambda functions and the intents that you have created\. It also allows you to see those permissions in a single policy when you manage Lambda functions that have many event sources\. 

For more information, see [ Using Resource\-Based Polices for AWS Lambda \(Lambda Function Policies\)](http://docs.aws.amazon.com/lambda/latest/dg/access-control-resource-based.html) in the *AWS Lambda Developer Guide*\. 

 To create resource\-based policies for intents that you associate with a Lambda function, you can use the Amazon Lex console\. Or, you can use the AWS command line interface \(AWS CLI\)\. In the AWS CLI, use the Lambda [AddPermisssion](http://docs.aws.amazon.com/lambda/latest/dg/API_AddPermission.html) API with the `Principal` field set to `lex.amazonaws.com` and the `SourceArn` set to the ARN of the intent that is allowed to invoke the function\. 

## Deleting Service\-Linked Roles<a name="howitworks-delete-service-linked-roles"></a>

You can use the IAM console, the IAM CLI, or the IAM API to delete the `AWSServiceRoleForLexBots` and `AWSServiceRoleForLexChannels` service\-linked roles\. For more information, see [Deleting a Service\-Linked Role](http://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#delete-service-linked-role) in the *IAM User Guide*\.