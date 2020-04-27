# Tagging Your Amazon Lex Resources<a name="how-it-works-tags"></a>

To help you manage your Amazon Lex bots, bot aliases, and bot channels, you can assign metadata to each resource as *tags\.* A tag is a label that you assign to an AWS resource\. Each tag consists of a key and a value\.

Tags enable you to categorize your AWS resources in different ways, for example, by purpose, owner, or application\. Tags help you to:
+ Identify and organize your AWS resources\. Many AWS resources support tagging, so you can assign the same tag to resources in different services to indicate that the resources are related\. For example, you can tag a bot and the Lambda functions that it uses with the same tag\.
+ Allocate costs\. You activate tags on the AWS Billing and Cost Management dashboard\. AWS uses the tags to categorize your costs and deliver a monthly cost allocation report to you\. For Amazon Lex, you can allocate costs for each alias using tags specific to the alias, except for the `$LATEST` alias\. You allocate costs for the `$LATEST` alias using tags for your Amazon Lex bot\. For more information, see [ Use Cost Allocation Tags ](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/cost-alloc-tags.html) in the *AWS Billing and Cost Management User Guide*\.
+ Control access to your resources\. You can use tags to Amazon Lex to create policies to control access to Amazon Lex resources\. These policies can be attached to an IAM role or user to enable tag\-based access control\. For more information, see [Authorization Based on Amazon Lex Tags](security_iam_service-with-iam.md#security_iam_service-with-iam-tags)\. To view an example identity\-based policy for limiting access to a resource based on the tags on that resource, see [Example: Use a Tag to Access a Resource](security_iam_id-based-policy-examples.md#security_iam_id-based-policy-examples-tag)\. 

You can work with tags using the AWS Management Console, the AWS Command Line Interface, or the Amazon Lex API\.

## Tagging Your Resources<a name="tagging-resources"></a>

If you are using the Amazon Lex console, you can tag resources when you create them, or you can add the tags later\. You can also use the console to update or remove existing tags\. 

If you are using the AWS CLI or the Amazon Lex API, you use the following operations to manage tags for your resources:
+  [ListTagsForResource](API_ListTagsForResource.md) – view the tags associated with a resource\.
+ [PutBot](API_PutBot.md) and [PutBotAlias](API_PutBotAlias.md) – apply tags when you create a bot or a bot alias\.
+  [TagResource](API_TagResource.md) – add and modify tags on an existing resource\.
+  [UntagResource](API_UntagResource.md) – remove tags from a resource\. 

The following resources in Amazon Lex support tagging:
+ Bots \- use an Amazon Resource Name \(ARN\) like the following:
  + `arn:${partition}:lex:${region}:${account}:bot:${bot-name}`
+ Bot aliases \- use an ARN like the following:
  + `arn:${partition}:lex:${region}:${account}:bot:${bot-name}:${bot-alias}`
+ Bot channels \- use an ARN like the following:
  + `arn:${partition}:lex:${region}:${account}:bot-channel:${bot-name}:${bot-alias}:${channel-name}`

## Tag Restrictions<a name="tags-restrictions"></a>

The following basic restrictions apply to tags on Amazon Lex resources:
+ Maximum number of tags \- 50
+ Maximum key length – 128 characters
+ Maximum value length – 256 characters
+ Valid characters for key and value – a–z, A–Z, 0–9, space, and the following characters: \_ \. : / = \+ \- and @
+ Keys and values are case sensitive\.
+ Don't use `aws:` as a prefix for keys; it's reserved for AWS use\.