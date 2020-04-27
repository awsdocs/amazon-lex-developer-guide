# LogSettingsRequest<a name="API_LogSettingsRequest"></a>

Settings used to configure delivery mode and destination for conversation logs\.

## Contents<a name="API_LogSettingsRequest_Contents"></a>

 **destination**   <a name="lex-Type-LogSettingsRequest-destination"></a>
Where the logs will be delivered\. Text logs are delivered to a CloudWatch Logs log group\. Audio logs are delivered to an S3 bucket\.  
Type: String  
Valid Values:` CLOUDWATCH_LOGS | S3`   
Required: Yes

 **kmsKeyArn**   <a name="lex-Type-LogSettingsRequest-kmsKeyArn"></a>
The Amazon Resource Name \(ARN\) of the AWS KMS customer managed key for encrypting audio logs delivered to an S3 bucket\. The key does not apply to CloudWatch Logs and is optional for S3 buckets\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 2048\.  
Pattern: `^arn:[\w\-]+:kms:[\w\-]+:[\d]{12}:(?:key\/[\w\-]+|alias\/[a-zA-Z0-9:\/_\-]{1,256})$`   
Required: No

 **logType**   <a name="lex-Type-LogSettingsRequest-logType"></a>
The type of logging to enable\. Text logs are delivered to a CloudWatch Logs log group\. Audio logs are delivered to an S3 bucket\.  
Type: String  
Valid Values:` AUDIO | TEXT`   
Required: Yes

 **resourceArn**   <a name="lex-Type-LogSettingsRequest-resourceArn"></a>
The Amazon Resource Name \(ARN\) of the CloudWatch Logs log group or S3 bucket where the logs should be delivered\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^arn:[\w\-]+:(?:logs:[\w\-]+:[\d]{12}:log-group:[\.\-_/#A-Za-z0-9]{1,512}(?::\*)?|s3:::[a-z0-9][\.\-a-z0-9]{1,61}[a-z0-9])$`   
Required: Yes

## See Also<a name="API_LogSettingsRequest_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/LogSettingsRequest) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/LogSettingsRequest) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/LogSettingsRequest) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/LogSettingsRequest) 