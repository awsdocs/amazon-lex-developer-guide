# Setting Session Attributes<a name="context-mgmt-session-attribs"></a>

*Session attributes* contain application\-specific information that is passed between a bot and a client application during a session\. Amazon Lex passes session attributes to all Lambda functions configured for a bot\. If a Lambda function adds or updates session attributes, Amazon Lex passes the new information back to the client application\. For example:
+ In [Exercise 1: Create an Amazon Lex Bot Using a Blueprint \(Console\)](gs-bp.md), the example bot uses the `price` session attribute to maintain the price of flowers\. The Lambda function sets this attribute based on the type of flowers that was ordered\. For more information, see [Step 5 \(Optional\): Review the Details of the Information Flow \(Console\)](gs-bp-details-after-lambda.md)\. 
+ In [Book Trip](ex-book-trip.md), the example bot uses the `currentReservation` session attribute to maintain a copy of the slot type data during the conversation to book a hotel or to book a rental car\. For more information, see [Details of the Information Flow](book-trip-detail-flow.md)\.

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

If you are sending binary or structured data in a session attribute, you must first transform the data to a simple string\. For more information, see [Setting Complex Attributes](context-mgmt-complex-attributes.md)\.