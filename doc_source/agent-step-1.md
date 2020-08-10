# Step 1: Create an Amazon Kendra Index<a name="agent-step-1"></a>

Begin by creating an Amazon Kendra index of documents that answer customer questions\. An index provides a search API for client queries\. You create the index from source documents\. Amazon Kendra returns answers it finds in indexed documents to the bot, which displays them to the agent\.

The quality and accuracy of the responses suggested by Amazon Kendra depend on the documents that you index\. Documents should include files that are frequently accessed by the agent and must be stored in an S3 bucket\. For this tutorial, use the documents available from link\. You can index unstructured and semi\-structured data in \.html, Microsoft Office \(\.doc, \.ppt\), PDF, and text formats\. 

To create an Amazon Kendra index, see [Getting started with an S3 bucket \(console\)](https://docs.aws.amazon.com/kendra/latest/dg/gs-console.html) in the *Amazon Kendra Developer Guide*\.

To add questions and answers \(FAQs\) that help answer customer queries, see [Adding questions and answers](https://docs.aws.amazon.com/kendra/latest/dg/in-creating-faq.html) in the *Amazon Kendra Developer Guide*\. You can use the FAQ file available at [https://github\.com/awsdocs/amazon\-lex\-developer\-guide/blob/master/example\_apps/agent\_assistance\_bot/ ](https://github.com/awsdocs/amazon-lex-developer-guide/blob/master/example_apps/agent_assistance_bot/)

## Next step<a name="agent-step-1-next"></a>

[Step 2: Create an Amazon Lex Bot](agent-step-2.md)