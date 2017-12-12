# Step 3: Create an Intent \(AWS CLI\)<a name="gs-cli-create-order-flowers"></a>

Create an intent for the `OrderFlowersBot` bot and provide three slots, or parameters\. The slots allow the bot to fulfill the intent:

+ `FlowerType` is a custom slot type that specifies which types of flowers can be ordered\.

+ `AMAZON.DATE` and `AMAZON.TIME` are built\-in slot types used for getting the date and time to deliver the flowers from the user\.

**To create the `OrderFlowers` intent \(AWS CLI\)**

1. Create a text file named **OrderFlowers\.json**\. Copy the JSON code from [OrderFlowers\.json](gs-cli-create-order-flowers-json.md) into the text file\.

1. In the AWS CLI, call the [PutIntent](API_PutIntent.md) operation to create the intent\. The example is formatted for Unix, Linux, and macOS\. For Windows, replace the backslash \(\\\) Unix continuation character at the end of each line with a caret \(^\)\.

   ```
   aws lex-models put-intent \
      --region region \
      --endpoint endpoint \
      --name OrderFlowers \
      --cli-input-json file://OrderFlowers.json
   ```

   The server responds with the following:

## Next Step<a name="gs-create-next-4"></a>

[Step 4: Create a Bot \(AWS CLI\)](gs-cli-create-order-flowers-bot.md)