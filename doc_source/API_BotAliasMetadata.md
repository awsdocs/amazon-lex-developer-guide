# BotAliasMetadata<a name="API_BotAliasMetadata"></a>

Provides information about a bot alias\.

## Contents<a name="API_BotAliasMetadata_Contents"></a>

 **botName**   <a name="lex-Type-BotAliasMetadata-botName"></a>
The name of the bot to which the alias points\.  
Type: String  
Length Constraints: Minimum length of 2\. Maximum length of 50\.  
Pattern: `^([A-Za-z]_?)+$`   
Required: No

 **botVersion**   <a name="lex-Type-BotAliasMetadata-botVersion"></a>
The version of the Amazon Lex bot to which the alias points\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `\$LATEST|[0-9]+`   
Required: No

 **checksum**   <a name="lex-Type-BotAliasMetadata-checksum"></a>
Checksum of the bot alias\.  
Type: String  
Required: No

 **conversationLogs**   <a name="lex-Type-BotAliasMetadata-conversationLogs"></a>
Settings that determine how Amazon Lex uses conversation logs for the alias\.  
Type: [ConversationLogsResponse](API_ConversationLogsResponse.md) object  
Required: No

 **createdDate**   <a name="lex-Type-BotAliasMetadata-createdDate"></a>
The date that the bot alias was created\.  
Type: Timestamp  
Required: No

 **description**   <a name="lex-Type-BotAliasMetadata-description"></a>
A description of the bot alias\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 200\.  
Required: No

 **lastUpdatedDate**   <a name="lex-Type-BotAliasMetadata-lastUpdatedDate"></a>
The date that the bot alias was updated\. When you create a resource, the creation date and last updated date are the same\.  
Type: Timestamp  
Required: No

 **name**   <a name="lex-Type-BotAliasMetadata-name"></a>
The name of the bot alias\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$`   
Required: No

## See Also<a name="API_BotAliasMetadata_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/BotAliasMetadata) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/BotAliasMetadata) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/BotAliasMetadata) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/BotAliasMetadata) 