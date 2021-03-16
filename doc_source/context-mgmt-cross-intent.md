# Sharing Information Between Intents<a name="context-mgmt-cross-intent"></a>

Amazon Lex supports sharing information between intents\. To share between intents, use session attributes\. 

For example, a user of the `ShoeOrdering` bot starts by ordering shoes\. The bot engages in a conversation with the user, gathering slot data, such as shoe size, color, and brand\. When the user places an order, the Lambda function that fulfills the order sets the `orderNumber` session attribute, which contains the order number\. To get the status of the order, the user uses the `GetOrderStatus` intent\. The bot can ask the user for slot data, such as order number and order date\. When the bot has the required information, it returns the status of the order\.

If you think that your users might switch intents during the same session, you can design your bot to return the status of the latest order\. Instead of asking the user for order information again, you use the `orderNumber` session attribute to share information across intents and fulfill the `GetOrderStatus` intent\. The bot does this by returning the status of the last order that the user placed\.

For an example of cross\-intent information sharing, see [Book Trip](ex-book-trip.md)\.