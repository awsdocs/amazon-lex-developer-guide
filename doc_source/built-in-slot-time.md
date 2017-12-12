# AMAZON\.TIME<a name="built-in-slot-time"></a>

Converts words that represent times into time values\.

Amazon Lex extends the [AMAZON\.TIME](https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/built-in-intent-ref/slot-type-reference#time) slot type to include resolutions for ambiguous times\. When a user enters an ambiguous time, Amazon Lex uses the `slotDetails` attribute of a Lambda event to pass resolutions for the ambiguous times to your Lambda function\. For example, if your bot prompts the user for a delivery time, the user can respond by saying "10 o'clock\." This time is ambiguous\. It means either 10:00 AM or 10:00 PM\. In this case, the value in the `slots` map is `null`, and the `slotDetails` entity contains the two possible resolutions of the time\. Amazon Lex inputs the following into the Lambda function:

```
"slots": {
   "deliveryTime": null
},
"slotDetails": {
   "deliveryTime": {
      "resolutions": [
         {
            "value": "10:00"
         },
         {
            "value": "22:00"
         }
      ]
   }
}
```

When the user responds with an unambiguous time, Amazon Lex sends the time to your Lambda function in the `slots` attribute of the Lambda event and the `slotDetails` attribute is empty\. For example, if your user responds to the prompt for a delivery time with "10:00 PM," Amazon Lex inputs the following into the Lambda function:

```
"slots": {
   "deliveryTime": "22:00"
}
```

For more information about the data sent from Amazon Lex to a Lambda function, see [Input Event Format](lambda-input-response-format.md#using-lambda-input-event-format)\.