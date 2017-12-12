# Step 6: Update the Intent Configuration to Add an Utterance \(Console\)<a name="gs-bp-utterance"></a>

 The `OrderFlowers` bot is configured with only two utterances\. This provides limited information for Amazon Lex to build a machine learning model that recognizes and responds to the user's intent\. Try typing "I want to order flowers" in the test window\. Amazon Lex doesn’t recognize the text, and responds with "I didn't understand you, what would you like to do?" You can improve the machine learning model by adding more utterances\.

![\[Test window shows missed utterance\]](http://docs.aws.amazon.com/lex/latest/dg/images/gs1-120.png)

Each utterance that you add provides Amazon Lex with more information about how to respond to your users\. You don't need to add an exact utterance, Amazon Lex generalizes from the samples that you provide to recognize both exact matches and similar input\.

**To add an utterance \(console\)**

1. Add the utterance "I want flowers" to the intent by typing it in the **Sample utterances** section of the intent editor, and then clicking the plus icon next to the new utterance\.  
![\[Intent editor with the new utterance.\]](http://docs.aws.amazon.com/lex/latest/dg/images/gs1-130.png)

1.  Build your bot to pick up the change\. Choose **Build**, and then choose **Build** again\. 

1. Test your bot to confirm that it recognized the new utterance \. In the test window, type "I want to order flowers\." Amazon Lex recognizes the phrase and responds with "What type of flowers would you like to order?"\.  
![\[The intent editor recognizes the new utterance.\]](http://docs.aws.amazon.com/lex/latest/dg/images/gs1-140.png)

**Next Step**  
[Step 7 \(Optional\): Clean Up \(Console\)](gs-bp-cleaning-up.md)