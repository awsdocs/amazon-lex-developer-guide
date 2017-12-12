# Managing Messages \(Prompts and Statements\)<a name="howitworks-manage-prompts"></a>


+ [Types of Messages](#msg-prompts-msg-types)
+ [Contexts for Configuring Messages](#msg-prompts-context-for-msgs)
+ [Supported Message Formats](#msg-prompts-formats)
+ [Response Cards](#msg-prompts-resp-card)

You configure messages that you want a bot to send when you create the bot\. Consider the following examples:

+ You can configure your bot with the following clarification prompt: 

  ```
  I don't understand. What would you like to do?
  ```

  Amazon Lex sends this message to the client if it doesn't understand the user's intent\. 

   

+ Suppose that you create a bot to support an intent called `OrderPizza`\. For a pizza order, you want users to provide information such as pizza size, toppings, and crust type\. For example, you can configure prompts such as the following:

  ```
  What size pizza you want?
  What toppings you want on the pizza?
  Do you want thick or thin crust?
  ```

  After Amazon Lex determines the user's intent to order pizza, it sends these messages to the client to elicit data from the user\.

This section explains designing user interactions in your bot configuration\. 

## Types of Messages<a name="msg-prompts-msg-types"></a>

You can classify messages as follows:

+ Prompt – A prompt expects a user response, typically a question\. 

+ Statement – A statement does not expect a response\.

The messages you configure can have dynamic components:

+ Messages can use the following syntax to refer to slot values of the intent that Amazon Lex is currently aware of:

  ```
  {SlotName} 
  ```

+ Messages can use the following syntax to refer to session attributes:

  ```
  [AttributeName] 
  ```

You can have messages that include both slots and session attributes\. 

At runtime, Amazon Lex substitutes these references with actual values\. For example, suppose that you configure the following message in the OrderPizza intent of your bot:

```
"Hey [FirstName], your {PizzaTopping} pizza will arrive in [DeliveryTime] minutes" 
```

This message refers to both slot \(`PizzaTopping`\) and session attributes \(`FirstName` and `DeliveryTime`\)\. At runtime, Amazon Lex replaces these placeholders with values and returns the following message to the client:

```
"Hey John, your cheese pizza will arrive in 30 minutes" 
```

For information about session attributes, see the runtime API operations [PostText](API_runtime_PostText.md), and [PostContent](API_runtime_PostContent.md)\. For an example, see [Example Bot: BookTrip](ex-book-trip.md)\. 

If you add code hooks using Lambda functions in your intent configuration, you can create messages dynamically\. Lambda functions can generate messages and return them to Amazon Lex to send to the user\. By providing the messages while configuring your bot, you can eliminate the need to construct a prompt in code hooks\.

## Contexts for Configuring Messages<a name="msg-prompts-context-for-msgs"></a>

You can add messages in the following contexts\. Use the Amazon Lex console or build\-time API to configure your bot:

+ Bot\-level messages – You can configure your bot with clarification prompts and hang\-up messages\. At runtime, Amazon Lex uses the clarification prompts if it does not understand the user's intent\. You can also configure the number of times that Amazon Lex requests clarification before hanging up with a hang\-up message\. You configure these bot\-level messages with the [PutBot](API_PutBot.md) operation, or in the **Error Handling** section in the Amazon Lex console, as shown in the following screen shot:

     
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lex/latest/dg/images/how-works-20.png)
**Note**  
If you have a Lambda function configured as a code hook for an intent, the Lambda function might return a response directing Amazon Lex to elicit user intent\. If the Lambda function does not provide a message to convey to the user, then Amazon Lex uses the clarification prompt you configured\.  
 
Amazon Lex uses the hang\-up statement whenever the user doesn't respond with an appropriate answer for a prompt within the maximum permissible attempts\. This includes responses to intent elicitations, slot elicitations, follow\-up prompts, and intent confirmations\. To configure the maximum permissible attempts, use the [PutBot](API_PutBot.md) operation, or, in the console, specify it in the **Error Handling** section\.  
 

+ Intent\-level messages – You can configure the intent\-level messages such as confirmation prompts, cancel statements, goodbye message, and prompts that Amazon Lex can use to elicit slot values, as shown in the following screenshot:

     
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lex/latest/dg/images/how-works-30.png)

  + Confirmation prompts and cancel statements – After a user provides all of the required data, Amazon Lex asks the user for confirmation using the specified message before fulfilling the intent\. If the user replies "No" to a confirmation prompt, Amazon Lex returns the cancel statement to the client\.

     

  + Goodbye message or follow\-up prompts – If you add a Lambda function as a code hook to fulfill the intent, you can configure one of these messages as backup messages\. If the Lambda function succeeds but does not provide a message to send to the user, Amazon Lex sends the message that you configured\.

     

    + The following is an example of a goodbye message\. The example assumes that the application maintains the `DeliveryTime` session attribute\.

      ```
       "I have placed your order for pizza. It will arrive in [DeliveryTime] minutes."
      ```

    + The following is an example of a follow\-up prompt: 

      ```
      "I have placed your order for pizza. Do you want me to do anything else?".
      ```

      If you configure a follow\-up prompt, you must also configure a cancel statement\. If the user's reply to a follow\-up prompt is a "Yes," Amazon Lex recognizes the user's confirmation and also recognizes the user's intent \(`OrderDrink`\), and then follows up accordingly\. For example:

      ```
      "Yes, I also want to order a drink."
      ```

      If the user says "No," Amazon Lex sends the cancel statement\. For example:

      ```
      "Alright. Let me know if you need anything else."
      ```

  + Prompts to elicit value slot values – You must specify at least one prompt message for each of the required slots in an intent\. At runtime, Amazon Lex uses one of these messages to prompt the user to provide value for this slot\. For example, for a `cityName` slot, the following is a valid prompt:

    ```
     "Which city would you like to fly to?"
    ```
**Note**  
In a Lambda function that is a code hook for an intent, you can override any of the messages that you configured at build time\. 

You can configure more than one message for a specific context\. At runtime, Amazon Lex picks the message with the maximum possible substitutions\. For example, to elicit a value for crust type in the `OrderPizza` intent, you can configure multiple messages, as follows: 

```
Hey [FirstName], what topping would you like for your {PizzaSize} pizza?
Hey [FirstName], what topping would you like for your pizza?
What topping would you like?
Tell me the topping you would like on your pizza.
```

Then, Amazon Lex uses the following order of selection:

+ If both the `FirstName` session attribute and the `PizzaSize` slot value are available, Amazon Lex uses the first prompt\.

+ If the `FirstName` session attribute is available, but the `PizzaSize` slot value isn't, Amazon Lex uses the second prompt\.

+ If both the session attribute and the slot value aren't available, Amazon Lex randomly chooses the third or fourth prompt\.

At runtime, Amazon Lex disregards messages with references to unresolved slot values\. If all of the messages for a given context have unresolved references, Amazon Lex throws a `BadRequestException` error\. We recommend that you have at least one message without references\.

## Supported Message Formats<a name="msg-prompts-formats"></a>

Amazon Lex supports messages in the following formats: plain text and Speech Synthesis Markup Language \(SSML\)\. 

If the output mode is text, such as when a client sends requests using the `PostText` API operation or the `PostContent` API operation with the `Accept` HTTP header set to `text/plain; charset=utf-8`, Amazon Lex selects only plain text messages\. It disregards SSML messages\.

**Note**  
If you configure your bot with only SSML messages and a text client communicates with your bot, Amazon Lex returns a `BadRequestException` error\. We recommend that you provide at least one `PlainText` message for each context\. 
If `outputDialogMode` in the incoming event is text, you must return a `PlainText` message from your AWS Lambda function\. For more information, see [Lambda Function Input Event and Response Format](lambda-input-response-format.md)\. 

Amazon Lex also supports synthesizing audio from SSML\. For more information, see [Using SSML](http://docs.aws.amazon.com/polly/latest/dg/ssml.html) in the *Amazon Polly Developer Guide*\. 

## Response Cards<a name="msg-prompts-resp-card"></a>

Use response cards to simplify interactions for your users and increase your bot's accuracy by reducing typographical errors in text interactions\. A *response card* contains a set of appropriate responses that a user can select to respond to a prompt\. You can send a response card for each prompt that Amazon Lex sends to your client application\. You can use response cards with Facebook Messenger, Slack, and Twilio as well as your own client applications\.

For example, in a taxi application, you can configure an option in the response card for "Home" and set the value to the user's home address\. When the user selects this option, Amazon Lex receives the entire address as the input text\.

![\[An example response card.\]](http://docs.aws.amazon.com/lex/latest/dg/images/resp-console-5.png)

You can define a response card for the following prompts:

+ Conclusion statement

+ Confirmation prompt

+ Follow\-up prompt

+ Rejection statement

+ Slot type utterances

You can define only one response card for each prompt\. 

You configure response cards when you create an intent\. You can define a static response card at build time using the console or the [PutIntent](API_PutIntent.md) operation\. Or you can define a dynamic response card at runtime in a Lambda function\. If you define both static and dynamic response cards, the dynamic response card takes precedence\. 

Amazon Lex sends response cards in the format that the client understands\. It transforms response cards for Facebook Messenger, Slack, and Twilio\. For other clients, Amazon Lex sends a JSON structure in the [PostText](API_runtime_PostText.md) response\. For example, if the client is Facebook Messenger, Amazon Lex transforms the response card to a generic template\. For more information about Facebook Messenger generic templates, see [Generic Template](https://developers.facebook.com/docs/messenger-platform/send-api-reference/generic-template) on the Facebook website\. For an example of the JSON structure, see [Generating Response Cards Dynamically](#msg-prompts-resp-card-dynamic)\.

You can use response cards only with the [PostText](API_runtime_PostText.md) operation\. You can't use response cards with the [PostContent](API_runtime_PostContent.md) operation\. 

### Defining Static Response Cards<a name="msg-prompts-resp-card-static"></a>

Define static response cards with the [PutBot](API_PutBot.md) operation or the Amazon Lex console when you create an intent\. A static response card is defined at the same time as the intent\. Use a static response card when the responses are fixed\. Suppose that you are creating a bot with an intent that has a slot for flavor\. When defining the flavor slot, you specify prompts, as shown in the following console screenshot:

![\[The intent editor in the console.\]](http://docs.aws.amazon.com/lex/latest/dg/images/resp-console-10a.png)

When defining prompts, you can optionally associate a response card and define details with the [PutBot](API_PutBot.md) operation, or, in the Amazon Lex console, as shown in the following example:

![\[The console showing the response card editor.\]](http://docs.aws.amazon.com/lex/latest/dg/images/resp-console-20a.png)

Now suppose that you've integrated your bot with Facebook Messenger\. The user can click the buttons to choose a flavor, as shown in the following illustration:

![\[A response card in Facebook Messenger.\]](http://docs.aws.amazon.com/lex/latest/dg/images/resp-fb-exampleA.png)

To customize the content of a response card, you can refer to session attributes\. At runtime, Amazon Lex substitutes these references with appropriate values from the session attributes\. For more information, see [Setting Session Attributes](context-mgmt.md#context-mgmt-session-attribs)\. For an example, see [Example: Using a Response Card](ex-resp-card.md)\.

### Generating Response Cards Dynamically<a name="msg-prompts-resp-card-dynamic"></a>

To generate response cards dynamically at runtime, use the initialization and validation Lambda function for the intent\. Use a dynamic response card when the responses are determined at runtime in the Lambda function\. In response to user input, the Lambda function generates a response card and returns the it in the `dialogAction` section of the response\. For more information, see [Response Format](lambda-input-response-format.md#using-lambda-response-format)\. 

The following is a partial response from a Lambda function that shows the `responseCard` element\. It generates a user experience similar to the one shown in the preceding section\.

```
responseCard: {
  "version": 1,
  "contentType": "application/vnd.amazonaws.card.generic",
  "genericAttachments": [
    {
      "title": "What Flavor?",
      "subtitle": "What flavor do you want?",
      "imageUrl: "Link to image",
      "attachmentLinkUrl: "Link to attachment",
      "buttons": [
        {
          "text": "Lemon",
          "value": "lemon"
        },
        {
          "text": "Raspberry",
          "value": "raspberry"
        },
        {
          "text": "Plain",
          "value": "plain"
        }
      ]
    }
  ]
}
```

For an example, see [Example Bot: ScheduleAppointment](ex1-sch-appt.md)\.