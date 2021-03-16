# Setting Request Attributes<a name="context-mgmt-request-attribs"></a>

*Request attributes* contain request\-specific information and apply only to the current request\. A client application sends this information to Amazon Lex\. Use request attributes to pass information that doesn't need to persist for the entire session\. You can create your own request attributes or you can use predefined attributes\. To send request attributes, use the `x-amz-lex-request-attributes` header in a [PostContent](API_runtime_PostContent.md) or the `requestAttributes` field in a [PostText](API_runtime_PostText.md) request\. Because request attributes don't persist across requests like session attributes do, they are not returned in `PostContent` or `PostText` responses\. 

**Note**  
To send information that persists across requests, use session attributes\.

The namespace `x-amz-lex:` is reserved for the predefined request attributes\. Don't create request attributes with the prefix `x-amz-lex:`\.

## Setting Predefined Request Attributes<a name="context-mgmt-special"></a>

Amazon Lex provides predefined request attributes for managing the way that it processes information sent to your bot\. The attributes do not persist for the entire session, so you must send the predefined attributes in each request\. All predefined attributes are in the `x-amz-lex:` namespace\.

In addition to the following predefined attributes, Amazon Lex provides predefined attributes for messaging platforms\. For a list of those attributes, see [Deploying an Amazon Lex Bot on a Messaging Platform](example1.md)\.

### Setting the Response Type<a name="special-response"></a>

If you have two client applications that have different capabilities, you may need to limit the format of messages in a response\. For example, you might want to restrict messages sent to a Web client to plain text, but enable a mobile client to use both plain text and Speech Synthesis Markup Language \(SSML\)\. To set the format of messages returned by the [PostContent](API_runtime_PostContent.md) and [PostText](API_runtime_PostText.md) operations, use the `x-amz-lex:accept-content-types"` request attribute\. 

You can set the attribute to any combination of the following message types: 
+ `PlainText`—The message contains plain UTF\-8 text\.
+ `SSML`—The message contains text formatted for voice output\.
+ `CustomPayload`—The message contains a custom format that you have created for your client\. You can define the payload to meet the needs of your application\.

Amazon Lex returns only messages with the specified type in the `Message` field of the response\. You can set more than one value by separating values with a comma\. If you are using message groups, every message group must contain at least one message of the specified type\. Otherwise, you get a `NoUsableMessageException` error\. For more information, see [Message Groups](howitworks-manage-prompts.md#message-groups)\.

**Note**  
The `x-amz-lex:accept-content-types` request attribute has no effect on the contents of the HTML body\. The contents of a `PostText` operation response is always plain UTF\-8 text\. The body of a `PostContent` operation response contains data in the format set in the `Accept` header in the request\.

### Setting the Preferred Time Zone<a name="special-time-zone"></a>

To set the time zone used to resolve dates so that it is relative to the user's time zone, use the `x-amz-lex:time-zone` request attribute\. If you do not specify a time zone in the `x-amz-lex:time-zone` attribute, the default depends on the region that you are using for your bot\.


| Region | Default time zone | 
| --- | --- | 
| US East \(N\. Virginia\) |  America/New\_York  | 
| US West \(Oregon\) |  America/Los\_Angeles  | 
| Asia Pacific \(Singapore\) |  Asia/Singapore  | 
| Asia Pacific \(Sydney\) |  Australia/Sydney  | 
| Asia Pacific \(Tokyo\) |  Asia/Tokyo  | 
| Europe \(Frankfurt\) |  Europe/Berlin  | 
| Europe \(Ireland\) |  Europe/Dublin  | 
| Europe \(London\) |  Europe/London  | 

For example, if the user responds `tomorrow` in response to the prompt "Which day would you like your package delivered?" the actual *date* that the package is delivered depends on the user's time zone\. For example, when it is 01:00 September 16 in New York, it is 22:00 September 15 in Los Angeles\. If your service is running in the US East \(N\. Virginia\) Region and a person in Los Angeles orders a package to be delivered "tomorrow" using the default time zone, the package would be delivered on the 17th, not the 16th\. However, if you set the `x-amz-lex:time-zone` request attribute to `America/Los_Angeles`, the package would be delivered on the 16th\.

You can set the attribute to any of the Internet Assigned Number Authority \(IANA\) time zone names\. For the list of time zone names, see the [List of tz database time zones](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) on Wikipedia\.

## Setting User\-Defined Request Attributes<a name="context-mgmt-user"></a>

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

If you are sending binary or structured data in a request attribute, you must first transform the data to a simple string\. For more information, see [Setting Complex Attributes](context-mgmt-complex-attributes.md)\.