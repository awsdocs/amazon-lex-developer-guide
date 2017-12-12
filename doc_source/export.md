# Exporting Amazon Lex Bots<a name="export"></a>

Amazon Lex enables you to export a bot in a format compatible with a target platform\. When you export a bot you convert its associated intents, slot types, and dialog model into a JSON file\. Use the Amazon Lex console or the [GetExport](API_GetExport.md) operation to create the JSON file\.

## Export to an Alexa Skill<a name="export-to-alexa"></a>

You can export your bot schema in a format compatible with an Alexa skill\. After you export the bot, you upload it to Alexa using the skill builder\.

First export your bot and its interaction model to a JSON file\.

1. Sign in to the AWS Management Console and open the Amazon Lex console at [https://console\.aws\.amazon\.com/lex/](https://console.aws.amazon.com/lex/)\.

1. Under **Actions** choose **Export** to export the bot\.

1. Choose the name and version of the bot that you want to export and then choose **Export**\. Choose **Alexa Skills Kit** as the format to export\.

1. In a moment a download dialog box will appear\. Select a location for the file and choose **Save**\.

The downloaded file is a ZIP archive containing one files, named after the bot that was exported\. It contains the information necessary to import the bot as an Alexa skill\.

**Note**  
Note these differences between Amazon Lex and the Alexa Skills Kit\.  
Session attributes, denoted by square brackets \(\[\]\), are not supported by the Alexa Skills Kit\. You will need to update prompts that use session attributes\.
Punctuation marks are not supported by the Alexa Skills Kit\. You will need to update utterances that use punctuation\.

Once you have exported your bot, you can upload it into an Alexa skill using the skill builder\.

1. Log in to the Alexa section of the developer portal at [https://developer\.amazon\.com/](https://developer.amazon.com/edw/home.html#/)\.

1. In the Alexa Skills Kit box, choose **Get Started** to open the Alexa Skill Kit page\. This displays any skills you've created\.

1. Choose **Add a New Skill**\. Fill in the required fields:

   + **Skill Type** \(select **Custom Interaction Model**\)

   + **Language**

   + **Name**

   + **Invocation Name**

1. Choose **Save** to save the new skill and then choose **Next**\.

1. Choose **Launch Skill Builder**\. From the left menu, choose **Code Editor**\.

1. Paste the contents of the JSON file that you downloaded from the Amazon Lex console into the code editor field\. Alexa requires that each skill contain the `AMAZON.CancelIntent`, `AMAZON.HelpIntent`, and `AMAZON.StopIntent` intents\. If your skill does not contain these intents, add them\.

   ```
       {
         "name": "AMAZON.CancelIntent",
         "samples": []
       },
       {
         "name": "AMAZON.HelpIntent",
         "samples": []
       },
       {
         "name": "AMAZON.StopIntent",
         "samples": []
       }
   ```

1. Choose **Apply Changes** to save your changes and then choose **Build Model**\.

Once you have uploaded the schema into an Alexa skill you can make any changes necessary for running the skill with Alexa\. For more information about creating an Alexa skill, see the [Use the Skill Builder \(Beta\)](https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/ask-define-the-vui-with-gui) in the *Alexa Skills Kit*\. 