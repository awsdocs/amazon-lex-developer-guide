# Amazon Lex Identity\-Based Policy Examples<a name="security_iam_id-based-policy-examples"></a>

By default, IAM users and roles don't have permission to create or modify Amazon Lex resources\. They also can't perform tasks using the AWS Management Console, AWS CLI, or AWS API\. An IAM administrator must create IAM policies that grant users and roles permission to perform specific API operations on the specified resources that they need\. The administrator must then attach those policies to the IAM users or groups that require those permissions\.

To learn how to create an IAM identity\-based policy using example JSON policy documents, see [Creating Policies on the JSON Tab](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create.html#access_policies_create-json-editor) in the *IAM User Guide*\.

**Topics**
+ [Policy Best Practices](#security_iam_service-with-iam-policy-best-practices)
+ [Using the Amazon Lex Console](#security_iam_id-based-policy-examples-console)
+ [AWS Managed \(Predefined\) Policies for Amazon Lex](#access-policy-examples-aws-managed)
+ [Example: Allow Users to View Their Own Permissions](#security_iam_id-based-policy-examples-view-own-permissions)
+ [Example: Delete All Amazon Lex Bots](#security_iam_id-based-policy-examples-access-one-bot)
+ [Example: Use a Tag to Access a Resource](#security_iam_id-based-policy-examples-tag)

## Policy Best Practices<a name="security_iam_service-with-iam-policy-best-practices"></a>

Identity\-based policies are very powerful\. They determine whether someone can create, access, or delete Amazon Lex resources in your account\. These actions can incur costs for your AWS account\. When you create or edit identity\-based policies, follow these guidelines and recommendations:
+ **Get Started Using AWS Managed Policies** – To start using Amazon Lex quickly, use AWS managed policies to give your employees the permissions they need\. These policies are already available in your account and are maintained and updated by AWS\. For more information, see [Get Started Using Permissions With AWS Managed Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#bp-use-aws-defined-policies) in the *IAM User Guide*\.
+ **Grant Least Privilege** – When you create custom policies, grant only the permissions required to perform a task\. Start with a minimum set of permissions and grant additional permissions as necessary\. Doing so is more secure than starting with permissions that are too lenient and then trying to tighten them later\. For more information, see [Grant Least Privilege](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#grant-least-privilege) in the *IAM User Guide*\.
+ **Enable MFA for Sensitive Operations** – For extra security, require IAM users to use multi\-factor authentication \(MFA\) to access sensitive resources or API operations\. For more information, see [Using Multi\-Factor Authentication \(MFA\) in AWS](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa.html) in the *IAM User Guide*\.
+ **Use Policy Conditions for Extra Security**– To the extent that it's practical, define the conditions under which your identity\-based policies allow access to a resource\. For example, you can write conditions to specify a range of allowable IP addresses that a request must come from\. You can also write conditions to allow requests only within a specified date or time range, or to require the use of SSL or MFA\. For more information, see [IAM JSON Policy Elements: Condition](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_condition.html) in the *IAM User Guide*\.

## Using the Amazon Lex Console<a name="security_iam_id-based-policy-examples-console"></a>

To access the Amazon Lex console, you must have a minimum set of permissions\. These permissions must allow you to list and view details about the Amazon Lex resources in your AWS account\. If you create an identity\-based policy that applies permissions that are more restrictive than the minimum required permissions, the console won't function as intended for entities \(IAM users or roles\) with that policy\.

The following are the minimum permissions required to use the Amazon Lex console\. 

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
          "Action": "kendra:ListIndices",
          "Resource": "*"
       },
        {
            "Effect": "Allow",
            "Action": [
                "lambda:AddPermission",
                "lambda:RemovePermission"
            ],
            "Resource": "arn:aws:lambda:*:*:function:AmazonLex*",
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
                "iam:DeleteServiceLinkedRole",
                "iam:GetServiceLinkedRoleDeletionStatus"
            ],
            "Resource": [
                "arn:aws:iam::*:role/aws-service-role/lex.amazonaws.com/AWSServiceRoleForLexBots"
            ]
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
                "iam:DeleteServiceLinkedRole",
                "iam:GetServiceLinkedRoleDeletionStatus"
            ],
            "Resource": [
                "arn:aws:iam::*:role/aws-service-role/channels.lex.amazonaws.com/AWSServiceRoleForLexChannels"
            ]
        },
        {
          "Action": [
            "iam:PassRole"
          ],
            "Effect": "Allow",
          "Resource": [
                "arn:aws:iam::*:role/aws-service-role/lex.amazonaws.com/AWSServiceRoleForLexBots"
            ],
          "Condition": {
            "StringLike": {
               "iam:PassedToService": [
                  "lex.amazonaws.com"
              ]
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
+ `cloudwatch` permissions allow you to view performance and monitoring information in the console\.
+ `iam` actions allow Amazon Lex to assume IAM roles for making calls to Lambda functions and processing data for a bot channel association\.
+ `iam` actions allow you to use the console to manage server\-linked roles that grant permission to use other AWS resources\.
+ `kendra` actions allow you to list the Amazon Kendra indexes in your account\.
+ `kms` actions allow you to manage the AWS Key Management Service keys used to encrypt data when creating a bot channel association\.
+ `lambda` actions allow you to display the Lambda functions that your bot can use, and to grant Amazon Lex the necessary permissions for your bot to invoke these functions\.
+ `lex` actions allow the console to display the Amazon Lex resources in the account\.
+ `polly` actions allow the console to display the available Amazon Polly voices and translate text to speech\.

You don't need to allow minimum console permissions for users that are making calls only to the AWS CLI or the AWS API\. Instead, allow access to only the actions that match the API operation that you're trying to perform\.

For more information, see [Adding Permissions to a User](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_change-permissions.html#users_change_permissions-add-console) in the *IAM User Guide*\.

## AWS Managed \(Predefined\) Policies for Amazon Lex<a name="access-policy-examples-aws-managed"></a>

AWS addresses many common use cases by providing standalone IAM policies that are created and administered by AWS\. These policies are called AWS managed policies\. AWS managed policies make it easier for you to assign appropriate permissions to users, groups, and roles than if you had to write the policies yourself\.\. For more information, see [AWS Managed Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

The following AWS managed policies, which you can attach to groups and roles in your account, are specific to Amazon Lex:
+ **ReadOnly** — Grants read\-only access to Amazon Lex resources\.
+ **RunBotsOnly** — Grants access to run Amazon Lex conversational bots\.
+ **FullAccess** — Grants full access to create, read, update, delete, and run all Amazon Lex resources\. Also grants the ability to associate Lambda functions whose name starts with `AmazonLex` with Amazon Lex intents\.

**Note**  
You can review these permissions policies by signing in to the IAM console and searching for specific policies\.

You can also create your own custom IAM policies to allow permissions for Amazon Lex API actions\. You can attach these custom policies to the IAM roles or groups that require those permission\.

## Example: Allow Users to View Their Own Permissions<a name="security_iam_id-based-policy-examples-view-own-permissions"></a>

This example policy allows IAM users to view the inline and managed policies that are attached to their user identity\. This policy includes permissions to complete this action on the console or programmatically using the AWS CLI or AWS API\.

```
{
       "Version": "2012-10-17",
       "Statement": [
           {
               "Sid": "ViewOwnUserInfo",
               "Effect": "Allow",
               "Action": [
                   "iam:GetUserPolicy",
                   "iam:ListGroupsForUser",
                   "iam:ListAttachedUserPolicies",
                   "iam:ListUserPolicies",
                   "iam:GetUser"
               ],
               "Resource": [
                   "arn:aws:iam::*:user/${aws:username}"
               ]
           },
           {
               "Sid": "NavigateInConsole",
               "Effect": "Allow",
               "Action": [
                   "iam:GetGroupPolicy",
                   "iam:GetPolicyVersion",
                   "iam:GetPolicy",
                   "iam:ListAttachedGroupPolicies",
                   "iam:ListGroupPolicies",
                   "iam:ListPolicyVersions",
                   "iam:ListPolicies",
                   "iam:ListUsers"
               ],
               "Resource": "*"
           }
       ]
   }
```

## Example: Delete All Amazon Lex Bots<a name="security_iam_id-based-policy-examples-access-one-bot"></a>

This example policy grants an IAM user in your AWS account permission to delete any bot in your account\.

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

## Example: Use a Tag to Access a Resource<a name="security_iam_id-based-policy-examples-tag"></a>

This example policy grants an IAM user or role in your AWS account permission to use the `PostText` operation with any resource tagged with the key **Department** and the value **Support**\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": "lex:PostText",
            "Effect": "Allow",
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "lex:ResourceTag/Department": "Support"
                }
            }
        }
    ]
}
```