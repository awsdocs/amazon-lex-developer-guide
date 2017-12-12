# BotMetadata<a name="API_BotMetadata"></a>

Provides information about a bot\. \.

## Contents<a name="API_BotMetadata_Contents"></a>

 **createdDate**   
The date that the bot was created\.  
Type: Timestamp  
Required: No

 **description**   
A description of the bot\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 200\.  
Required: No

 **lastUpdatedDate**   
The date that the bot was updated\. When you create a bot, the creation date and last updated date are the same\.   
Type: Timestamp  
Required: No

 **name**   
The name of the bot\.   
Type: String  
Length Constraints: Minimum length of 2\. Maximum length of 50\.  
Pattern: `^([A-Za-z]_?)+$`   
Required: No

 **status**   
The status of the bot\.  
Type: String  
Valid Values:` BUILDING | READY | FAILED | NOT_BUILT`   
Required: No

 **version**   
The version of the bot\. For a new bot, the version is always `$LATEST`\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `\$LATEST|[0-9]+`   
Required: No

## See Also<a name="API_BotMetadata_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:

+  [AWS SDK for C\+\+](http://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/BotMetadata) 

+  [AWS SDK for Go](http://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/BotMetadata) 

+  [AWS SDK for Java](http://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/BotMetadata) 

+  [AWS SDK for Ruby V2](http://docs.aws.amazon.com/goto/SdkForRubyV2/lex-models-2017-04-19/BotMetadata) 