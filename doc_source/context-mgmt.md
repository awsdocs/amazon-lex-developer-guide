# Managing Conversation Context<a name="context-mgmt"></a>

*Conversation context* is the information that a user, your application, or a Lambda function provides to an Amazon Lex bot to fulfill an intent\. Conversation context includes slot data that the user provides, request attributes set by the client application, and session attributes that the client application and Lambda functions create\. 

**Topics**
+ [Setting Session Attributes](#context-mgmt-session-attribs)
+ [Setting Request Attributes](#context-mgmt-request-attribs)
+ [Setting the Session Timeout](#context-mgmt-session-timeout)
+ [Sharing Information Between Intents](#context-mgmt-cross-intent)
+ [Setting Complex Attributes](#context-mgmt-complex-attributes)

## Setting Session Attributes<a name="context-mgmt-session-attribs"></a>

*Session attributes* contain application\-specific information that is passed between a bot and a client application during a session\. Amazon Lex passes session attributes to all Lambda functions configured for a bot\. If a Lambda function adds or updates session attributes, Amazon Lex passes the new information back to the client application\. For example:
+ In [Exercise 1: Create an Amazon Lex Bot Using a Blueprint \(Console\)](gs-bp.md), the example bot uses the `price` session attribute to maintain the price of flowers\. The Lambda function sets this attribute based on the type of flowers that was ordered\. For more information, see [Step 5 \(Optional\): Review the Details of the Information Flow \(Console\)](gs-bp-details-after-lambda.md)\. 
+ In [Example: BookTrip](ex-book-trip.md), the example bot uses the `currentReservation` session attribute to maintain a copy of the slot type data during the conversation to book a hotel or to book a rental car\. For more information, see [Details of the Information Flow](book-trip-detail-flow.md)\.

Use session attributes in your Lambda functions to initialize a bot and to customize prompts and response cards\. For example:
+ Initialization — In a pizza ordering bot, the client application passes the user's location as a session attribute in the first call to the [PostContent](API_runtime_PostContent.md) or [PostText](API_runtime_PostText.md) operation\. For example, `"Location": "111 Maple Street"`\. The Lambda function uses this information to find the closest pizzeria to place the order\.
+ Personalize prompts — Configure prompts and response cards to refer to session attributes\. For example, "Hey \[FirstName\], what toppings would you like?" If you pass the user's first name as a session attribute \(`{"FirstName": "Jo"}`\), Amazon Lex substitutes the name for the placeholder\. It then sends a personalized prompt to the user, "Hey Jo, which toppings would you like?"

Session attributes persist for the duration of the session\. Amazon Lex stores them in an encrypted data store until the session ends\. The client can create session attributes in a request by calling either the [PostContent](API_runtime_PostContent.md) or the [PostText](API_runtime_PostText.md) operation with the `sessionAttributes` field set to a value\. A Lambda function can create a session attribute in a response\. After the client or a Lambda function creates a session attribute, the stored attribute value is used any time that the client application doesn't include `sessionAttribute` field in a request to Amazon Lex\.

For example, suppose you have two session attributes, `{"x": "1", "y": "2"}`\. If the client calls the `PostContent` or `PostText` operation without specifying the `sessionAttributes` field, Amazon Lex calls the Lambda function with the stored session attributes \(`{"x": 1, "y": 2}`\)\. If the Lambda function doesn't return session attributes, Amazon Lex returns the stored session attributes to the client application\.

If either the client application or a Lambda function passes session attributes, Amazon Lex updates the stored session attributes\. Passing an existing value, such as ` {"x": 2}`, updates the stored value\. If you pass a new set of session attributes, such as `{"z": 3}`, the existing values are removed and only the new value is kept\. When an empty map, `{}`, is passed, stored values are erased\.

To send session attributes to Amazon Lex, you create a string\-to\-string map of the attributes\. The following shows how to map session attributes: 

```
{
   "attributeName": "attributeValue",
   "attributeName": "attributeValue"
}
```

For the `PostText` operation, you insert the map into the body of the request using the `sessionAttributes` field, as follows:

```
"sessionAttributes": {
   "attributeName": "attributeValue",
   "attributeName": "attributeValue"
}
```

For the `PostContent` operation, you base64 encode the map, and then send it as the `x-amz-lex-session-attributes` header\.

If you are sending binary or structured data in a session attribute, you must first transform the data to a simple string\. For more information, see [Setting Complex Attributes](#context-mgmt-complex-attributes)\.

## Setting Request Attributes<a name="context-mgmt-request-attribs"></a>

*Request attributes* contain request\-specific information and apply only to the current request\. A client application sends this information to Amazon Lex\. Use request attributes to pass information that doesn't need to persist for the entire session\. You can create your own request attributes or you can use predefined attributes\. To send request attributes, use the `x-amz-lex-request-attributes` header in a [PostContent](API_runtime_PostContent.md) or the `requestAttributes` field in a [PostText](API_runtime_PostText.md) request\. Because request attributes don't persist across requests like session attributes do, they are not returned in `PostContent` or `PostText` responses\. 

**Note**  
To send information that persists across requests, use session attributes\.

The namespace `x-amz-lex:` is reserved for the predefined request attributes\. Don't create request attributes with the prefix `x-amz-lex:`\.

### Setting Predefined Request Attributes<a name="context-mgmt-special"></a>

Amazon Lex provides predefined request attributes for managing the way that it processes information sent to your bot\. The attributes do not persist for the entire session, so you must send the predefined attributes in each request\. All predefined attributes are in the `x-amz-lex:` namespace\.

In addition to the following predefined attributes, Amazon Lex provides predefined attributes for messaging platforms\. For a list of those attributes, see [Deploying an Amazon Lex Bot on a Messaging Platform](example1.md)\.

#### Setting the Response Type<a name="special-response"></a>

If you have two client applications that have different capabilities, you may need to limit the format of messages in a response\. For example, you might want to restrict messages sent to a Web client to plain text, but enable a mobile client to use both plain text and Speech Synthesis Markup Language \(SSML\)\. To set the format of messages returned by the [PostContent](API_runtime_PostContent.md) and [PostText](API_runtime_PostText.md) operations, use the `x-amz-lex:accept-content-types"` request attribute\. 

You can set the attribute to any combination of the following message types: 
+ `PlainText`—The message contains plain UTF\-8 text\.
+ `SSML`—The message contains text formatted for voice output\.
+ `CustomPayload`—The message contains a custom format that you have created for your client\. You can define the payload to meet the needs of your application\.

Amazon Lex returns only messages with the specified type in the `Message` field of the response\. You can set more than one value by separating values with a comma\. If you are using message groups, every message group must contain at least one message of the specified type\. Otherwise, you get a `NoUsableMessageException` error\. For more information, see [Message Groups](howitworks-manage-prompts.md#message-groups)\.

**Note**  
The `x-amz-lex:accept-content-types` request attribute has no effect on the contents of the HTML body\. The contents of a `PostText` operation response is always plain UTF\-8 text\. The body of a `PostContent` operation response contains data in the format set in the `Accept` header in the request\.

#### Setting the Preferred Time Zone<a name="special-time-zone"></a>

To set the time zone used to resolve dates so that it is relative to the user's time zone, use the `x-amz-lex:time-zone` request attribute\. If you do not specify a time zone in the `x-amz-lex:time-zone` attribute, the default depends on the region that you are using for your bot\.


| Region | Default time zone | 
| --- | --- | 
| US East \(N\. Virginia\) | America/New\_York | 
| US West \(Oregon\) | America/Los\_Angeles | 
| Asia Pacific \(Singapore\) | Asia/Singapore | 
| Asia Pacific \(Sydney\) | Australia/Sydney | 
| Asia Pacific \(Tokyo\) | Asia/Tokyo | 
| Europe \(Frankfurt\) | Europe/Berlin | 
| Europe \(Ireland\) | Europe/Dublin | 
| Europe \(London\) | Europe/London | 

For example, if the user responds `tomorrow` in response to the prompt "Which day would you like your package delivered?" the actual *date* that the package is delivered depends on the user's time zone\. For example, when it is 01:00 September 16 in New York, it is 22:00 September 15 in Los Angeles\. If your service is running in the US East \(N\. Virginia\) Region and a person in Los Angeles orders a package to be delivered "tomorrow" using the default time zone, the package would be delivered on the 17th, not the 16th\. However, if you set the `x-amz-lex:time-zone` request attribute to `America/Los_Angeles`, the package would be delivered on the 16th\.

You can set the attribute to any of the Internet Assigned Number Authority \(IANA\) time zone names\. For the list of time zone names, see the [List of tz database time zones](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) on Wikipedia\.

### Setting User\-Defined Request Attributes<a name="context-mgmt-user"></a>

A *user\-defined request attribute* is data that you send to your bot in each request\. You send the information in the `amz-lex-request-attributes` header of a `PostContent` request or in the `requestAttributes` field of a `PostText` request\. 

To send request attributes to Amazon Lex, you create a string\-to\-string map of the attributes\. The following shows how to map request attributes: 

```
{
   "attributeName": "attributeValue",
   "attributeName": "attributeValue"
}
```

For the `PostText` operation, you insert the map into the body of the request using the `requestAttributes` field, as follows:

```
"requestAttributes": {
   "attributeName": "attributeValue",
   "attributeName": "attributeValue"
}
```

For the `PostContent` operation, you base64 encode the map, and then send it as the `x-amz-lex-request-attributes` header\.

If you are sending binary or structured data in a request attribute, you must first transform the data to a simple string\. For more information, see [Setting Complex Attributes](#context-mgmt-complex-attributes)\.

## Setting the Session Timeout<a name="context-mgmt-session-timeout"></a>

Amazon Lex retains context information—slot data and session attributes—until a conversation session ends\. To control how long a session lasts for a bot, set the session timeout\. By default, session duration is 5 minutes, but you can specify any duration between 0 and 1,440 minutes \(24 hours\)\. 

For example, suppose that you create a `ShoeOrdering` bot that supports intents such as `OrderShoes` and `GetOrderStatus`\. When Amazon Lex detects that the user's intent is to order shoes, it asks for slot data\. For example, it asks for shoe size, color, brand, etc\. If the user provides some of the slot data but doesn't complete the shoe purchase, Amazon Lex remembers all of the slot data and session attributes for the entire session\. If the user returns to the session before it expires, he or she can provide the remaining slot data, and complete the purchase\.

In the Amazon Lex console, you set the session timeout when you create a bot\. With the AWS command line interface \(AWS CLI\) or API, you set the timeout when you create or update a bot with the [PutBot](API_PutBot.md) operation by setting the [idleSessionTTLInSeconds](https://docs.aws.amazon.com/lex/latest/dg/API_PutBot.html#lex-PutBot-request-idleSessionTTLInSeconds) field\.

## Sharing Information Between Intents<a name="context-mgmt-cross-intent"></a>

Amazon Lex supports sharing information between intents\. To share between intents, use session attributes\. 

For example, a user of the `ShoeOrdering` bot starts by ordering shoes\. The bot engages in a conversation with the user, gathering slot data, such as shoe size, color, and brand\. When the user places an order, the Lambda function that fulfills the order sets the `orderNumber` session attribute, which contains the order number\. To get the status of the order, the user uses the `GetOrderStatus` intent\. The bot can ask the user for slot data, such as order number and order date\. When the bot has the required information, it returns the status of the order\.

If you think that your users might switch intents during the same session, you can design your bot to return the status of the latest order\. Instead of asking the user for order information again, you use the `orderNumber` session attribute to share information across intents and fulfill the `GetOrderStatus` intent\. The bot does this by returning the status of the last order that the user placed\.

For an example of cross\-intent information sharing, see [Example: BookTrip](ex-book-trip.md)\.

## Setting Complex Attributes<a name="context-mgmt-complex-attributes"></a>

Session and request attributes are string\-to\-string maps of attributes and values\. In many cases, you can use the string map to transfer attribute values between your client application and a bot\. In some cases, however, you might need to transfer binary data or a complex structure that can't be easily converted to a string map\. For example, the following JSON object represents an array of the three most populous cities in the United States:

```
{
   "cities": [
      {
         "city": {
            "name": "New York",
            "state": "New York",
            "pop": "8537673"
         }
      },
      {
         "city": {
            "name": "Los Angeles",
            "state": "California",
            "pop": "3976322"
         }
      },
      {
         "city": {
            "name": "Chicago",
            "state": "Illinois",
            "pop": "2704958"
         }
      }
   ]
}
```

This array of data doesn't translate well to a string\-to\-string map\. In such a case, you can transform an object to a simple string so that you can send it to your bot with the [PostContent](API_runtime_PostContent.md) and [PostText](API_runtime_PostText.md) operations\. 

For example, if you are using JavaScript, you can use the `JSON.stringify` operation to convert an object to JSON, and the `JSON.parse` operation to convert JSON text to a JavaScript object:

```
// To convert an object to a string.
var jsonString = JSON.stringify(object, null, 2);
// To convert a string to an object.
var obj = JSON.parse(JSON string);
```

To send session attributes with the `PostContent` operation, you must base64 encode the attributes before you add them to the request header, as shown in the following JavaScript code:

```
var encodedAttributes = new Buffer(attributeString).toString("base64");
```

You can send binary data to the `PostContent` and `PostText` operations by first converting the data to a base64\-encoded string, and then sending the string as the value in the session attributes:

```
"sessionAttributes" : {
   "binaryData": "base64 encoded data"
}
```