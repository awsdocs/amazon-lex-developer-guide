# Built\-in Intents<a name="howitworks-builtins-intents"></a>

For common actions, you can use the Alexa standard built\-in intents library\. To create an intent from a built\-in intent, choose a built\-intent in the console, and give it a new name\. The new intent has the configuration of the base intent, such as the sample utterances and slots\. 

For a list of built\-in intents, see [Standard Built\-in Intents](https://developer.amazon.com/docs/custom-skills/standard-built-in-intents.html) in the *Alexa Skills Kit*\.

**Note**  
Amazon Lex doesn't support the following intents:  
`AMAZON.YesIntent`
`AMAZON.NoIntent` 
The intents in the [Built\-in Intent Library](https://developer.amazon.com/docs/custom-skills/built-in-intent-library.html) in the *Alexa Skills Kit*
In the current implementation, you can't do the following:   
Remove sample utterances or slots from the base intent
Configure slots for built\-in intents

**Topics**
+ [AMAZON\.FallbackIntent](built-in-intent-fallback.md)
+ [AMAZON\.KendraSearchIntent](built-in-intent-kendra-search.md)