# BotAliasMetadata<a name="API_BotAliasMetadata"></a>

Provides information about a bot alias\.

## Contents<a name="API_BotAliasMetadata_Contents"></a>

 **botName**   
The name of the bot to which the alias points\.  
Type: String  
Length Constraints: Minimum length of 2\. Maximum length of 50\.  
Pattern: `^([A-Za-z]_?)+$`   
Required: No

 **botVersion**   
The version of the Amazon Lex bot to which the alias points\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `\$LATEST|[0-9]+`   
Required: No

 **checksum**   
Checksum of the bot alias\.  
Type: String  
Required: No

 **createdDate**   
The date that the bot alias was created\.  
Type: Timestamp  
Required: No

 **description**   
A description of the bot alias\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 200\.  
Required: No

 **lastUpdatedDate**   
The date that the bot alias was updated\. When you create a resource, the creation date and last updated date are the same\.  
Type: Timestamp  
Required: No

 **name**   
The name of the bot alias\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$`   
Required: No

## See Also<a name="API_BotAliasMetadata_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:

+  [AWS SDK for C\+\+](http://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/BotAliasMetadata) 

+  [AWS SDK for Go](http://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/BotAliasMetadata) 

+  [AWS SDK for Java](http://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/BotAliasMetadata) 

+  [AWS SDK for Ruby V2](http://docs.aws.amazon.com/goto/SdkForRubyV2/lex-models-2017-04-19/BotAliasMetadata) 