# Using Identity\-Based Policies \(IAM Policies\) for Amazon Lex<a name="access-control-managing-permissions"></a>

This topic provides examples of identity\-based policies that demonstrate how an account administrator can attach permissions policies to IAM identities \(that is, users, groups, and roles\) and thereby grant permissions to perform operations on Amazon Lex resources\. 

**Important**  
Before you proceed, we recommend that you review [Overview of Managing Access Permissions to Your Amazon Lex Resources](access-control-overview.md)\. 

The sections in this topic cover the following:
+  [Permissions Required to Use the Amazon Lex Console](#additional-console-required-permissions) 
+ [AWS Managed \(Predefined\) Policies for Amazon Lex](#access-policy-examples-aws-managed)
+ [Examples of Customer Managed Policies ](#access-policy-examples-for-sdk-cli) 

The following is an example of a permissions policy:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "lex:PostText"
             ],   
            "Resource": [
                "arn:aws:lex:us-east-1:account-id:bot:OrderPizza:*"
            ]
        }
    ]
}
```

The policy has one statement that grants permission to use the `PostText` action with the `OrderPizza` bot\. The resource specifies a wildcard character \(\*\) to give permission to any alias of the `OrderPizza` bot\.

The policy doesn't specify the `Principal` element because you don't specify the principal who gets the permission in an identity\-based policy\. When you attach a policy to a user, the user is the implicit principal\. When you attach a permissions policy to an IAM role, the principal identified in the role's trust policy gets the permissions\. 

For a table showing all of the Amazon Lex API actions and the resources that they apply to, see [Amazon Lex API Permissions: Actions, Resources, and Conditions Reference](lex-api-permissions-ref.md)\.

## Permissions Required to Use the Amazon Lex Console<a name="additional-console-required-permissions"></a>

The permissions reference table lists the Amazon Lex API operations and shows the required permissions for each operation\. For more information about Amazon Lex API operations, see [Amazon Lex API Permissions: Actions, Resources, and Conditions Reference](lex-api-permissions-ref.md)\.

 To use the Amazon Lex console, you need to grant permissions for additional actions as shown in the following permissions policy: 

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "cloudwatch:GetMetricStatistics",
                "cloudwatch:DescribeAlarms",
                "cloudwatch:DescribeAlarmsForMetric",
                "kms:DescribeKey",
                "kms:ListAliases",
                "lambda:GetPolicy",
                "lambda:ListFunctions",
                "lex:*",
                "polly:DescribeVoices",
                "polly:SynthesizeSpeech"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "lambda:AddPermission",
                "lambda:RemovePermission"
            ],
            "Resource": "*",
            "Condition": {
                "StringLike": {
                    "lambda:Principal": "lex.amazonaws.com"
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": [
                "iam:GetRole",
                "iam:DeleteRole"
            ],
            "Resource": [
                "arn:aws:iam::*:role/aws-service-role/lex.amazonaws.com/AWSServiceRoleForLexBots",
                "arn:aws:iam::*:role/aws-service-role/channels.lex.amazonaws.com/AWSServiceRoleForLexChannels"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "iam:CreateServiceLinkedRole"
            ],
            "Resource": [
                "arn:aws:iam::*:role/aws-service-role/lex.amazonaws.com/AWSServiceRoleForLexBots"
            ],
            "Condition": {
                "StringLike": {
                    "iam:AWSServiceName": "lex.amazonaws.com"
                }
           }
        },
        {
            "Effect": "Allow",
            "Action": [
                "iam:DetachRolePolicy"
            ],
            "Resource": [
                "arn:aws:iam::*:role/aws-service-role/lex.amazonaws.com/AWSServiceRoleForLexBots"
            ],
            "Condition": {
                "StringLike": {
                    "iam:PolicyArn": "arn:aws:iam::aws:policy/aws-service-role/AmazonLexBotPolicy"
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": [
                "iam:CreateServiceLinkedRole"
            ],
            "Resource": [
                "arn:aws:iam::*:role/aws-service-role/channels.lex.amazonaws.com/AWSServiceRoleForLexChannels"
            ],
            "Condition": {
                "StringLike": {
                    "iam:AWSServiceName": "channels.lex.amazonaws.com"
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": [
                "iam:DetachRolePolicy"
            ],
            "Resource": [
                "arn:aws:iam::*:role/aws-service-role/channels.lex.amazonaws.com/AWSServiceRoleForLexChannels"
            ],
            "Condition": {
                "StringLike": {
                    "iam:PolicyArn": "arn:aws:iam::aws:policy/aws-service-role/LexChannelPolicy"
                }
            }
        }
    ]
 }
```

