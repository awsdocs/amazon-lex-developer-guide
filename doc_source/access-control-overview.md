# Overview of Managing Access Permissions to Your Amazon Lex Resources<a name="access-control-overview"></a>

 Every AWS resource is owned by an AWS account, and permissions to create or access a resource are governed by permissions policies\. An account administrator can attach permissions policies to IAM identities \(that is, users, groups, and roles\), and some services \(such as AWS Lambda\) also support attaching permissions policies to resources\. 

**Note**  
 An *account administrator* \(or administrator user\) is a user with administrator privileges\. For more information, see [IAM Best Practices](http://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html) in the *IAM User Guide*\. 

 When granting permissions, you decide who is getting the permissions, the resources they get permissions for, and the specific actions that you want to allow on those resources\. 


+ [Amazon Lex Resources and Operations](#access-control-resources)
+ [Understanding Resource Ownership](#access-control-owner)
+ [Managing Access to Resources](#access-control-manage-access-intro)
+ [Specifying Policy Elements: Actions, Effects, and Principals](#access-control-specify-lex-actions)
+ [Specifying Conditions in a Policy](#specifying-conditions)

## Amazon Lex Resources and Operations<a name="access-control-resources"></a>

 In Amazon Lex, the primary resource is a *bot*\. Amazon Lex also supports additional resource types, the *intent*, the *slot type*, the *alias*, and the *bot channel association*\. Aliases and bot channel associations are referred to as *subresources*\. For Amazon Lex, you can create subresources only in the context of an existing bot\. 

 These resources and subresources have unique Amazon Resource Names \(ARNs\) associated with them as shown in the following table\. 


****  

| Resource Type | ARN Format | 
| --- | --- | 
| Bot version |  arn:aws:lex:region:account\-id:bot:bot\-name:version  | 
| Intent |  arn:aws:lex:region:account\-id:intent:intent\-name:version  | 
| Slot type |  arn:aws:lex:region:account\-id:slottype:slottype\-name:version  | 
| Bot alias |  arn:aws:lex:region:account\-id:bot:bot\-name:alias\-name  | 
| Bot channel |  arn:aws:lex:region:account\-id:bot\-channel:bot\-name:alias\-name:channel\-name  | 

 Amazon Lex provides a set of operations to work with Amazon Lex resources\. For a list of available operations, see Amazon Lex [Actions](API_Operations.md)\. 

## Understanding Resource Ownership<a name="access-control-owner"></a>

 The AWS account owns the resources that are created in the account, regardless of who created the resources\. Specifically, the resource owner is the AWS account of the [principal entity](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html) \(that is, the root account, an IAM user, or an IAM role\) that authenticates the resource creation request\. The following examples illustrate how this works: 

+  If you use the root account credentials of your AWS account to create a bot, your AWS account is the owner of the resource \(in Amazon Lex, the resource is the bot\)\. 

+  If you create an IAM user in your AWS account and grant permissions to create a bot to that user, the user can create a bot\. However, your AWS account, to which the user belongs, owns the bot resource\. 

+  If you create an IAM role in your AWS account with permissions to create a bot, anyone who can assume the role can create a bot\. Your AWS account, to which the role belongs, owns the bot resource\. 

## Managing Access to Resources<a name="access-control-manage-access-intro"></a>

A *permissions policy* describes who has access to what\. The following section explains the available options for creating permissions policies\.

**Note**  
This section discusses using IAM in the context of Amazon Lex\. It doesn't provide detailed information about the IAM service\. For complete IAM documentation, see [What Is IAM?](http://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) in the *IAM User Guide*\. For information about IAM policy syntax and descriptions, see [AWS IAM Policy Reference](http://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html) in the *IAM User Guide*\.

Policies attached to an IAM identity are referred to as *identity\-based* policies \(IAM policies\) and policies attached to a resource are referred to as *resource\-based* policies\. Amazon Lex supports only identity\-based policies \(IAM policies\)\. 


+ [Identity\-Based Policies \(IAM Policies\)](#access-control-manage-access-intro-iam-policies)
+ [Resource\-Based Policies](#access-control-manage-access-intro-resource-policies)

### Identity\-Based Policies \(IAM Policies\)<a name="access-control-manage-access-intro-iam-policies"></a>

You can attach policies to IAM identities\. For example, you can do the following:

+ **Attach a permissions policy to a user or a group in your account** – To grant a user or a group of users permissions to create a Amazon Lex resource, such as a bot, you can attach a permissions policy to a user or group that the user belongs to\.

+ **Attach a permissions policy to a role \(grant cross\-account permissions\)** – To grant cross\-account permissions, you can attach an identity\-based permissions policy to an IAM role\. For example, the administrator in Account A can create a role to grant cross\-account permissions to another AWS account \(for example, Account B\) or an AWS service as follows:

  1. Account A administrator creates an IAM role and attaches a permissions policy to the role that grants permissions on resources in Account A\.

  1. Account A administrator attaches a trust policy to the role identifying Account B as the principal who can assume the role\. 

  1. Account B administrator can then delegate permissions to assume the role to any users in Account B\. Doing this allows users in Account B to create or access resources in Account A\. If you want to grant an AWS service permissions to assume the role, the principal in the trust policy can also be an AWS service principal\.

  For more information about using IAM to delegate permissions, see [Access Management](http://docs.aws.amazon.com/IAM/latest/UserGuide/access.html) in the *IAM User Guide*\.

The following is an example policy that allows the user to perform the `PutBot` action for your AWS account\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "lex:PutBot"],
            "Resource": [
                "*"
            ]
        }
    ]
}
```

For more information about using identity\-based policies with Amazon Lex, see [Using Identity\-Based Policies \(IAM Policies\) for Amazon Lex](access-control-managing-permissions.md)\. For more information about users, groups, roles, and permissions, see [Identities \(Users, Groups, and Roles\)](http://docs.aws.amazon.com/IAM/latest/UserGuide/id.html) in the *IAM User Guide*\. 

### Resource\-Based Policies<a name="access-control-manage-access-intro-resource-policies"></a>

Other services, such as Lambda, support resource\-based permissions policies\. For example, you can attach a policy to an S3 bucket to manage access permissions to that bucket\. Amazon Lex doesn't support resource\-based policies\. However, it does *use* resource\-based policies to access Lambda and Amazon Polly services\. 

## Specifying Policy Elements: Actions, Effects, and Principals<a name="access-control-specify-lex-actions"></a>

For each Amazon Lex resource \(see [Amazon Lex Resources and Operations](#access-control-resources)\), the service defines a set of API operations \(see [Actions](API_Operations.md)\)\. To grant permissions for these API operations, Amazon Lex defines a set of actions that you can specify in a policy\. For example, for the Amazon Lex Intent resource, the following actions are defined: `CreateIntent` and `CreateIntentVersion`\. Performing an API operation can require permissions for more than one action\.

The following are the most basic policy elements:

+ **Resource** – In a policy, you use an Amazon Resource Name \(ARN\) to identify the resource to which the policy applies\. For more information, see [Amazon Lex Resources and Operations](#access-control-resources)\.

+ **Action** – You use action keywords to identify resource operations that you want to allow or deny\. For example, depending on the specified `Effect`, `lex:bBot` either allows or denies the user permissions to perform the Amazon Lex `CreateBot` operation\.

+ **Effect** – You specify the effect of the action that occurs when the user requests the specific action—this can be either allow or deny\. If you don't explicitly grant access to \(allow\) a resource, access is implicitly denied\. You can also explicitly deny access to a resource\. You might do this to make sure that a user cannot access the resource, even if a different policy grants access\.

+ **Principal** – In identity\-based policies \(IAM policies\), the user that the policy is attached to is the implicit principal\. For resource\-based policies, you specify the user, account, service, or other entity that you want to receive permissions\. This applies to resource\-based policies only\. Amazon Lex doesn't support resource\-based policies\.

To learn more about IAM policy syntax and descriptions, see [AWS IAM Policy Reference](http://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html) in the *IAM User Guide*\.

For a table showing all of the Amazon Lex API actions, see [Amazon Lex API Permissions: Actions, Resources, and Conditions Reference](lex-api-permissions-ref.md)\.

## Specifying Conditions in a Policy<a name="specifying-conditions"></a>

When you grant permissions, you use the IAM policy language to specify the conditions under which a policy should take effect\. For example, you might want a policy to be applied only after a specific date\. For more information about specifying conditions in a policy language, see [Condition](http://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#Condition) in the *IAM User Guide*\. 

AWS provides a set of predefined condition keys for all AWS services that support IAM for access control\. For example, you can use the `aws:userid` condition key to require a specific AWS ID when requesting an action\. For more information and a complete list of AWS\-wide keys, see [Available Keys for Conditions](http://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#AvailableKeys) in the *IAM User Guide*\. 

**Note**  
Condition keys are case sensitive\.

Amazon Lex provides additional condition keys that you can include in `Condition` elements in an IAM permissions policy\. The following table shows the Amazon Lex condition keys that apply to Amazon Lex resources\.


**Amazon Lex Policy Condition Keys**  

| Amazon Lex Condition Key | Description | Value Type | Permission | 
| --- | --- | --- | --- | 
| lex:associatedIntents | Scopes the set of intents that can be used when creating or modifying the definition of a bot\. | Array of strings | `lex:PutBot` | 
| lex:associatedSlotTypes | Scopes the set of slot types that can be used when creating or modifying the definition of a slot type\. | Array of strings | `lex:PutIntent` | 
| lex:ChannelType | Scopes the type of bot channel association that a user can create, get, or delete\.  | String | `lex:CreateBotChannelAssociation` `lex:DeleteBotChannelAssociation` `lex:GetBotChannelAssociation` | 

### Example Policy: Using Condition Keys<a name="specifying-conditions-example-policies"></a>

The following example shows how to use condition keys in Amazon Lex IAM permissions policies\.

#### Example 1: Grant Permission to Create Bots Using the OrderPizza Intent<a name="specifying-conditions-example-policies-example-1"></a>

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "lex:PutBot"
            "Resource": [
                " *"
            ],
            "Condition": {
                "ForAllValues:StringLike": {
                    "lex:associatedIntents": [
                        "OrderPizza"
                    ]
                }
            }
        }
    ]
}
```