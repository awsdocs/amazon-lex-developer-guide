# Exercise 3: Add a Lambda Function \(AWS CLI\)<a name="gs-cli-update-lambda"></a>

Add a Lambda function that validates user input and fulfills the user's intent to the bot\.

Adding a Lambda expression is a five\-step process\.

1. Use the Lambda [AddPermission](http://docs.aws.amazon.com/lambda/latest/dg/API_AddPermission.html) function to enable the `OrderFlowers` intent to call the Lambda [Invoke](http://docs.aws.amazon.com/lambda/latest/dg/lambda-api-permissions-ref.html) operation\.

1. Use the [GetIntent](API_GetIntent.md) operation to get the intent from Amazon Lex\.

1. Update the intent to add the Lambda function\.

1. Use the [PutIntent](API_PutIntent.md) operation to send the updated intent back to Amazon Lex\.

1. Use the [GetBot](API_GetBot.md) and [PutBot](API_PutBot.md) operations to rebuild any bot that uses the intent\.

To run the commands in this exercise, you need to know the region where the commands will be run\. For a list of regions, see [ Model Building Quotas ](gl-limits.md#gl-limits-model-building)\.

If you add a Lambda function to an intent before you add the `InvokeFunction` permission, you get the following error message:

```
            An error occurred (BadRequestException) when calling the 
            PutIntent operation: Lex is unable to access the Lambda 
            function Lambda function ARN in the context of intent 
            intent ARN.  Please check the resource-based policy on 
            the function.
```

The response from the `GetIntent` operation contains a field called `checksum` that identifies a specific revision of the intent\. When you use the [PutIntent](API_PutIntent.md) operation to update an intent, you must provide the checksum value\. If you don't, you get the following error message:

```
            An error occurred (PreconditionFailedException) when calling 
            the PutIntent operation: Intent intent name already exists. 
            If you are trying to update intent name you must specify the 
            checksum.
```

This exercise uses the Lambda function from [Exercise 1: Create an Amazon Lex Bot Using a Blueprint \(Console\)](gs-bp.md)\. For instructions to create the Lambda function, see [Step 3: Create a Lambda Function \(Console\)](gs-bp-create-lambda-function.md)\.

**Note**  
The following AWS CLI example is formatted for Unix, Linux, and macOS\. For Windows, change `"\$LATEST"` to `$LATEST`\.

**To add a Lambda function to an intent**

1. In the AWS CLI, add the `InvokeFunction` permission for the `OrderFlowers` intent:

   ```
   aws lambda add-permission \
       --region region \
       --function-name OrderFlowersCodeHook \
       --statement-id LexGettingStarted-OrderFlowersBot \
       --action lambda:InvokeFunction \
       --principal lex.amazonaws.com \
       --source-arn "arn:aws:lex:region:account ID:intent:OrderFlowers:*"
   ```

   Lambda sends the following response:

   ```
   {
       "Statement": "{\"Sid\":\"LexGettingStarted-OrderFlowersBot\",
         \"Resource\":\"arn:aws:lambda:region:account ID:function:OrderFlowersCodeHook\",
         \"Effect\":\"Allow\",
         \"Principal\":{\"Service\":\"lex.amazonaws.com\"},
         \"Action\":[\"lambda:InvokeFunction\"],
         \"Condition\":{\"ArnLike\":
           {\"AWS:SourceArn\":
             \"arn:aws:lex:region:account ID:intent:OrderFlowers:*\"}}}"
   }
   ```

1. Get the intent from Amazon Lex\. Amazon Lex sends the output to a file called **OrderFlowers\-V3\.json**\.

   ```
   aws lex-models get-intent \
       --region region \
       --name OrderFlowers \
       --intent-version "\$LATEST" > OrderFlowers-V3.json
   ```

1. In a text editor, open the **OrderFlowers\-V3\.json**\.

   1. Find and delete the `createdDate`, `lastUpdatedDate`, and `version` fields\.

   1. Update the `fulfillmentActivity` field :

      ```
          "fulfillmentActivity": {
              "type": "CodeHook",
              "codeHook": {
                  "uri": "arn:aws:lambda:region:account ID:function:OrderFlowersCodeHook",
                  "messageVersion": "1.0"
              }
          }
      ```

   1. Save the file\.

1. In the AWS CLI, send the updated intent to Amazon Lex:

   ```
   aws lex-models put-intent \
       --region region \
       --name OrderFlowers \
       --cli-input-json file://OrderFlowers-V3.json
   ```

Now that you have updated the intent, rebuild the bot\. 

**To rebuild the `OrderFlowersBot` bot**

1. In the AWS CLI, get the definition of the `OrderFlowersBot` bot and save it to a file:

   ```
   aws lex-models get-bot \
       --region region \
       --name OrderFlowersBot \
       --version-or-alias "\$LATEST" > OrderFlowersBot-V3.json
   ```

1. In a text editor,open **OrderFlowersBot\-V3\.json**\. Remove the `createdDate`, `lastUpdatedDate`, `status`, and `version` fields\.

1. In the text editor, add the following line to the definition of the bot:

   ```
   "processBehavior": "BUILD",
   ```

1. In the AWS CLI, build a new revision of the bot:

   ```
   aws lex-models put-bot \
       --region region \
       --name OrderFlowersBot \
       --cli-input-json file://OrderFlowersBot-V3.json
   ```

   The response from the server is:

   ```
   {
       "status": "READY", 
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
       "createdDate": timestamp, 
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

## Next Step<a name="gs-cli-next-exercise-4"></a>

[Exercise 4: Publish a Version \(AWS CLI\)](gs-cli-publish.md)