The Amazon Lex console needs these additional permissions for the following reasons:
+  `cloudwatch` permissions to view performance and monitoring information in the console\. 
+ `iam` actions to assume IAM roles for making calls to Lambda functions and processing data for a bot channel association\.
+ `kms` actions to manage the AWS Key Management Service keys used to encrypt data when creating a bot channel association\.
+ `lambda` actions to display Lambda functions that your bot can use, and to grant Lex the necessary permissions for your bot to invoke these functions\.
+ `lex` actions so that the console can display Amazon Lex resources in the account\.
+ `polly` actions so that the console can display Amazon Polly voices and so that it can translate text to speech\.
+ `iam` actions so that the console can manage server\-linked roles that grant permission to use other AWS resources\.

## AWS Managed \(Predefined\) Policies for Amazon Lex<a name="access-policy-examples-aws-managed"></a>

AWS addresses many common use cases by providing standalone IAM policies that are created and administered by AWS\. Managed policies grant necessary permissions for common use cases so you can avoid having to investigate which permissions are needed\. For more information, see [AWS Managed Policies](http://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\. 

The following AWS managed policies, which you can attach to users in your account, are specific to Amazon Lex:
+ **ReadOnly** — Grants read\-only access to Amazon Lex resources\. 
+ **RunBotsOnly** — Grants access to run Amazon Lex conversational bots\.
+ **FullAccess** — Grants full access to create, read, update, delete, and run all Amazon Lex resources\. Grants access to associate Lambda functions whose name starts with `AmazonLex` with Amazon Lex intents\.

**Note**  
You can review these permissions policies by signing in to the IAM console and searching for specific policies\.

You can also create your own custom IAM policies to allow permissions for Amazon Lex API actions\. You can attach these custom policies to the IAM users or groups that require those permissions\. 

## Examples of Customer Managed Policies<a name="access-policy-examples-for-sdk-cli"></a>

In this section, we provide examples of user policies that grant permissions for various Amazon Lex actions\. These policies work with the AWS SDKs or the AWS command line interface \(AWS \)\. When you use the console, you need to grant additional permissions specific to the console, which is discussed in [Permissions Required to Use the Amazon Lex Console](#additional-console-required-permissions)\.

**Note**  
All examples use the us\-east\-1 Region and contain fictitious account IDs\.

**Topics**
+ [Example 1: Allow a User to Delete Any Bot](#access-policy-example-update-any-bot)
+ [Example 2: Allow a User to Update a Specific Bot](#access-policy-example-update-specific-bot)
+ [Example 3: Allow a User to Manage a Specific Bot](#access-policy-example-build-specific-bot)

### Example 1: Allow a User to Delete Any Bot<a name="access-policy-example-update-any-bot"></a>

The following permissions policy grants the user permissions to delete any bot that exists in the `us-east-1` Region\. 

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "lex:DeleteBot"
            "Resource": [
                "*"
            ]
        }
    ]
}
```

### Example 2: Allow a User to Update a Specific Bot<a name="access-policy-example-update-specific-bot"></a>

The following policy grants the user permissions to update a specific bot in the `us-east-1` Region, in this case, the bot named "PizzaBot\." 

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "lex:PutBot"
            "Resource": [
                "arn:aws:lex:us-east-1:account-id:bot:PizzaBot:$LATEST"
            ]
        }
    ]
}
```

### Example 3: Allow a User to Manage a Specific Bot<a name="access-policy-example-build-specific-bot"></a>

The following permissions policy grants the user permissions to build and test a pizza ordering, and can only use the `OrderPizza` intent and `Toppings` slot type when editing the bot in the us\-east\-1 region\. The policy uses the `lex:associatedIntents` and `lex:associatedSlotType` to limit the intent and slot types that the user can use for this bot\.

```
{
    "Version": "2012-10-17",
    "Statement": [
       {
           "Effect": "Allow",
           "Action": [
                "lex:Create*Version",
                "lex:Post*",
                "lex:Put*",
                "lex:Delete*"
            ],
            "Resource": [
                "arn:aws:lex:us-east-1:*:bot:PizzaBot:*",
                "arn:aws:lex:us-east-1:*:intent:OrderPizza:*",
                "arn:aws:lex:us-east-1:*:slottype:Toppings:*"
            ],
            "Condition": {
                "ForAllValues:StringEqualsIfExists": {
                    "lex:associatedIntents": [
                        "OrderPizza"
                    ],
                    "lex:associatedSlotTypes": [
                        "Toppings"
                    ]
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": [
                "lex:Get*"
            ],
            "Resource": [
                "arn:aws:lex:us-east-1:*:bot:*",
                "arn:aws:lex:us-east-1:*:intent:*",
                "arn:aws:lex:us-east-1:*:slottype:*"
            ]
        }
    ]
 }
```