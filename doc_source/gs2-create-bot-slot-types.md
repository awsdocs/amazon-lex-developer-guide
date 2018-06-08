# Create Slot Types<a name="gs2-create-bot-slot-types"></a>

Create the slot types, or parameter values, that the `OrderPizza` intent uses\.

**To create slot types**

1. <a name="slotTypeStart"></a>In the left menu, choose the plus sign \(\+\) next to **Slot types**\.

1. In the **Add slot type** dialog box, add the following: 
   + **Slot type name** – Crusts
   + **Description** – Available crusts
   + Choose **Restrict to Slot values and Synonyms**
   + **Value** – Type **thick**\. Press tab and in the **Synonym** field type **stuffed**\. Choose the plus sign \(\+\)\. Type **thin** and then choose the plus sign \(\+\) again\.

   The dialog should look like this:  
![\[The edit slot type dialog box.\]](http://docs.aws.amazon.com/lex/latest/dg/images/gs1-25a.png)

1. Choose **Add slot to intent**\.

1. <a name="slotTypeFinish"></a>On the **Intent** page, choose **Required**\. Change the name of the slot from **slotOne** to **crust**\. Change the prompt to **What kind of crust would you like?**

1. Repeat [Step 1](#slotTypeStart) through [Step 4](#slotTypeFinish) using the values in the following table:    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lex/latest/dg/gs2-create-bot-slot-types.html)

## Next Step<a name="gs2-next-step-configure-intent"></a>

[Configure the Intent](gs2-create-bot-configure-intent.md)