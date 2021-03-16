# Amazon Lex Identity\-Based Policy Examples<a name="security_iam_id-based-policy-examples"></a>

By default, IAM users and roles don't have permission to create or modify Amazon Lex resources\. They also can't perform tasks using the AWS Management Console, AWS CLI, or AWS API\. An IAM administrator must create IAM policies that grant users and roles permission to perform specific API operations on the specified resources that they need\. The administrator must then attach those policies to the IAM users or groups that require those permissions\.

To learn how to create an IAM identity\-based policy using example JSON policy documents, see [Creating Policies on the JSON Tab](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create.html#access_policies_create-json-editor) in the *IAM User Guide*\.

**Topics**
+ [Policy Best Practices](#security_iam_service-with-iam-policy-best-practices)
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

## AWS Managed \(Predefined\) Policies for Amazon Lex<a name="access-policy-examples-aws-managed"></a>

AWS addresses many common use cases by providing standalone IAM policies that are created and administered by AWS\. These policies are called AWS managed policies\. AWS managed policies make it easier for you to assign appropriate permissions to users, groups, and roles than if you had to write the policies yourself\.\. For more information, see [AWS Managed Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

The following AWS managed policies, which you can attach to groups and roles in your account, are specific to Amazon Lex:
+ **AmazonLexReadOnly** — Grants read\-only access to Amazon Lex resources\.
+ **AmazonLexRunBotsOnly** — Grants access to run Amazon Lex conversational bots\.
+ **AmazonLexFullAccess** — Grants full access to create, read, update, delete, and run all Amazon Lex resources\. Also grants the ability to associate Lambda functions whose name starts with `AmazonLex` with Amazon Lex intents\.

**Note**  
You can review these permissions policies by signing in to the IAM console and searching for specific policies\.

The **AmazonLexFullAccess** policy doesn't grant the user permission to use the `KendraSearchIntent` intent to query an Amazon Kendra index\. To query an index, you must add additional permissions to the policy\. For the required permissions, see [IAM Policy for Amazon Kendra Search](built-in-intent-kendra-search.md#kendra-search-iam)\.

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
            ],
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