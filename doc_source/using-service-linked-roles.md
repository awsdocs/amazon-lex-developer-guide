# Using Service\-Linked Roles for Amazon Lex<a name="using-service-linked-roles"></a>

Amazon Lex uses AWS Identity and Access Management \(IAM\)[ service\-linked roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html#iam-term-service-linked-role)\. A service\-linked role is a unique type of IAM role that is linked directly to Amazon Lex\. Service\-linked roles are predefined by Amazon Lex and include all the permissions that the service requires to call other AWS services on your behalf\. 

A service\-linked role makes setting up Amazon Lex easier because you don’t have to manually add the necessary permissions\. Amazon Lex defines the permissions of its service\-linked roles, and unless defined otherwise, only Amazon Lex can assume its roles\. The defined permissions include the trust policy and the permissions policy, and that permissions policy cannot be attached to any other IAM entity\.

You can delete a service\-linked role only after first deleting its related resources\. This protects your Amazon Lex resources because you can't inadvertently remove permission to access the resources\.

## Service\-Linked Roles Permissions for Amazon Lex<a name="slr-permissions"></a>

Amazon Lex uses two service linked roles:
+ **AWSServiceRoleForLexBots** – Amazon Lex uses this service\-linked role to invoke Amazon Polly to synthesize speech responses for your bot, to call Amazon Comprehend for sentiment analyisis, and optionally Amazon Kendra for searching indexes\.
+ **AWSServiceRoleForLexChannels** – Amazon Lex uses this service\-linked role to post text to your bot when managing channels\.

You must configure permissions to allow an IAM entity \(such as a user, group, or role\) to create, edit, or delete a service\-linked role\. For more information, see [Service\-Linked Role Permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#service-linked-role-permissions) in the *IAM User Guide*\.

## Creating a Service\-Linked Role for Amazon Lex<a name="create-slr"></a>

You don't need to manually create a service\-linked role\. When you create a bot, bot channel, or Amazon Kendra search intent in the AWS Management Console, Amazon Lex creates the service\-linked role for you\. 

If you delete this service\-linked role, and then need to create it again, you can use the same process to recreate the role in your account\. When you create a new bot, channel association, or Amazon Kendra search intent, Amazon Lex creates the service\-linked role for you again\. 

You can also use the AWS CLI to create a service\-linked role with the **AWSServiceRoleForLexBots** use case\. In the AWS CLI create a service\-linked role with the Amazon Lex service name\. For more information, see [Step 1: Create a Service\-Linked Role \(AWS CLI\)](gs-create-role.md)\. If you delete this service\-linked role, you can use this same process to create the role again\.

## Editing a Service\-Linked Role for Amazon Lex<a name="edit-slr"></a>

Amazon Lex does not allow you to edit Amazon Lex service\-linked roles\. After you create a service\-linked role, you cannot change the name of the role because various entities might reference the role\. However, you can edit the description of the role using IAM\. For more information, see [Editing a Service\-Linked Role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#edit-service-linked-role) in the *IAM User Guide*\.

## Deleting a Service\-Linked Role for Amazon Lex<a name="delete-slr"></a>

If you no longer need to use a feature or service that requires a service\-linked role, we recommend that you delete that role\. That way you don’t have an unused entity that is not actively monitored or maintained\. However, you must clean up the resources for your service\-linked role before you can manually delete it\.

**Note**  
If the Amazon Lex service is using the role when you try to delete the resources, then the deletion might fail\. If that happens, wait for a few minutes and try the operation again\.

**To delete Amazon Lex resources used by service\-linked roles:**

1.  Delete any bot channels that you are using\. 

1.  Delete any bots in your account\. 

 **To manually delete the service\-linked role using IAM** 

Use the IAM console, the AWS CLI, or the AWS API to delete the Amazon Lex service\-linked roles\. For more information, see [Deleting a Service\-Linked Role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#delete-service-linked-role) in the *IAM User Guide*\.

## Supported Regions for Amazon Lex Service\-Linked Roles<a name="slr-regions"></a>

Amazon Lex supports using service\-linked roles in all of the regions where the service is available\. For more information, see [Amazon Lex endpoints and quotas](https://docs.aws.amazon.com/general/latest/gr/lex.html)\.