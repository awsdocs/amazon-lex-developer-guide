# How Amazon Lex Works with IAM<a name="security_iam_service-with-iam"></a>

Before you use AWS Identity and Access Management \(IAM\) to manage access to Amazon Lex, you should understand which IAM features are available to use with Amazon Lex\. For a high\-level view of how Amazon Lex and other AWS services work with IAM, see [AWS Services That Work with IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_aws-services-that-work-with-iam.html) in the *IAM User Guide*\.

**Topics**
+ [Amazon Lex Identity\-Based Policies](#security_iam_service-with-iam-id-based-policies)
+ [Amazon Lex Resource\-Based Policies](#security_iam_service-with-iam-resource-based-policies)
+ [Authorization Based on Amazon Lex Tags](#security_iam_service-with-iam-tags)
+ [Amazon Lex IAM Roles](#security_iam_service-with-iam-roles)

## Amazon Lex Identity\-Based Policies<a name="security_iam_service-with-iam-id-based-policies"></a>

To specify allowed or denied actions and resources and the conditions under which actions are allowed or denied, use IAM identity\-based policies,\. Amazon Lex supports specific actions, resources, and condition keys\. To learn about all of the elements that you use in a JSON policy, see [IAM JSON Policy Elements Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html) in the *IAM User Guide*\.

### Actions<a name="security_iam_service-with-iam-id-based-policies-actions"></a>

The `Action` element of an IAM identity\-based policy describes the specific action or actions that will be allowed or denied by the policy\. Policy actions usually have the same name as the associated AWS API operation\. The action is used in a policy to grant permissions to perform the associated operation\. 

In Amazon Lex, policy actions use the following prefix before the action: `lex:`\. For example, to grant someone permission to call an Amazon Lex bot with the `PostContent` operation, you include the `lex:PostContent` action in their policy\. Policy statements must include either an `Action` or `NotAction` element\. Amazon Lex defines actions that describe the tasks that you can perform with this service\. To see a list of Amazon Lex actions, see [Actions Defined by Amazon Lex](https://docs.aws.amazon.com/IAM/latest/UserGuide/list_amazonlex.html#amazonlex-actions-as-permissions) in the *IAM User Guide*\.

To specify multiple actions in a single statement, separate them with commas as follows\.

```
"Action": [
      "lex:action1",
      "lex:action2"
```

You can specify multiple actions using wildcards \(\*\)\. For example, to specify all actions that begin with the word `Put`, include the following action\.

```
"Action": "lex:Put*"
```



### Resources<a name="security_iam_service-with-iam-id-based-policies-resources"></a>

The `Resource` element specifies the object or objects to which the action applies\. Statements must include either a `Resource` or a `NotResource` element\. You specify a resource using an ARN or, to indicate that the statement applies to all resources, the wildcard \(\*\)\.



An Amazon Lex bot resource ARN has the following format\.

```
arn:aws:lex:${Region}:${Account}:bot:${Bot-Name}
```

For more information about the format of ARNs, see [Amazon Resource Names \(ARNs\) and AWS Service Namespaces](https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html)\.

For example, to specify the `OrderFlowers` bot in your statement, use the following ARN\.

```
"Resource": "arn:aws:lex:us-east-2:123456789012:bot:OrderFlowers"
```

To specify all bots that belong to a specific account, use the wildcard \(\*\)\.

```
"Resource": "arn:aws:lex:us-east-2:123456789012:bot:*"
```

Some Amazon Lex actions, such as those for creating resources, can't be performed on a specific resource\. In those cases, you must use the wildcard, \(\*\)\.

```
"Resource": "*"
```

For a list of Amazon Lex resource types and their ARNs, see [Resources Defined by Amazon Lex](https://docs.aws.amazon.com/IAM/latest/UserGuide/list_amazonlex.html#amazonlex-resources-for-iam-policies) in the *IAM User Guide*\. To learn with which actions you can specify the ARN of each resource, see [Actions Defined by Amazon Lex](https://docs.aws.amazon.com/IAM/latest/UserGuide/list_amazonlex.html#amazonlex-actions-as-permissions)\.

### Condition Keys<a name="security_iam_service-with-iam-id-based-policies-conditionkeys"></a>

Use the `Condition` element \(or a `Condition` *block*\) to specify conditions in which a statement is in effect\. The `Condition` element is optional\. You can build conditional expressions that use [condition operators](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_condition_operators.html), such as equals or less than, to match the condition in the policy with values in the request\. 

If you specify multiple `Condition` elements in a statement, or multiple keys in a single `Condition` element, AWS evaluates them using a logical `AND` operation\. If you specify multiple values for a single condition key, AWS evaluates the condition using a logical `OR` operation\. All of the conditions must be met before the statement's permissions are granted\.

You can also use placeholder variables when you specify conditions\. For example, you can grant an IAM user permission to access a resource only if it is tagged with their IAM user name\. For more information, see [IAM Policy Elements: Variables and Tags](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_variables.html) in the *IAM User Guide*\. 

Amazon Lex defines its own set of condition keys and also supports using some global condition keys\. For a list of all AWS global condition keys, see [AWS Global Condition Context Keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html) in the *IAM User Guide*\.



The following table lists the Amazon Lex condition keys that apply to Amazon Lex resources\. You can include these keys in `Condition` elements in an IAM permissions policy\. 


****  

| Amazon Lex Condition Key | Description | Value Type | Permission | 
| --- | --- | --- | --- | 
| lex:associatedIntents |  Scopes the set of intents that can be used when creating or modifying the definition of a bot\.  |  Array of strings  |  `lex:PutBot`  | 
| lex:associatedSlotTypes |  Scopes the set of slot types that can be used when creating or modifying the definition of a slot type\.  |  Array of strings  |  `lex:PutIntent`  | 
| lex:ChannelType |  Scopes the type of bot channel association that a user can create, get, or delete\.   |  String  |  `lex:CreateBotChannelAssociation` `lex:DeleteBotChannelAssociation` `lex:GetBotChannelAssociation`  | 

### Examples<a name="security_iam_service-with-iam-id-based-policies-examples"></a>



For examples of Amazon Lex identity\-based policies, see [Amazon Lex Identity\-Based Policy Examples](security_iam_id-based-policy-examples.md)\.

## Amazon Lex Resource\-Based Policies<a name="security_iam_service-with-iam-resource-based-policies"></a>

Resource\-based policies are JSON policy documents that specify what actions a specified principal can perform on the Amazon Lex resource and under what conditions\. Amazon Lex supports resource\-based permissions policies for bots, intents, and slot types\. Use resource\-based policies to grant usage permission to other accounts on a per\-resource basis\. You can also use a resource\-based policy to allow an AWS service to access your Amazon Lex resources\.

To enable cross\-account access, you can specify an entire account or you can specify IAM entities in another account as the [principal in a resource\-based policy](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_principal.html)\. Adding a cross\-account principal to a resource\-based policy is only the first step in establishing the trust relationship\. When the principal and the resource are in different AWS accounts, you must also grant the principal entity permission to access the resource\. Grant permission by attaching an identity\-based policy to the entity\. However, if a resource\-based policy grants access to a principal in the same account, no additional identity\-based policy is required\. For more information, see [How IAM Roles Differ from Resource\-based Policies ](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_compare-resource-policies.html)in the *IAM User Guide*\.

### Examples<a name="security_iam_service-with-iam-resource-based-policies-examples"></a>



For examples of Amazon Lex resource\-based policies, see [Amazon Lex Resource\-Based Policy Example](security_iam_resource-based-policy-examples.md),

## Authorization Based on Amazon Lex Tags<a name="security_iam_service-with-iam-tags"></a>

You can associate tags with certain types of Amazon Lex resources for authorization\. To control access based on tags, provide tag information in the condition element of a policy by using the `lex:ResourceTag/${TagKey}`, `aws:RequestTag/${TagKey}`, or `aws:TagKeys` condition keys\.

For information about tagging Amazon Lex resources, see [Tagging Your Amazon Lex Resources](how-it-works-tags.md)\. For an example identity\-based policy that limits access to a resource based on the resource tags, see [Example: Use a Tag to Access a Resource](security_iam_id-based-policy-examples.md#security_iam_id-based-policy-examples-tag)\. For more information about using tags to limit access to resources, see [Controlling Access Using Tags](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_tags.html) in the *IAM User Guide*\. 

The following table lists the actions and corresponding resource types for tag\-based access control\. Each action is authorized based on the tags associated with the corresponding resource type\.


| Action | Resource type | Condition keys | Notes | 
| --- | --- | --- | --- | 
| [CreateBotVersion](API_CreateBotVersion.md) | bot | lex:ResourceTag |   | 
| [DeleteBot](API_DeleteBot.md) | bot | lex:ResourceTag |   | 
| [DeleteBotAlias](API_DeleteBotAlias.md) | alias | lex:ResourceTag |   | 
| [DeleteBotChannelAssociation](API_DeleteBotChannelAssociation.md) | channel | lex:ResourceTag |   | 
| [DeleteBotVersion](API_DeleteBotVersion.md) | bot | lex:ResourceTag |   | 
| [DeleteSession](API_runtime_DeleteSession.md) | bot or alias | lex:ResourceTag | Uses tags associated with the bot when alias is set to $LATEST\. Uses tags associated with the specified alias when used with other aliases\. | 
| [DeleteUtterances](API_DeleteUtterances.md) | bot | lex:ResourceTag |   | 
| [GetBot](API_GetBot.md) | bot or alias | lex:ResourceTag | Uses tags associated with the bot when versionOrAlias is set to $LATEST or numeric version\. Uses tags associated with the specified alias when used with aliases | 
| [GetBotAlias](API_GetBotAlias.md) | alias | lex:ResourceTag |   | 
| [GetBotChannelAssociation](API_GetBotChannelAssociation.md) | chanel | lex:ResourceTag |   | 
| [GetBotChannelAssociations](API_GetBotChannelAssociations.md) | chanel | lex:ResourceTag | Uses tags associated with the bot when alias is set to "\-"\. Uses tags associated with the specified alias when a bot alias is specified | 
| [GetBotVersions](API_GetBotVersions.md) | bot | lex:ResourceTag |   | 
| [GetExport](API_GetExport.md) | bot | lex:ResourceTag |   | 
| [GetSession](API_runtime_GetSession.md) | bot or alias | lex:ResourceTag | Uses tags associated with the bot when alias is set to $LATEST\. Uses tags associated with the specified alias when used with other aliases\. | 
| [GetUtterancesView](API_GetUtterancesView.md) | bot | lex:ResourceTag |   | 
| [ListTagsForResource](API_ListTagsForResource.md) | bot, alias, or channel | lex:ResourceTag |   | 
| [PostContent](API_runtime_PostContent.md) | bot or alias | lex:ResourceTag | Uses tags associated with the bot when alias is set to $LATEST\. Uses tags associated with the specified alias when used with other aliases\. | 
| [PostText](API_runtime_PostText.md) | bot or alias | lex:ResourceTag | Uses tags associated with the bot when alias is set to $LATEST\. Uses tags associated with the specified alias when used with other aliases\. | 
| [PutBot](API_PutBot.md) | bot | lex:ResourceTag, aws:RequestTag, aws:TagKeys |   | 
| [PutBotAlias](API_PutBotAlias.md) | alias | lex:ResourceTag, aws:RequestTag, aws:TagKeys |   | 
| [PutSession](API_runtime_PutSession.md) | bot or alias | lex:ResourceTag | Uses tags associated with the bot when alias is set to $LATEST\. Uses tags associated with the specified alias when used with other aliases\. | 
| [StartImport](API_StartImport.md) | bot | lex:ResourceTag | Relies on access policy for the PutBot operation\. Tags and permissions specific to the StartImport operation are ignored\. | 
| [TagResource](API_TagResource.md) | bot, alias, or channel | lex:ResourceTag, aws:RequestTag, aws:TagKeys |   | 
| [UntagResource](API_UntagResource.md) | bot, alias, or channel | lex:ResourceTag, aws:RequestTag, aws:TagKeys |   | 

## Amazon Lex IAM Roles<a name="security_iam_service-with-iam-roles"></a>

An [IAM role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html) is an entity within your AWS account that has specific permissions\.

### Using Temporary Credentials with Amazon Lex<a name="security_iam_service-with-iam-roles-tempcreds"></a>

You can use temporary credentials to sign in with federation, assume an IAM role, or to assume a cross\-account role\. You obtain temporary security credentials by calling AWS STS API operations such as [AssumeRole](https://docs.aws.amazon.com/STS/latest/APIReference/API_AssumeRole.html) or [GetFederationToken](https://docs.aws.amazon.com/STS/latest/APIReference/API_GetFederationToken.html)\. 

Amazon Lex supports using temporary credentials\. 

### Service\-Linked Roles<a name="security_iam_service-with-iam-roles-service-linked"></a>

[Service\-linked roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html#iam-term-service-linked-role) allow AWS services to access resources in other services to complete an action on your behalf\. Service\-linked roles appear in your IAM account and are owned by the service\. An IAM administrator can view, but not edit, the permissions for service\-linked roles\.

Amazon Lex supports service\-linked roles\. For details about creating or managing Amazon Lex service\-linked roles, see [Step 1: Create a Service\-Linked Role \(AWS CLI\)](gs-create-role.md)\.

### Service Roles<a name="security_iam_service-with-iam-roles-service"></a>

A service can assume a [service role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html#iam-term-service-role) on your behalf\. This role allows the service to access resources in other services to complete an action on your behalf\. Service roles appear in your IAM account and are owned by the account\. This means that an IAM administrator can change the permissions for this role\. However, doing so might prevent the service from functioning as expected\.

Amazon Lex supports service roles\. 

### Choosing an IAM Role in Amazon Lex<a name="security_iam_service-with-iam-roles-choose"></a>

Amazon Lex uses service\-linked roles to call Amazon Comprehend and Amazon Polly\. It uses resource\-level permissions on your AWS Lambda functions to invoke them\.

You must provide an IAM role to enable conversation tagging\. For more information, see [Creating an IAM Role and Policies for Conversation Logs](conversation-logs-policies.md#conversation-logs-role-and-policy)\.