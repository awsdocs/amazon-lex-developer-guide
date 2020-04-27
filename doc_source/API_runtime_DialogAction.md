# DialogAction<a name="API_runtime_DialogAction"></a>

Describes the next action that the bot should take in its interaction with the user and provides information about the context in which the action takes place\. Use the `DialogAction` data type to set the interaction to a specific state, or to return the interaction to a previous state\.

## Contents<a name="API_runtime_DialogAction_Contents"></a>

 **fulfillmentState**   <a name="lex-Type-runtime_DialogAction-fulfillmentState"></a>
The fulfillment state of the intent\. The possible values are:  
+  `Failed` \- The Lambda function associated with the intent failed to fulfill the intent\.
+  `Fulfilled` \- The intent has fulfilled by the Lambda function associated with the intent\. 
+  `ReadyForFulfillment` \- All of the information necessary for the intent is present and the intent ready to be fulfilled by the client application\.
Type: String  
Valid Values:` Fulfilled | Failed | ReadyForFulfillment`   
Required: No

 **intentName**   <a name="lex-Type-runtime_DialogAction-intentName"></a>
The name of the intent\.  
Type: String  
Required: No

 **message**   <a name="lex-Type-runtime_DialogAction-message"></a>
The message that should be shown to the user\. If you don't specify a message, Amazon Lex will use the message configured for the intent\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1024\.  
Required: No

 **messageFormat**   <a name="lex-Type-runtime_DialogAction-messageFormat"></a>
+  `PlainText` \- The message contains plain UTF\-8 text\.
+  `CustomPayload` \- The message is a custom format for the client\.
+  `SSML` \- The message contains text formatted for voice output\.
+  `Composite` \- The message contains an escaped JSON object containing one or more messages\. For more information, see [Message Groups](https://docs.aws.amazon.com/lex/latest/dg/howitworks-manage-prompts.html)\. 
Type: String  
Valid Values:` PlainText | CustomPayload | SSML | Composite`   
Required: No

 **slots**   <a name="lex-Type-runtime_DialogAction-slots"></a>
Map of the slots that have been gathered and their values\.   
Type: String to string map  
Required: No

 **slotToElicit**   <a name="lex-Type-runtime_DialogAction-slotToElicit"></a>
The name of the slot that should be elicited from the user\.  
Type: String  
Required: No

 **type**   <a name="lex-Type-runtime_DialogAction-type"></a>
The next action that the bot should take in its interaction with the user\. The possible values are:  
+  `ConfirmIntent` \- The next action is asking the user if the intent is complete and ready to be fulfilled\. This is a yes/no question such as "Place the order?"
+  `Close` \- Indicates that the there will not be a response from the user\. For example, the statement "Your order has been placed" does not require a response\.
+  `Delegate` \- The next action is determined by Amazon Lex\.
+  `ElicitIntent` \- The next action is to determine the intent that the user wants to fulfill\.
+  `ElicitSlot` \- The next action is to elicit a slot value from the user\.
Type: String  
Valid Values:` ElicitIntent | ConfirmIntent | ElicitSlot | Close | Delegate`   
Required: Yes

## See Also<a name="API_runtime_DialogAction_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/runtime.lex-2016-11-28/DialogAction) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/runtime.lex-2016-11-28/DialogAction) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/runtime.lex-2016-11-28/DialogAction) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/runtime.lex-2016-11-28/DialogAction) 