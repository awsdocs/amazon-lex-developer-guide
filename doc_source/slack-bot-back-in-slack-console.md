# Step 5: Complete Slack Integration<a name="slack-bot-back-in-slack-console"></a>

In this section, use the Slack API console to complete integration of the Slack application\.

1. Sign in to the Slack API console at [http://api\.slack\.com](http://api.slack.com)\. Choose the app that you created in [Step 3: Create a Slack Application](slack-bot-assoc-create-app.md)\.

1. Update the **OAuth & Permissions** feature as follows:

   1. In the **Redirect URLs** section, add the OAuth URL that Amazon Lex provided in the preceding step\. Choose **Add a new Redirect URL**, and then choose **Save URLs**\.

   1. In the **Scopes** section, choose two permissions in the **Select Permission Scopes** drop\-down\. Filter the list with the following text:

      + **chat:write:bot**

      + **team:read**

      Choose **Save Changes**\.

1. Update the **Interactive Components** feature by updating the **Request URL** value to the Postback URL that Amazon Lex provided in the preceding step\. Choose **Add**, and then choose **Save URLs**\.

1. Subscribe to the **Event Subscriptions** feature as follows:

   + Enable events by choosing the **On** option\.

   + Set the **Request URL** value to the Postback URL that Amazon Lex provided in the preceding step\. 

   + In the **Subscribe to Bot Events** section, subscribe to the `message.im` bot event to enable direct messaging between the end user and the Slack bot\.

   + Save the changes\.

**Next Step**  
[Step 6: Test the Integration ](slack-bot-test.md)