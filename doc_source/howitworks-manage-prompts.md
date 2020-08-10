# Managing Messages<a name="howitworks-manage-prompts"></a>

**Topics**
+ [Types of Messages](#msg-prompts-msg-types)
+ [Contexts for Configuring Messages](#msg-prompts-context-for-msgs)
+ [Supported Message Formats](#msg-prompts-formats)
+ [Message Groups](#message-groups)
+ [Response Cards](#msg-prompts-resp-card)

When you create a bot, you can configure clarifying or informational messages that you want it to send to the client\. Consider the following examples:
+ You could configure your bot with the following clarification prompt: 

  ```
  I don't understand. What would you like to do?
  ```

  Amazon Lex sends this message to the client if it doesn't understand the user's intent\. 

   
+ Suppose that you create a bot to support an intent called `OrderPizza`\. For a pizza order, you want users to provide information such as pizza size, toppings, and crust type\. You could configure the following prompts:

  ```
  What size pizza do you want?
  What toppings do you want?
  Do you want thick or thin crust?
  ```

  After Amazon Lex determines the user's intent to order pizza, it sends these messages to the client to get information from the user\.

This section explains designing user interactions in your bot configuration\. 

## Types of Messages<a name="msg-prompts-msg-types"></a>

A message can be a prompt or a statement\.
+ A *prompt* is typically a question and expects a user response\. 
+ A *statement* is informational\. It doesn’t expect a response\.

A message can include references to slot, session attributes, and request attributes\. At runtime, Amazon Lex substitutes these references with actual values\. 

To refer to slots values that have been set, use the following syntax:

```
{SlotName} 
```

To refer to session attributes, use the following syntax:

```
[SessionAttributeName] 
```

To refer to request attributes, use the following syntax:

```
((RequestAttributeName)) 
```

Messages can include both slot values, session attributes and request attributes\. 

For example, suppose that you configure the following message in your bot's OrderPizza intent:

```
"Hey [FirstName], your {PizzaTopping} pizza will arrive in [DeliveryTime] minutes." 
```

This message refers to both slot \(`PizzaTopping`\) and session attributes \(`FirstName` and `DeliveryTime`\)\. At runtime, Amazon Lex replaces these placeholders with values and returns the following message to the client:

```
"Hey John, your cheese pizza will arrive in 30 minutes." 
```

To include brackets \(\[\]\) or braces \(\{\}\) in a message, use the backslash \(\\\) escape character\. For example, the following message includes the curly braces and square brackets: 

```
\{Text\} \[Text\]
```

The text returned to the client application looks like this:

```
{Text} [Text]
```

For information about session attributes, see the runtime API operations [PostText](API_runtime_PostText.md) and [PostContent](API_runtime_PostContent.md)\. For an example, see [Example: BookTrip](ex-book-trip.md)\. 

Lambda functions can also generate messages and return them to Amazon Lex to send to the user\. If you add Lambda functions when you configure your intent, you can create messages dynamically\. By providing the messages while configuring your bot, you can eliminate the need to construct a prompt in your Lambda function\.

## Contexts for Configuring Messages<a name="msg-prompts-context-for-msgs"></a>

When you are creating your bot, you can create messages in different contexts, such as clarification prompts in bot, prompts for slot values, and messages from intents\. Amazon Lex chooses an appropriate message in each context to return to your user\. You can provide a group of messages for each context\. If you do, Amazon Lex randomly chooses one message from the group\. You can also specify the format of the message or group the messages together\. For more information, see [Supported Message Formats](#msg-prompts-formats)\.

If you have a Lambda function associated with an intent, you can override any of the messages that you configured at build time\. A Lambda function is not required to use any of these messages, however\.

### Bot Messages<a name="msg-prompts-bot"></a>

You can configure your bot with clarification prompts and session end messages\. At runtime, Amazon Lex uses the clarification prompt** if it doesn't understand the user's intent\. You can configure the number of times that Amazon Lex requests clarification before sending the session end message\. You configure bot\-level messages in the **Error Handling** section of the Amazon Lex console, as follows:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lex/latest/dg/images/how-works-20.png)

With the API, you configure messages by setting the `clarificationPrompt` and `abortStatement` fields in the [PutBot](API_PutBot.md) operation\.

If you use a Lambda function with an intent, the Lambda function might return a response directing Amazon Lex to ask a user's intent\. If the Lambda function doesn’t provide such a message, Amazon Lex uses the clarification prompt\.

### Slot Prompts<a name="msg-prompts-slots"></a>

You must specify at least one prompt message for each of the required slots in an intent\. At runtime, Amazon Lex uses one of these messages to prompt the user to provide a value for the slot\. For example, for a `cityName` slot, the following is a valid prompt: 

```
Which city would you like to fly to?
```

You can set one or more prompts for each slot using the console\. You can also create groups of prompts using the [PutIntent](API_PutIntent.md) operation\. For more information, see [Message Groups](#message-groups)\.

### Responses<a name="msg-prompts-response"></a>

In the console, use the **Responses** section to build dynamic, engaging conversations for your bot\. You can create one or more message groups for a response\. At runtime, Amazon Lex builds a response by selecting one message from each message group\. For more information about message groups, see [Message Groups](#message-groups)\. 

For example, your first message group could contain different greetings: "Hello," "Hi," and "Greetings\." The second message group could contain different forms of introduction: "I am the reservation bot" and "This is the reservation bot\." A third message group could communicate the bot's capabilities: "I can help with car rentals and hotel reservations," "You can make car rentals and hotel reservations," and "I can help you rent a car and book a hotel\."

Lex uses a message from each of the message groups to dynamically build the responses in a conversation\. For example, one interaction could be:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lex/latest/dg/images/default-response-10b.png)

Another one could be:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lex/latest/dg/images/default-response-20c.png)

In either case, the user could respond with a new intent, such as the `BookCar` or `BookHotel` intent\.

You can set up the bot to ask a follow\-up question in the response\. For example, for the preceding interaction, you could create a fourth message group with the following questions: "Can I help with a car or a hotel?", "Would you like to make a reservation now?", and "Is there anything that I can do for you?"\. For messages that include "No" as a response, you can create a follow\-up prompt\. For example:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lex/latest/dg/images/default-response-25a.png)

To create a follow\-up prompt, choose **Wait for user reply**\. Then type the message or messages that you want to send when the user says "No\." When you create a response to use as a follow\-up prompt, you must also specify an appropriate statement when the answer to the statement is "No\." For example:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lex/latest/dg/images/default-response-30b.png)

To add responses to an intent with the API, use the `PutIntent` operation\. To specify a response, set the `conclusionStatement` field in the `PutIntent` request\. To set a follow\-up prompt, set the `followUpPrompt` field and include the statement to send when the user says "No\." You can't set both the `conclusionStatement` field and the `followUpPrompt` field on the same intent\.

## Supported Message Formats<a name="msg-prompts-formats"></a>

When you use the [PostText](API_runtime_PostText.md) operation, or when you use the [PostContent](API_runtime_PostContent.md) operation with the `Accept` header set to `text/plain;charset=utf8`, Amazon Lex supports messages in the following formats:
+ `PlainText`—The message contains plain UTF\-8 text\.
+ `SSML`—The message contains text formatted for voice output\.
+ `CustomPayload`—The message contains a custom format that you have created for your client\. You can define the payload to meet the needs of your application\.
+ `Composite`—The message is a collection of messages, one from each message group\. For more information about message groups, see [Message Groups](#message-groups)\.

By default, Amazon Lex returns any one of the messages defined for a particular prompt\. For example, if you define five messages to elicit a slot value, Amazon Lex chooses one of the messages randomly and returns it to the client\.

If you want Amazon Lex to return a specific type of message to the client in a run\-time request, set the `x-amzn-lex:accept-content-types` request parameter\. The response is limited to the type or types requested\. If there is more than one message of the specified type, Amazon Lex returns one at random\. For more information about the `x-amz-lex:accept-content-types` header, see [Setting the Response Type](context-mgmt.md#special-response)\.

## Message Groups<a name="message-groups"></a>

A *message group* is a set of suitable responses to a particular prompt\. Use message groups when you want your bot to dynamically build the responses in a conversation\. When Amazon Lex returns a response to the client application, it randomly chooses one message from each group\. You can create a maximum of five message groups for each response\. Each group can contain a maximum of five messages\. For examples of creating message groups in the console, see [Responses](#msg-prompts-response)\.

To create a message group, you can use the console or you can use the [PutBot](API_PutBot.md), [PutIntent](API_PutIntent.md), or [PutSlotType](API_PutSlotType.md) operations to assign a group number to a message\. If you don't create a message group, or if you create only one message group, Amazon Lex sends a single message in the `Message` field\. Client applications get multiple messages in a response only when you have created more than one message group in the console, or when you create more than one message group when you create or update an intent with the [PutIntent](API_PutIntent.md) operation\. 

When Amazon Lex sends a message from a group, the response's `Message` field contains an escaped JSON object that contains the messages\. The following example shows the contents of the `Message` field when it contains multiple messages\.

**Note**  
The example is formatted for readability\. A response doesn't contain carriage returns \(CR\)\.

```
{\"messages\":[
   {\"type\":\"PlainText\",\"group\":0,\"value\":\"Plain text\"},
   {\"type\":\"SSML\",\"group\":1,\"value\":\"SSML text\"},
   {\"type\":\"CustomPayload\",\"group\":2,\"value\":\"Custom payload\"}
]}
```

You can set the format of the messages\. The format can be one of the following:
+ PlainText—The message is in plain UTF\-8 text\.
+ SSML—The message is Speech Synthesis Markup Language \(SSML\)\.
+ CustomPayload—The message is in a custom format that you specified\.

To control the format of messages that the `PostContent` and `PostText` operations return in the `Message` field, set the `x-amz-lex:accept-content-types` request attribute\. For example, if you set the header to the following, you receive only plain text and SSML messages in the response:

```
x-amz-lex:accept-content-types: PlainText,SSML
```

If you request a specific message format and a message group doesn't contain that a message with that format, you get a `NoUsableMessageException` exception\. When you use a message group to group messages by type, don't use the `x-amz-lex:accept-content-types` header\.

For more information about the `x-amz-lex:accept-content-types` header, see [Setting the Response Type](context-mgmt.md#special-response)\.

## Response Cards<a name="msg-prompts-resp-card"></a>

A *response card* contains a set of appropriate responses to a prompt\. Use response cards to simplify interactions for your users and increase your bot's accuracy by reducing typographical errors in text interactions\. You can send a response card for each prompt that Amazon Lex sends to your client application\. You can use response cards with Facebook Messenger, Slack, Twilio, and your own client applications\.

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

To generate response cards dynamically at runtime, use the initialization and validation Lambda function for the intent\. Use a dynamic response card when the responses are determined at runtime in the Lambda function\. In response to user input, the Lambda function generates a response card and returns it in the `dialogAction` section of the response\. For more information, see [Response Format](lambda-input-response-format.md#using-lambda-response-format)\. 

The following is a partial response from a Lambda function that shows the `responseCard` element\. It generates a user experience similar to the one shown in the preceding section\.

```
responseCard: {
  "version": 1,
  "contentType": "application/vnd.amazonaws.card.generic",
  "genericAttachments": [
    {
      "title": "What Flavor?",
      "subtitle": "What flavor do you want?",
      "imageUrl": "Link to image",
      "attachmentLinkUrl": "Link to attachment",
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

For an example, see [Example: ScheduleAppointment](ex1-sch-appt.md)\.