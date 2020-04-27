# IntentSummary<a name="API_runtime_IntentSummary"></a>

Provides information about the state of an intent\. You can use this information to get the current state of an intent so that you can process the intent, or so that you can return the intent to its previous state\.

## Contents<a name="API_runtime_IntentSummary_Contents"></a>

 **checkpointLabel**   <a name="lex-Type-runtime_IntentSummary-checkpointLabel"></a>
A user\-defined label that identifies a particular intent\. You can use this label to return to a previous intent\.   
Use the `checkpointLabelFilter` parameter of the `GetSessionRequest` operation to filter the intents returned by the operation to those with only the specified label\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 255\.  
Pattern: `[a-zA-Z0-9-]+`   
Required: No

 **confirmationStatus**   <a name="lex-Type-runtime_IntentSummary-confirmationStatus"></a>
The status of the intent after the user responds to the confirmation prompt\. If the user confirms the intent, Amazon Lex sets this field to `Confirmed`\. If the user denies the intent, Amazon Lex sets this value to `Denied`\. The possible values are:  
+  `Confirmed` \- The user has responded "Yes" to the confirmation prompt, confirming that the intent is complete and that it is ready to be fulfilled\.
+  `Denied` \- The user has responded "No" to the confirmation prompt\.
+  `None` \- The user has never been prompted for confirmation; or, the user was prompted but did not confirm or deny the prompt\.
Type: String  
Valid Values:` None | Confirmed | Denied`   
Required: No

 **dialogActionType**   <a name="lex-Type-runtime_IntentSummary-dialogActionType"></a>
The next action that the bot should take in its interaction with the user\. The possible values are:  
+  `ConfirmIntent` \- The next action is asking the user if the intent is complete and ready to be fulfilled\. This is a yes/no question such as "Place the order?"
+  `Close` \- Indicates that the there will not be a response from the user\. For example, the statement "Your order has been placed" does not require a response\.
+  `ElicitIntent` \- The next action is to determine the intent that the user wants to fulfill\.
+  `ElicitSlot` \- The next action is to elicit a slot value from the user\.
Type: String  
Valid Values:` ElicitIntent | ConfirmIntent | ElicitSlot | Close | Delegate`   
Required: Yes

 **fulfillmentState**   <a name="lex-Type-runtime_IntentSummary-fulfillmentState"></a>
The fulfillment state of the intent\. The possible values are:  
+  `Failed` \- The Lambda function associated with the intent failed to fulfill the intent\.
+  `Fulfilled` \- The intent has fulfilled by the Lambda function associated with the intent\. 
+  `ReadyForFulfillment` \- All of the information necessary for the intent is present and the intent ready to be fulfilled by the client application\.
Type: String  
Valid Values:` Fulfilled | Failed | ReadyForFulfillment`   
Required: No

 **intentName**   <a name="lex-Type-runtime_IntentSummary-intentName"></a>
The name of the intent\.  
Type: String  
Required: No

 **slots**   <a name="lex-Type-runtime_IntentSummary-slots"></a>
Map of the slots that have been gathered and their values\.   
Type: String to string map  
Required: No

 **slotToElicit**   <a name="lex-Type-runtime_IntentSummary-slotToElicit"></a>
The next slot to elicit from the user\. If there is not slot to elicit, the field is blank\.  
Type: String  
Required: No

## See Also<a name="API_runtime_IntentSummary_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/runtime.lex-2016-11-28/IntentSummary) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/runtime.lex-2016-11-28/IntentSummary) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/runtime.lex-2016-11-28/IntentSummary) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/runtime.lex-2016-11-28/IntentSummary) 