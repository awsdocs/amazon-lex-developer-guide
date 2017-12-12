# Exercise 2: Add a New Utterance \(AWS CLI\)<a name="gs-cli-update-utterance"></a>

To improve the machine learning model that Amazon Lex uses to recognize requests from your users, add another sample utterance to the bot\. 

Adding a new utterance is a four\-step process\.

1. Use the [GetIntent](API_GetIntent.md) operation to get an intent from Amazon Lex\.

1. Update the intent\.

1. Use the [PutIntent](API_PutIntent.md) operation to send the updated intent back to Amazon Lex\.

1. Use the [GetBot](API_GetBot.md) and [PutBot](API_PutBot.md) operations to rebuild any bot that uses the intent\.

The response from the `GetIntent` operation contains a field called `checksum` that identifies a specific revision of the intent\. You must provide the checksum value when you use the [PutIntent](API_PutIntent.md) operation to update an intent\. If you don't, you'll get the following error message:

**Note**  
The following AWS CLI example is formatted for Unix, Linux, and macOS\. For Windows, change `"\$LATEST"` to `$LATEST`\.

**To update the `OrderFlowers` intent \(AWS CLI\)**

1. In the AWS CLI, get the intent from Amazon Lex\. Amazon Lex sends the output to a file called **OrderFlowers\-V2\.json\.**

   ```
   aws lex-models get-intent \
       --region region \
       --endpoint endpoint \     
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
       --endpoint endpoint \
       --name OrderFlowers \
       --cli-input-json file://OrderFlowers-V2.json
   ```

   Amazon Lex sends the following response:

Now that you have updated the intent, rebuild any bot that uses it\. 

**To rebuild the `OrderFlowersBot` bot \(AWS CLI\)**

1. In the AWS CLI, get the definition of the `OrderFlowersBot` bot and save it to a file with the following command:

   ```
   aws lex-models get-bot \
       --region region \
       --endpoint endpoint \     
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
       --endpoint endpoint \ 
       --name OrderFlowersBot \
       --cli-input-json file://OrderFlowersBot-V2.json
   ```

   The response from the server is:

## Next Step<a name="gs-cli-next-exercise-3"></a>

[Exercise 3: Add a Lambda Function \(AWS CLI\)](gs-cli-update-lambda.md)