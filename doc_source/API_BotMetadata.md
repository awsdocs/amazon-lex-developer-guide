# BotMetadata<a name="API_BotMetadata"></a>

Provides information about a bot\. \.

## Contents<a name="API_BotMetadata_Contents"></a>

 **createdDate**   <a name="lex-Type-BotMetadata-createdDate"></a>
The date that the bot was created\.  
Type: Timestamp  
Required: No

 **description**   <a name="lex-Type-BotMetadata-description"></a>
A description of the bot\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 200\.  
Required: No

 **lastUpdatedDate**   <a name="lex-Type-BotMetadata-lastUpdatedDate"></a>
The date that the bot was updated\. When you create a bot, the creation date and last updated date are the same\.   
Type: Timestamp  
Required: No

 **name**   <a name="lex-Type-BotMetadata-name"></a>
The name of the bot\.   
Type: String  
Length Constraints: Minimum length of 2\. Maximum length of 50\.  
Pattern: `^([A-Za-z]_?)+$`   
Required: No

 **status**   <a name="lex-Type-BotMetadata-status"></a>
The status of the bot\.  
Type: String  
Valid Values:` BUILDING | READY | READY_BASIC_TESTING | FAILED | NOT_BUILT`   
Required: No

 **version**   <a name="lex-Type-BotMetadata-version"></a>
The version of the bot\. For a new bot, the version is always `$LATEST`\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `\$LATEST|[0-9]+`   
Required: No

## See Also<a name="API_BotMetadata_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/BotMetadata) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/BotMetadata) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/BotMetadata) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/BotMetadata) 