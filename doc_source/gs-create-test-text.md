# Test the Bot Using Text Input \(AWS CLI\)<a name="gs-create-test-text"></a>

 To verify that the bot works correctly with text input, use the [PostText](API_runtime_PostText.md) operation\.

**Note**  
The following AWS CLI example is formatted for Unix, Linux, and macOS\. For Windows, change `"\$LATEST"` to `$LATEST`\.

**To use text to test the bot \(AWS CLI\)**

1. In the AWS CLI, start a conversation with the `OrderFlowersBot` bot\. The example is formatted for Unix, Linux, and macOS\. For Windows, replace the backslash \(\\\) Unix continuation character at the end of each line with a caret \(^\)\.

   ```
   aws lex-runtime post-text \
       --region region \
       --endpoint endpoint \
       --bot-name OrderFlowersBot \
       --bot-alias "\$LATEST" \
       --user-id UserOne \
       --input-text "i would like to order flowers"
   ```

   Amazon Lex recognizes the user's intent and starts a conversation by returning the following response:

1. Run the following commands to finish the conversation with the bot\.

   ```
   aws lex-runtime post-text \
       --region region \
       --endpoint endpoint \
       --bot-name OrderFlowersBot \
       --bot-alias "\$LATEST" \
       --user-id UserOne \
       --input-text "roses"
   ```

   ```
   aws lex-runtime post-text  \
       --region region \
       --endpoint endpoint \
       --bot-name OrderFlowersBot \
       --bot-alias "\$LATEST" \
       --user-id UserOne \
       --input-text "tuesday"
   ```

   ```
   aws lex-runtime post-text  \
       --region region \
       --endpoint endpoint \
       --bot-name OrderFlowersBot --bot-alias "\$LATEST" \
       --user-id UserOne \
       --input-text "10:00 a.m."
   ```

   ```
   aws lex-runtime post-text  \
       --region region \
       --endpoint endpoint \
       --bot-name OrderFlowersBot \
       --bot-alias "\$LATEST" \
       --user-id UserOne \
       --input-text "yes"
   ```

    After you confirm the order, Amazon Lex sends a fulfillment response to complete the conversation: 

## Next Step<a name="gs-create-next-test"></a>

[Test the Bot Using Speech Input \(AWS CLI\)](gs-create-test-speech.md)