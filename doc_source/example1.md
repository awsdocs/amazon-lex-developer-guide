# Deploying an Amazon Lex Bot on a Messaging Platform<a name="example1"></a>

This section explains how to deploy Amazon Lex bots on the Facebook, Slack, and Twilio messaging platforms\. 

**Note**  
When storing your Facebook, Slack, or Twilio configurations, Amazon Lex uses AWS Key Management Service customer master keys \(CMK\) to encrypt the information\. The first time that you create a channel to one of these messaging platforms, Amazon Lex creates a default CMK \(`aws/lex`\)\. Alternatively, you can create your own CMK with AWS KMS\. This gives you more flexibility, including the ability to create, rotate, and disable keys\. You can also define access controls and audit the encryption keys used to protect your data\. For more information, see the [AWS Key Management Service Developer Guide](http://docs.aws.amazon.com/kms/latest/developerguide/)\.

When a messaging platform sends a request to Amazon Lex it includes platform\-specific information as a request attribute to your Lambda function\. Use these attributes to customize the way that your bot behaves\. For more information, see [Setting Request Attributes](context-mgmt.md#context-mgmt-request-attribs)\.

All of the attributes take the namespace, `x-amz-lex:`, as the prefix \. For example, the `user-id` attribute is called `x-amz-lex:user-id`\. There are common attributes that are sent by all messaging platforms in addition to attributes that are specific to a particular platform\. The following tables list the request attributes that messaging platforms send to your bot's Lambda function\.


**Common Request Attributes**  

| Attribute | Description | 
| --- | --- | 
| channel\-id | The channel endpoint identifier from Amazon Lex\. | 
| channel\-name | The channel name from Amazon Lex\. | 
| channel\-type |  One of the following values: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lex/latest/dg/example1.html)  | 
| webhook\-endpoint\-url | The Amazon Lex endpoint for the channel\. | 


**Facebook Request Attributes**  

| Attribute | Description | 
| --- | --- | 
| user\-id | The Facebook identifier of the sender\. See [https://developers\.facebook\.com/docs/messenger\-platform/webhook\-reference/message\-received](https://developers.facebook.com/docs/messenger-platform/webhook-reference/message-received)\. | 
| facebook\-page\-id | The Facebook page identifier of the recipient\. See [https://developers\.facebook\.com/docs/messenger\-platform/webhook\-reference/message\-received](https://developers.facebook.com/docs/messenger-platform/webhook-reference/message-received)\. | 


**Kik Request Attributes**  

| Attribute | Description | 
| --- | --- | 
| kik\-chat\-id | The identifier for the conversation that your bot is involved in\. For more information, see [https://dev\.kik\.com/\#/docs/messaging\#message\-formats](https://dev.kik.com/#/docs/messaging#message-formats)\. | 
| kik\-chat\-type | The type of conversation that the message originated from\. For more information, see [https://dev\.kik\.com/\#/docs/messaging\#message\-formats](https://dev.kik.com/#/docs/messaging#message-formats)\. | 
| kik\-message\-id | A UUID the identifies the message\. For more information, see [https://dev\.kik\.com/\#/docs/messaging\#message\-formats](https://dev.kik.com/#/docs/messaging#message-formats)\. | 
| kik\-message\-type | The type of message\. For more information, see [https://dev\.kik\.com/\#/docs/messaging\#message\-types](https://dev.kik.com/#/docs/messaging#message-types)\. | 


**Twilio Request Attributes**  

| Attribute | Description | 
| --- | --- | 
| user\-id | The sender's phone number \("From"\)\. See [https://www\.twilio\.com/docs/api/rest/message](https://www.twilio.com/docs/api/rest/message)\. | 
| twilio\-target\-phone\-number | The phone number of the recipient \("To"\)\. See [https://www\.twilio\.com/docs/api/rest/message](https://www.twilio.com/docs/api/rest/message)\. | 


**Slack Request Attributes**  

| Attribute | Description | 
| --- | --- | 
| user\-id | The Slack user identifier\. See [https://api\.slack\.com/types/user](https://api.slack.com/types/user)\. | 
| slack\-team\-id | The identifier of the team that sent the message\. See [https://api\.slack\.com/methods/team\.info](https://api.slack.com/methods/team.info)\. | 
| slack\-bot\-token | The developer token that gives the bot access to the Slack APIs\. See [https://api\.slack\.com/docs/token\-types](https://api.slack.com/docs/token-types)\. | 