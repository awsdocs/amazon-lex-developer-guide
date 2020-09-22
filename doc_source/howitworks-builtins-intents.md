# Built\-in Intents<a name="howitworks-builtins-intents"></a>

For common actions, you can use the standard built\-in intents library\. To create an intent from a built\-in intent, choose a built\-intent in the console, and give it a new name\. The new intent has the configuration of the base intent, such as the sample utterances\. 

In the current implementation, you can't do the following: 
+ Add or remove sample utterances from the base intent
+ Configure slots for built\-in intents

**To add a built\-in intent to a bot**

1. Sign in to the AWS Management Console and open the Amazon Lex console at [https://console\.aws\.amazon\.com/lex/](https://console.aws.amazon.com/lex/)\.

1. Choose the bot to add the built\-in intent to\.

1. In the navigation pane, choose the plus \(\+\) next to **Intents**\.

1. For **Add intent**, choose **Search existing intents**\.

1. In the **Search intents** box, type the name of the built\-in intent to add to your bot\.

1. For **Copy built\-in intent**, give the intent a name, and then choose **Add**\.

1. Configure the intent as required for your bot\.

**Topics**
+ [AMAZON\.CancelIntent](built-in-intent-cancel.md)
+ [AMAZON\.FallbackIntent](built-in-intent-fallback.md)
+ [AMAZON\.HelpIntent](built-in-intent-help.md)
+ [AMAZON\.KendraSearchIntent](built-in-intent-kendra-search.md)
+ [AMAZON\.PauseIntent](built-in-intent-pause.md)
+ [AMAZON\.RepeatIntent](built-in-intent-repeat.md)
+ [AMAZON\.ResumeIntent](built-in-intent-resume.md)
+ [AMAZON\.StartOverIntent](built-in-intent-start-over.md)
+ [AMAZON\.StopIntent](built-in-intent-stop.md)

**Note**  
For the English \(US\) \(en\-US\) locale, Amazon Lex supports intents from the Alexa standard built\-in intents\. For a list of built\-in intents, see [Standard Built\-in Intents](https://developer.amazon.com/docs/custom-skills/standard-built-in-intents.html) in the *Alexa Skills Kit*\.  
Amazon Lex doesn't support the following intents:  
`AMAZON.YesIntent`
`AMAZON.NoIntent` 
The intents in the [Built\-in Intent Library](https://developer.amazon.com/docs/custom-skills/built-in-intent-library.html) in the *Alexa Skills Kit*