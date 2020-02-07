# Exercise 2: Add a New Utterance \(AWS CLI\)<a name="gs-cli-update-utterance"></a>

To improve the machine learning model that Amazon Lex uses to recognize requests from your users, add another sample utterance to the bot\. 

Adding a new utterance is a four\-step process\.

1. Use the [GetIntent](API_GetIntent.md) operation to get an intent from Amazon Lex\.

1. Update the intent\.

1. Use the [PutIntent](API_PutIntent.md) operation to send the updated intent back to Amazon Lex\.

1. Use the [GetBot](API_GetBot.md) and [PutBot](API_PutBot.md) operations to rebuild any bot that uses the intent\.

To run the commands in this exercise, you need to know the region where the commands will be run\. For a list of regions, see [ Model Building Quotas ](gl-limits.md#gl-limits-model-building)\.

The response from the `GetIntent` operation contains a field called `checksum` that identifies a specific revision of the intent\. You must provide the checksum value when you use the [PutIntent](API_PutIntent.md) operation to update an intent\. If you don't, you'll get the following error message:

```
            An error occurred (PreconditionFailedException) when calling 
            the PutIntent operation: Intent intent name already exists. 
            If you are trying to update intent name you must specify the 
            checksum.
```

**Note**  
The following AWS CLI example is formatted for Unix, Linux, and macOS\. For Windows, change `"\$LATEST"` to `$LATEST` and replace the backslash \(\\\) continuation character at the end of each line with a caret \(^\)\.

**To update the `OrderFlowers` intent \(AWS CLI\)**

1. In the AWS CLI, get the intent from Amazon Lex\. Amazon Lex sends the output to a file called **OrderFlowers\-V2\.json\.**

   ```
   aws lex-models get-intent \
       --region region \
       --name OrderFlowers \
       --intent-version "\$LATEST" > OrderFlowers-V2.json
   ```

1. Open **OrderFlowers\-V2\.json** in a text editor\.

   1. Find and delete the `createdDate`, `lastUpdatedDate`, and `version` fields\.

   1. Add the following to the `sampleUtterances` field:

      ```
      I want to order flowers
      ```

   1. Save the file\.

1. Send the updated intent to Amazon Lex with the following command:

   ```
   aws lex-models put-intent  \
       --region region \
       --name OrderFlowers \
       --cli-input-json file://OrderFlowers-V2.json
   ```

   Amazon Lex sends the following response:

   ```
   {
       "confirmationPrompt": {
           "maxAttempts": 2, 
           "messages": [
               {
                   "content": "Okay, your {FlowerType} will be ready for pickup by {PickupTime} on {PickupDate}.  Does this sound okay?", 
                   "contentType": "PlainText"
               }
           ]
       }, 
       "name": "OrderFlowers", 
       "checksum": "checksum", 
       "version": "$LATEST", 
       "rejectionStatement": {
           "messages": [
               {
                   "content": "Okay, I will not place your order.", 
                   "contentType": "PlainText"
               }
           ]
       }, 
       "createdDate": timestamp, 
       "lastUpdatedDate": timestamp, 
       "sampleUtterances": [
           "I would like to pick up flowers", 
           "I would like to order some flowers", 
           "I want to order flowers"
       ], 
       "slots": [
           {
               "slotType": "AMAZON.TIME", 
               "name": "PickupTime", 
               "slotConstraint": "Required", 
               "valueElicitationPrompt": {
                   "maxAttempts": 2, 
                   "messages": [
                       {
                           "content": "Pick up the {FlowerType} at what time on {PickupDate}?", 
                           "contentType": "PlainText"
                       }
                   ]
               }, 
               "priority": 3, 
               "description": "The time to pick up the flowers"
           }, 
           {
               "slotType": "FlowerTypes", 
               "name": "FlowerType", 
               "slotConstraint": "Required", 
               "valueElicitationPrompt": {
                   "maxAttempts": 2, 
                   "messages": [
                       {
                           "content": "What type of flowers would you like to order?", 
                           "contentType": "PlainText"
                       }
                   ]
               }, 
               "priority": 1, 
               "slotTypeVersion": "$LATEST", 
               "sampleUtterances": [
                   "I would like to order {FlowerType}"
               ], 
               "description": "The type of flowers to pick up"
           }, 
           {
               "slotType": "AMAZON.DATE", 
               "name": "PickupDate", 
               "slotConstraint": "Required", 
               "valueElicitationPrompt": {
                   "maxAttempts": 2, 
                   "messages": [
                       {
                           "content": "What day do you want the {FlowerType} to be picked up?", 
                           "contentType": "PlainText"
                       }
                   ]
               }, 
               "priority": 2, 
               "description": "The date to pick up the flowers"
           }
       ], 
       "fulfillmentActivity": {
           "type": "ReturnIntent"
       }, 
       "description": "Intent to order a bouquet of flowers for pick up"
   }
   ```

Now that you have updated the intent, rebuild any bot that uses it\. 

**To rebuild the `OrderFlowersBot` bot \(AWS CLI\)**

1. In the AWS CLI, get the definition of the `OrderFlowersBot` bot and save it to a file with the following command:

   ```
   aws lex-models get-bot \
       --region region \
       --name OrderFlowersBot \
       --version-or-alias "\$LATEST" > OrderFlowersBot-V2.json
   ```

1. In a text editor, open **OrderFlowersBot\-V2\.json**\. Remove the `createdDate`, `lastUpdatedDate`, `status` and `version` fields\.

1. In a text editor, add the following line to the bot definition:

   ```
   "processBehavior": "BUILD",
   ```

1. In the AWS CLI, build a new revision of the bot by running the following command to :

   ```
   aws lex-models put-bot \
       --region region \
       --name OrderFlowersBot \
       --cli-input-json file://OrderFlowersBot-V2.json
   ```

   The response from the server is:

   ```
   {
       "status": "BUILDING", 
       "intents": [
           {
               "intentVersion": "$LATEST", 
               "intentName": "OrderFlowers"
           }
       ], 
       "name": "OrderFlowersBot", 
       "locale": "en-US", 
       "checksum": "checksum", 
       "abortStatement": {
           "messages": [
               {
                   "content": "Sorry, I'm not able to assist at this time", 
                   "contentType": "PlainText"
               }
           ]
       }, 
       "version": "$LATEST", 
       "lastUpdatedDate": timestamp, 
       "createdDate": timestamp 
       "clarificationPrompt": {
           "maxAttempts": 2, 
           "messages": [
               {
                   "content": "I didn't understand you, what would you like to do?", 
                   "contentType": "PlainText"
               }
           ]
       }, 
       "voiceId": "Salli", 
       "childDirected": false, 
       "idleSessionTTLInSeconds": 600, 
       "description": "Bot to order flowers on the behalf of a user"
   }
   ```

## Next Step<a name="gs-cli-next-exercise-3"></a>

[Exercise 3: Add a Lambda Function \(AWS CLI\)](gs-cli-update-lambda.md)