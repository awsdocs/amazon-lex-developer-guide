# Data Protection in Amazon Lex<a name="data-protection"></a>

Amazon Lex collects customer content for troubleshooting and to help improve the service\. Customer content is secured by default\. You can delete content for individual customers using the Amazon Lex API\.

Amazon Lex stores four types of content:
+ Sample utterances, which are used to build and train a bot
+ Customer utterances from users interacting with the bot
+ Session attributes, which provide application\-specific information for the duration of a user's interaction with a bot
+ Request attributes, which contain information that applies to a single request to a bot

Any Amazon Lex bot that is designed for use by children is governed by the Children's Online Privacy Protection Act \(COPPA\)\. You tell Amazon Lex that the bot is subject to COPPA by using the console or the Amazon Lex API to set the `childDirected` field to `true`\. When the `childDirected` field is set to `true`, no user utterances are stored\.

**Topics**
+ [Encryption at Rest](at-rest.md)
+ [Encryption in Transit](in-transit.md)
+ [Key Management](key-management.md)