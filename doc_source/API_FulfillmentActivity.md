# FulfillmentActivity<a name="API_FulfillmentActivity"></a>

 Describes how the intent is fulfilled after the user provides all of the information required for the intent\. You can provide a Lambda function to process the intent, or you can return the intent information to the client application\. We recommend that you use a Lambda function so that the relevant logic lives in the Cloud and limit the client\-side code primarily to presentation\. If you need to update the logic, you only update the Lambda function; you don't need to upgrade your client application\. 

Consider the following examples:
+ In a pizza ordering application, after the user provides all of the information for placing an order, you use a Lambda function to place an order with a pizzeria\. 
+ In a gaming application, when a user says "pick up a rock," this information must go back to the client application so that it can perform the operation and update the graphics\. In this case, you want Amazon Lex to return the intent data to the client\. 

## Contents<a name="API_FulfillmentActivity_Contents"></a>

 **codeHook**   <a name="lex-Type-FulfillmentActivity-codeHook"></a>
 A description of the Lambda function that is run to fulfill the intent\.   
Type: [CodeHook](API_CodeHook.md) object  
Required: No

 **type**   <a name="lex-Type-FulfillmentActivity-type"></a>
 How the intent should be fulfilled, either by running a Lambda function or by returning the slot data to the client application\.   
Type: String  
Valid Values:` ReturnIntent | CodeHook`   
Required: Yes

## See Also<a name="API_FulfillmentActivity_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/FulfillmentActivity) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/FulfillmentActivity) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/FulfillmentActivity) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/FulfillmentActivity) 