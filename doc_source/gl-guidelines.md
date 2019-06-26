# General Guidelines<a name="gl-guidelines"></a>

This section describes general guidelines when using Amazon Lex\.
+ Signing requests – All Amazon Lex model\-building and runtime API operations in the [API Reference](API_Reference.md) use signature V4 for authenticating requests\. For more information about authenticating requests, see [Signature Version 4 Signing Process](https://docs.aws.amazon.com/general/latest/gr/signature-version-4.html) in the *Amazon Web Services General Reference*\. 

   

  For [PostContent](API_runtime_PostContent.md), Amazon Lex uses the unsigned payload option described in [ Signature Calculations for the Authorization Header: Transferring Payload in a Single Chunk \(AWS Signature Version 4\)](https://docs.aws.amazon.com/AmazonS3/latest/API/sig-v4-header-based-auth.html) in the *Amazon Simple Storage Service \(S3\) API Reference*\.

   

  When you use the unsigned payload option, don't include the hash of the payload in the canonical request\. Instead, you use the literal string "UNSIGNED\-PAYLOAD" as the hash of the payload\. Also include a header with the name `x-amz-content-sha256` and the value `UNSIGNED-PAYLOAD` in the `PostContent` request\.

   
+ Note the following about how Amazon Lex captures slot values from user utterances:

   

  Amazon Lex uses the enumeration values you provide in a slot type definition to train its machine learning models\. Suppose you define an intent called `GetPredictionIntent` with the following sample utterance:

  ```
  "Tell me the prediction for {Sign}" 
  ```

  Where `{Sign}` is a slot of custom type `ZodiacSign`\. It has 12 enumeration values, `Aries` through `Pisces`\. From the user utterance "Tell me the prediction for \.\.\." Amazon Lex understands what follows is a zodiac sign\. 

   

  When the `valueSelectionStrategy` field is set to `ORIGINAL_VALUE` using the [PutSlotType](API_PutSlotType.md) operation, or if **Expand values** is selected in the console, if the user says "Tell me the prediction for earth", Amazon Lex infers that "earth" is a `ZodiacSign` and passes it to your client application or Lambda functions\. You must check that slot values have valid values before using them in your fulfillment activity\.

   

  If you set the `valueSelectionStrategy` field to `TOP_RESOLUTION` using the [PutSlotType](API_PutSlotType.md) operation, or if **Restrict to slot values and synonyms** is selected in the console, the values that are returned are limited to the values that you defined for the slot type\. For example, if the user says "Tell me the prediction for earth" the value would not be recognized because it is not one of the values defined for the slot type\. When you define synonyms for slot values, they are recognized the same as a slot value, however, the slot value is returned instead of the synonym\.

   

  When Amazon Lex calls a Lambda function or returns the result of a speech interaction with your client application, the case of the slot values is not guaranteed\. For example, if you are eliciting values for the [AMAZON\.Movie](https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/built-in-intent-ref/slot-type-reference#movie) built\-in slot type, and a user says or types "Gone with the wind," Amazon Lex may return "Gone with the Wind," "gone with the wind," or "Gone With The Wind\." In text interactions, the case of the slot values matches the text entered or the slot value, depending on the value of the `valueResolutionStrategy` field\.

   
+ Amazon Lex does not support the AMAZON\.LITERAL built\-in slot type that the Alexa Skills Kit supports\. However, Amazon Lex supports creating custom slot types that you can use to implement this functionality\. As mentioned in the previous bullet, you can capture values outside the custom slot type definition\. Add more and diverse enumeration values to boost the automatic speech recognition \(ASR\) and natural language understanding \(NLU\) accuracy\. 

   
+ The [AMAZON\.DATE](https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/built-in-intent-ref/slot-type-reference#date) and [AMAZON\.TIME](https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/built-in-intent-ref/slot-type-reference#time) built\-in slot types capture both absolute and relative dates and times\. Relative dates and times are resolved in the region where Amazon Lex is processing the request\. 

   

  For the `AMAZON.TIME` built\-in slot type, if the user doesn't specify that a time is before or after noon, the time is ambiguous and Amazon Lex will prompt the user again\. We recommend prompts that elicit an absolute time\. For example, use a prompt such as "When do you want your pizza delivered? You can say 6 PM or 6 in the evening\." 

   
+ Providing confusable training data in your bot reduces Amazon Lex's ability to understand user input\. Consider these examples:

   

  Suppose you have two intents \(`OrderPizza` and `OrderDrink`\) in your bot and both are configured with an "I want to order" utterance\. This utterance does not map to a specific intent that Amazon Lex can learn from while building the language model for the bot at build time\. As a result, when a user inputs this utterance at runtime, Amazon Lex can't pick an intent with a high degree of confidence\.

   

  Consider another example where you define a custom intent for getting a confirmation from the user \(for example, `MyCustomConfirmationIntent`\) and configure the intent with the utterances "Yes" and "No\." Note that Amazon Lex also has a language model for understanding user confirmations\. This can create conflicting situation\. When the user responds with a "Yes," does this mean that this is a confirmation for the ongoing intent or that the user is requesting the custom intent that you created? 

   

  In general, the sample utterances you provide should map to a specific intent and, optionally, to specific slot values\.

   
+ The runtime API operations [PostContent](API_runtime_PostContent.md) and [PostText](API_runtime_PostText.md) take a user ID as the required parameter\. Developers can set this to any value that meets the constraints described in the API\. We recommend you don't use this parameter to send any confidential information such as user logins, emails, or social security numbers\. This ID is primarily used to uniquely identify conversation with a bot \(there can be multiple users ordering pizza\)\.

   
+ If your client application uses Amazon Cognito for authentication, you might use the Amazon Cognito user ID as Amazon Lex user ID\. Note that any Lambda function configured for your bot must have its own authentication mechanism to identify the user on whose behalf Amazon Lex is invoking the Lambda function\.

   
+ We encourage you to define an intent that captures a user's intention to discontinue the conversation\. For example, you can define an intent \(`NothingIntent`\) with sample utterances \("I don't want anything", "exit", "bye bye"\), no slots, and no Lambda function configured as a code hook\. This lets users gracefully close a conversation\.

   