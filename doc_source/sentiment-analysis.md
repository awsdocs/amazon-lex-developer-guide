# Sentiment Analysis<a name="sentiment-analysis"></a>

You can use sentiment analysis to determine the sentiments expressed in a user utterance\. With the sentiment information you can manage conversation flow or perform post\-call analysis\. For example, if the user sentiment is negative you can create a flow to hand over a conversation to a human agent\.

Amazon Lex integrates with Amazon Comprehend to detect user sentiment\. The response from Amazon Comprehend indicates whether the overall sentiment of the text is positive, neutral, negative, or mixed\. The response contains the most likely sentiment for the user utterance and the scores for each of the sentiment categories\. The score represents the likelihood that the sentiment was correctly detected\.

 You enable sentiment analysis for a bot using the console or by using the Amazon Lex API\. On the Amazon Lex console, choose the **Settings** tab for your bot, then set the **Sentiment Analysis** option to **Yes**\. If you are using the API, call the [PutBot](API_PutBot.md) operation with the `detectSentiment` field set to `true`\. 

When sentiment analysis is enabled, the response from the [PostContent](API_runtime_PostContent.md) and [PostText](API_runtime_PostText.md) operations return a field called `sentimentResponse` in the bot response with other metadata\. The `sentimentResponse` field has two fields, `SentimentLabel` and `SentimentScore`, that contain the result of the sentiment analysis\. If you are using a Lambda function, the `sentimentResponse` field is included in the event data sent to your function\.

The following is an example of the `sentimentResponse` field returned as part of the `PostText` or `PostContent` response\. The `SentimentScore` field is a string that contains the scores for the response\.

```
{
    "SentimentScore": 
        "{
        Mixed: 0.030585512690246105,
        Positive: 0.94992071056365967,
        Neutral: 0.0141543131828308,
        Negative: 0.00893945890665054
        }",
    "SentimentLabel": "POSITIVE"
}
```

Amazon Lex calls Amazon Comprehend on your behalf to determine the sentiment in every utterance processed by the bot\. By enabling sentiment analysis, you agree to the service terms and agreements for Amazon Comprehend\. For more information about pricing for Amazon Comprehend, see [Amazon Comprehend Pricing](http://aws.amazon.com/comprehend/pricing/)\.

For more information about how Amazon Comprehend sentiment analysis works, see [ Determine the Sentiment ](https://docs.aws.amazon.com/comprehend/latest/dg/how-sentiment.html) in the *Amazon Comprehend Developer Guide*\.