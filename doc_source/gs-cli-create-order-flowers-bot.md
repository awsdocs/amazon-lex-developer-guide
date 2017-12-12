# Step 4: Create a Bot \(AWS CLI\)<a name="gs-cli-create-order-flowers-bot"></a>

The `OrderFlowersBot` bot has one intent, the `OrderFlowers` intent that you created in the previous step\.

**Note**  
The following AWS CLI example is formatted for Unix, Linux, and macOS\. For Windows, change `"\$LATEST"` to `$LATEST`\.

**To create the `OrderFlowersBot` bot \(AWS CLI\)**

1. Create a text file named **OrderFlowersBot\.json**\. Copy the JSON code from [OrderFlowersBot\.json](gs-cli-create-order-flowers-bot-json.md) into the text file\.

1. In the AWS CLI, call the [PutBot](API_PutBot.md) operation to create the bot\. The example is formatted for Unix, Linux, and macOS\. For Windows, replace the backslash \(\\\) Unix continuation character at the end of each line with a caret \(^\)\.

   ```
   aws lex-models put-bot \
       --region region \
       --endpoint endpoint \
       --name OrderFlowersBot \
       --cli-input-json file://OrderFlowersBot.json
   ```

   The response from the server follows\. When you create or update bot, the `status` field is set to `BUILDING`\. This indicates that the bot isn't ready to use\. To determine when the bot is ready for use, use the [GetBot](API_GetBot.md) operation in the next step \. 

1. To determine if your new bot is ready for use, run the following command\. Repeat this command until the `status` field returns `READY`\. The example is formatted for Unix, Linux, and macOS\. For Windows, replace the backslash \(\\\) Unix continuation character at the end of each line with a caret \(^\)\.

   ```
   aws lex-models get-bot \
       --region region \
       --endpoint endpoint \
       --name OrderFlowersBot \
       --version-or-alias "\$LATEST"
   ```

   Look for the `status` field in the response:

## Next Step<a name="gs-create-step-next-5"></a>

[Step 5: Test a Bot \(AWS CLI\)](gs-create-test.md)