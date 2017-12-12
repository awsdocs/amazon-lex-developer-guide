# Exercise 3: Add a Lambda Function \(AWS CLI\)<a name="gs-cli-update-lambda"></a>

Add a Lambda function that validates user input and fulfills the user's intent to the bot\.

Adding a Lambda expression is a five\-step process\.

1. Use the Lambda [AddPermission](http://docs.aws.amazon.com/lambda/latest/dg/API_AddPermission.html) function to enable the `OrderFlowers` intent to call the Lambda [Invoke](http://docs.aws.amazon.com/lambda/latest/dg/lambda-api-permissions-ref.html) operation\.

1. Use the [GetIntent](API_GetIntent.md) operation to get the intent from Amazon Lex\.

1. Update the intent to add the Lambda function\.

1. Use the [PutIntent](API_PutIntent.md) operation to send the updated intent back to Amazon Lex\.

1. Use the [GetBot](API_GetBot.md) and [GetBot](API_GetBot.md) operations to rebuild any bot that uses the intent\.

If you add a Lambda function to an intent before you add the `InvokeFunction` permission, you get the following error message:

The response from the `GetIntent` operation contains a field called `checksum` that identifies a specific revision of the intent\. When you use the [PutIntent](API_PutIntent.md) operation to update an intent, you must provide the checksum value\. If you don't, you get the following error message:

This exercise uses the Lambda function from [Example Bot: ScheduleAppointment](ex1-sch-appt.md)\. For instructions to create the Lambda function, see [Step 2: Create a Lambda Function](ex1-sch-appt-create-lambda-function.md)\.

**Note**  
The following AWS CLI example is formatted for Unix, Linux, and macOS\. For Windows, change `"\$LATEST"` to `$LATEST`\.

**To add a Lambda function to an intent**

1. In the AWS CLI, add the `InvokeFunction` permission for the `OrderFlowers` intent:

   ```
   aws lambda add-permission 
       --region region \
       --endpoint endpoint \     
       --function-name OrderFlowersCodeHook \
       --statement-id LexGettingStarted-OrderFlowersBot \
       --action lambda:InvokeFunction \
       --principal lex.amazonaws.com \
       --source-arn "arn:aws:lex:region:account ID:intent:OrderFlowers:*"
   ```

   Lambda sends the following response:

1. Get the intent from Amazon Lex\. Amazon Lex sends the output to a file called **OrderFlowers\-V3\.json**\.

   ```
   aws lex-models get-intent 
       --region region \
       --endpoint endpoint \     
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
              },
          }
      ```

   1. Save the file\.

1. In the AWS CLI, send the updated intent to Amazon Lex:

   ```
   aws lex-models put-intent 
       --region region \
       --endpoint endpoint \     
       --name OrderFlowers \
       --cli-input-json file://OrderFlowers-V3.json
   ```

Now that you have updated the intent, rebuild the bot\. 

**To rebuild the `OrderFlowersBot` bot**

1. In the AWS CLI, get the definition of the `OrderFlowersBot` bot and save it to a file:

   ```
   aws lex-models get-bot 
       --region region \
       --endpoint endpoint \     
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
   aws lex-models put-bot 
       --region region \
       --endpoint endpoint \     
       --name OrderFlowersBot \
       --cli-input-json file://OrderFlowersBot-V3.json
   ```

   The response from the server is:

## Next Step<a name="gs-cli-next-exercise-4"></a>

[Exercise 4: Publish a Version \(AWS CLI\)](gs-cli-publish.md)