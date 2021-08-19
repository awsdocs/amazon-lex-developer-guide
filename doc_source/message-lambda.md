# Lambda function<a name="message-lambda"></a>

Amazon Lex V2 allows only one Lambda function for each language in a bot\. The Lambda function and its settings are configured for the bot alias that you use at runtime\. 

The Lambda function is invoked for all intents in that language if dialog and fulfillment code hooks are enabled for the intent\.

Amazon Lex V2 Lambda functions have a different input and output message format from Amazon Lex V1\. These are the differences in the Lambda function input format\.
+ Amazon Lex V2 replaces the `currentIntent` and `alternativeIntents` structures with the `interpretations` structure\. Each interpretation contains an intent, the NLU confidence score for the intent, and an optional sentiment analysis\.
+ Amazon Lex V2 moves the `activeContexts`, `sessionAttributes` in Amazon Lex V1 to the unified `sessionState` structure\. This structure provides information about the current state of the conversation, including the originating request ID\.
+ Amazon Lex V2 doesn't return the `recentIntentSummaryView`\. Use the information in the `sessionState` structure instead\.
+ The Amazon Lex V2 input provides the `botId` and `localeId` in the `bot` attribute\.
+ The input structure contains an `inputMode` attribute that provides information on the type of input: text, speech, or DTMF\.

These are the differences in the Lambda function output format:
+ The `activeContexts` and `sessionAttributes` structures in Amazon Lex V1 are replaced by the `sessionState` structure in Amazon Lex V2\.
+ The `recentIntentSummaryView` isn't included in the output\.
+ The Amazon Lex V1 `dialogAction` structure is split into two structures, `dialogAction` that is part of the `sessionState` structure, and `messages` that is required when the `dialogAction.type` is `EllicitIntent`\. Amazon Lex chooses messages from this structure to show to the user\.

When you build a bot with the Amazon Lex V2 APIs, there is only one Lambda function per bot alias instead of a Lambda function for each intent\. If you want to continue to use separate functions, you can create a router function that activates a separate function for each intent\. The following is a router function that you can use or modify for your application\.

```
import os
import json
import boto3

# reuse client connection as global
client = boto3.client('lambda') 

def router(event):
    intent_name = event['sessionState']['intent']['name']
    fn_name = os.environ.get(intent_name)
    print(f"Intent: {intent_name} -> Lambda: {fn_name}")
    if (fn_name):
        # invoke lambda and return result
        invoke_response = client.invoke(FunctionName=fn_name, Payload = json.dumps(event))
        print(invoke_response)
        payload = json.load(invoke_response['Payload'])
        return payload
    raise Exception('No environment variable for intent: ' + intent_name)
    
def lambda_handler(event, context):
    print(event)
    response = router(event)
    return response
```