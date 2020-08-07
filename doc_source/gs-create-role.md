# Step 1: Create a Service\-Linked Role \(AWS CLI\)<a name="gs-create-role"></a>

Amazon Lex assumes AWS Identity and Access Management service\-linked roles to call AWS services on behalf of your bots\. The roles, which are in your account, are linked to Amazon Lex use cases and have predefined permissions\. For more information, see [Using Service\-Linked Roles for Amazon Lex](using-service-linked-roles.md)\.

If you've already created an Amazon Lex bot using the console, the service\-linked role was created automatically\. Skip to [Step 2: Create a Custom Slot Type \(AWS CLI\)](gs-create-flower-types.md)\. 

**To create a service\-linked role \(AWS CLI\)**

1. In the AWS CLI, type the following command:

   ```
   aws iam create-service-linked-role --aws-service-name lex.amazonaws.com
   ```

1. Check the policy using the following command:

   ```
   aws iam get-role --role-name AWSServiceRoleForLexBots
   ```

   The response is:

   ```
   {
       "Role": {
           "AssumeRolePolicyDocument": {
               "Version": "2012-10-17", 
               "Statement": [
                   {
                       "Action": "sts:AssumeRole", 
                       "Effect": "Allow", 
                       "Principal": {
                           "Service": "lex.amazonaws.com"
                       }
                   }
               ]
           },
           "RoleName": "AWSServiceRoleForLexBots", 
           "Path": "/aws-service-role/lex.amazonaws.com/", 
           "Arn": "arn:aws:iam::account-id:role/aws-service-role/lex.amazonaws.com/AWSServiceRoleForLexBots"
   }
   ```

## Next Step<a name="gs-create-next-2"></a>

[Step 2: Create a Custom Slot Type \(AWS CLI\)](gs-create-flower-types.md)