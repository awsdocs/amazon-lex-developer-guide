# AMAZON\.KendraSearchIntent<a name="built-in-intent-kendra-search"></a>

To search documents that you have indexed with Amazon Kendra, use the `AMAZON.KendraSearchIntent` intent\. When Amazon Lex can't determine the next action in a conversation with the user, it triggers the search intent\.

Amazon Kendra is a machine\-learning\-based search service that indexes natural language documents such as PDF documents or Microsoft Word files\. It can search indexed documents and return the following types of responses to a question:
+ An answer 
+ An entry from a FAQ that might answer the question
+ A document that is related to the question

For an example of using the `AMAZON.KendraSearchIntent`, see [Example: Creating a FAQ Bot for an Amazon Kendra Index](faq-bot-kendra-search.md)\.

If you configure an `AMAZON.KendraSearchIntent` intent for your bot, Amazon Lex calls the intent whenever it can't determine the user utterance for a slot or intent\. For example, if your bot is eliciting a response for a slot type called "pizza topping" and the user says "What is a pizza?," Amazon Lex calls the `AMAZON.KendraSearchIntent` to handle the question\. If there is no response from Amazon Kendra, the conversation continues as configured in the bot\.

When you use both the `AMAZON.KendraSearchIntent` and the `AMAZON.FallbackIntent` in the same bot, Amazon Lex uses the intents as follows:

1. Amazon Lex calls the `AMAZON.KendraSearchIntent`\. The intent calls the Amazon Kendra `Query` operation\.

1. If Amazon Kendra returns a response, Amazon Lex displays the result to the user\.

1. If there is no response from Amazon Kendra, Amazon Lex re\-prompts the user\. The next action depends on response from the user\.
   + If the response from the user contains an utterance that Amazon Lex recognizes, such as filling a slot value or confirming an intent, the conversation with the user proceeds as configured for the bot\.
   + If the response from the user does not contain an utterance that Amazon Lex recognizes, Amazon Lex makes another call to the `Query` operation\.

1. If there is no response after the configured number of retries, Amazon Lex calls the `AMAZON.FallbackIntent` and ends the conversation with the user\.

There are three ways to use the `AMAZON.KendraSearchIntent` to make a request to Amazon Kendra:
+ Let the search intent make the request for you\. Amazon Lex calls Amazon Kendra with the user's utterance as the search string\. When you create the intent, you can define a query filter string that limits the number of responses that Amazon Kendra returns\. Amazon Lex uses the filter in the query request\.
+ Add additional query parameters to the request using your dialog Lambda function\. You add a `kendraQueryFilterString` field that contains Amazon Kendra query parameters to the `delegate` dialog action\. When you add query parameters to the request with the Lambda function, they take precedence over the query filter that you defined when you created the intent\.
+ Create a new query using the dialog Lambda function\. You can create a complete Amazon Kendra query request that Amazon Lex sends\. You specify the query in the `kendraQueryRequestPayload` field in the `delegate` dialog action\. The `kendraQueryRequestPayload` field takes precedence over the `kendraQueryFilterString` field\.

To specify the `queryFilterString` parameter when you create a bot, or to specify the `kendraQueryFilterString` field when you call the `delegate` action in a dialog Lambda function, you specify a string that is used as the attribute filter for the Amazon Kendra query\. If the string isn't a valid attribute filter, you'll get an `InvalidBotConfigException` exception at runtime\. For more information about attribute filters, see [Using document attributes to filter queries](https://docs.aws.amazon.com/kendra/latest/dg/filtering.html#search-filtering) in the *Amazon Kendra Developer Guide*\.

To have control over the query that Amazon Lex sends to Amazon Kendra, you can specify a query in the `kendraQueryRequestPayload`field in your dialog Lambda function\. If the query isn't valid, Amazon Lex returns an `InvalidLambdaResponseException` exception\. For more information, see the [Query operation](https://docs.aws.amazon.com/kendra/latest/dg/API_Query.html) in the *Amazon Kendra Developer Guide*\.

For an example of how to use the `AMAZON.KendraSearchIntent`, see [Example: Creating a FAQ Bot for an Amazon Kendra Index](faq-bot-kendra-search.md)\.

## IAM Policy for Amazon Kendra Search<a name="kendra-search-iam"></a>

To use the `AMAZON.KendraSearchIntent` intent, you must use a role that provides AWS Identity and Access Management \(IAM\) policies that enable Amazon Lex to assume a runtime role that has permission to call the Amazon Kendra `Query` intent\. The IAM settings that you use depend on whether you create the `AMAZON.KendraSearchIntent` using the Amazon Lex console, or using an AWS SDK or the AWS Command Line Interface \(AWS CLI\)\. When you use the console, you can choose between adding permission to call Amazon Kendra to the Amazon Lex service\-linked role or using a role specifically for calling the Amazon Kendra `Query` operation\. When you use the AWS CLI or an SDK to create the intent, you must use a role specifically for calling the `Query` operation\.

### Attaching Permissions<a name="kendra-iam-attach"></a>

You can use the console to attach permissions to access the Amazon Kendra `Query` operation to the default Amazon Lex service\-linked role\. When you attach permissions to the service\-linked role, you don't have to create and manage a runtime role specifically to connect to the Amazon Kendra index\.

The user, role, or group that you use to access the Amazon Lex console must have permissions to manage role policies\. Attach the following IAM policy to the console access role\. When you grant these permissions, the role has permissions to change the existing service\-linked role policy\. 

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "iam:AttachRolePolicy",
                "iam:PutRolePolicy",
                "iam:GetRolePolicy"
            ],
            "Resource": "arn:aws:iam::*:role/aws-service-role/lex.amazonaws.com/AWSServiceRoleForLexBots"
        },
        {
            "Effect": "Allow",
            "Action": "iam:ListRoles",
            "Resource": "*"
        }
    ]
}
```

### Specifying a Role<a name="kendra-iam-role"></a>

You can use the console, the AWS CLI, or the API to specify a runtime role to use when calling the Amazon Kendra `Query` operation\. 

The IAM user, role, or group that you use to specify the runtime role must have the `iam:PassRole` permission\. The following policy defines the permission\. You can use the `iam:AssociatedResourceArn` and `iam:PassedToService` condition context keys to further limit the scope of the permissions\. For more information, see [ IAM and AWS STS Condition Context Keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_iam-condition-keys.html) in the *AWS Identity and Access Management User Guide*\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "iam:PassRole",
            "Resource": "arn:aws:iam::account:role/role"
        }
    ]
}
```

The runtime role that Amazon Lex needs to use to call Amazon Kendra must have the `kendra:Query` permissions\. When you use an existing IAM role for permission to call the Amazon Kendra `Query` operation, the role must have the following policy attached\.

You can use the IAM console, the IAM API, or the AWS CLI to create a policy and attach it to a role\. These instructions use the AWS CLI to create the role and policies\.

**Note**  
The following code is formatted for Linux and MacOS\. For Windows, replace the Linux line continuation character \(\\\) with a caret \(^\)\.

**To add Query operation permission to a role**

1. Create a document called **KendraQueryPolicy\.json** in the current directory, add the following code to it, and save it

   ```
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Effect": "Allow",
               "Action": [
                   "kendra:Query"
               ],
               "Resource": [
                   "arn:aws:kendra:region:account:index/index ID"
               ]
           }
       ]
   }
   ```

1. In the AWS CLI, run the following command to create the IAM policy for running the Amazon Kendra `Query` operation\.

   ```
   aws iam create-policy \
       --policy-name query-policy-name \
       --policy-document file://KendraQueryPolicy.json
   ```

1. Attach the policy to the IAM role that you are using to call the `Query` operation\.

   ```
   aws iam attach-role-policy \
       --policy-arn arn:aws:iam::account-id:policy/query-policy-name
       --role-name role-name
   ```

You can choose to update the Amazon Lex service\-linked role or to use a role that you created when you create the `AMAZON.KendraSearchIntent` for your bot\. The following procedure shows how to choose the IAM role to use\.

**To specify the runtime role for AMAZON\.KendraSearchIntent**

1. Sign in to the AWS Management Console and open the Amazon Lex console at [https://console\.aws\.amazon\.com/lex/](https://console.aws.amazon.com/lex/)\.

1. Choose the bot that you want to add the `AMAZON.KendraSearchIntent` to\.

1. Choose the plus \(\+\) next to **Intents**\.

1. In **Add intent**, choose **Search existing intents**\.

1. In **Search intents**, enter **AMAZON\.KendraSearchIntent** and then choose **Add**\.

1. In **Copy built\-in intent**, enter a name for the intent, such as **KendraSearchIntent**, and then choose **Add**\.

1. Open the **Amazon Kendra query** section\.

1. For **IAM role** choose one of the following options:
   + To update the Amazon Lex service\-linked role to enable your bot to query Amazon Kendra indexes, choose **Add Amazon Kendra permissions**\.
   + To use a role that has permission to call the Amazon Kendra `Query` operation, choose **Use an existing role**\.

## Using Request and Session Attributes as Filters<a name="kendra-search-filter"></a>

To filter the response from Amazon Kendra to items related to current conversation, use session and request attributes as filters by adding the `queryFilterString` parameter when you create your bot\. You specify a placeholder for the attribute when you create the intent, and then Amazon Lex substitutes a value before it calls Amazon Kendra\. For more information about request attributes, see [Setting Request Attributes](context-mgmt.md#context-mgmt-request-attribs)\. For more information about session attributes, see [Setting Session Attributes](context-mgmt.md#context-mgmt-session-attribs)\.

The following is an example of a `queryFilterString` parameter that uses a session attribute called `"DocumentType"` to filter the Amazon Kendra query\.

```
"{\"equalsTo\": {\"key\": \"Type\", \"value\": {\"stringValue\": \"[DocumentType]\"}}}"
```

The following is an example of a `queryFilterString` parameter that uses a request attribute called `"DepartmentName"` to filter the Amazon Kendra query\.

```
"{\"equalsTo\": {\"key\": \"Department\", \"value\": {\"stringValue\": \"((DepartmentName))\"}}}"
```

## Using the Search Response<a name="kendra-search-response"></a>

Amazon Kendra returns the response to a search in the intent's `conclusion` statement\. The intent must have a `conclusion` statement unless a fulfillment Lambda function produces a conclusion message\.

Amazon Kendra has four types of responses\. 
+ `x-amz-lex:kendra-search-response-question_answer-question-<N>` – The question from a FAQ that matches the search\.
+ `x-amz-lex:kendra-search-response-question_answer-answer-<N>` – The answer from a FAQ that matches the search\.
+ `x-amz-lex:kendra-search-response-document-<N>` – An excerpt from a document in the index that is related to the text of the utterance\.
+ `x-amz-lex:kendra-search-response-answer-<N>` – An excerpt from a document in the index that answers the question\.

The responses are returned in `request` attributes\. There can be up to five responses for each attribute, numbered 1 through 5\. For more information about responses, see [Types of response](https://docs.aws.amazon.com/kendra/latest/dg/response-types.html) in the *Amazon Kendra Developer Guide*\. 

The `conclusion` statement must have one or more message groups\. Each message group contains one or more messages\. Each message can contain one or more placeholder variables that are replaced by request attributes in the response from Amazon Kendra\. There must be at least one message in the message group where all of the variables in the message are replaced by request attribute values in the runtime response, or there must be a message in the group with no placeholder variables\. The request attributes are set off with double parentheses \("\(\(" "\)\)"\)\. The following message group messages match any response from Amazon Kendra:
+ “I found a FAQ question for you: \(\(x\-amz\-lex:kendra\-search\-response\-question\_answer\-question\-1\)\), and the answer is \(\(x\-amz\-lex:kendra\-search\-response\-question\_answer\-answer\-1\)\)”
+ “I found an excerpt from a helpful document: \(\(x\-amz\-lex:kendra\-search\-response\-document\-1\)\)”
+ “I think the answer to your questions is \(\(x\-amz\-lex:kendra\-search\-response\-answer\-1\)\)”

## Using a Lambda Function to Manage the Request and Response<a name="kendra-search-lambda"></a>

The `AMAZON.KendraSearchIntent` intent can use your dialog code hook and fulfillment code hook to manage the request to Amazon Kendra and the response\. Use the dialog code hook Lambda function when you want to modify the query that you send to Amazon Kendra, and the fulfillment code hook Lambda function when you want to modify the response\.

### Creating a Query with the Dialog Code Hook<a name="kendra-search-lambda-dialog"></a>

You can use the dialog code hook to create a query to send to Amazon Kendra\. Using the dialog code hook is optional\. If you don't specify a dialog code hook, Amazon Lex constructs a query from the user utterance and uses the `queryFilterString` that you provided when you configured the intent, if you provided one\.

You can use two fields in the dialog code hook response to modify the request to Amazon Kendra:
+ `kendraQueryFilterString` – Use this string to specify attribute filters for the Amazon Kendra request\. You can filter the query using any of the index fields defined in your index\. For the structure of the filter string, see [Using document attributes to filter queries](https://docs.aws.amazon.com/kendra/latest/dg/filtering.html#search-filtering) in the *Amazon Kendra Developer Guide*\. If the specified filter string isn't valid, you will get an `InvalidLambdaResponseException` exception\. The `kendraQueryFilterString` string overrides any query string specified in the `queryFilterString` configured for the intent\.
+ `kendraQueryRequestPayload` – Use this string to specify an Amazon Kendra query\. Your query can use any of the features of Amazon Kendra\. If you don't specify a valid query, you get a `InvalidLambdaResponseException` exception\. For more information, see [Query](https://docs.aws.amazon.com/kendra/latest/dg/API_Query.html) in the *Amazon Kendra Developer Guide*\.

After you have created the filter or query string, you send the response to Amazon Lex with the `dialogAction` field of the response set to `delegate`\. Amazon Lex sends the query to Amazon Kendra and then returns the query response to the fulfillment code hook\.

### Using the Fulfillment Code Hook for the Response<a name="kendra-search-lambda-fulfillment"></a>

After Amazon Lex sends a query to Amazon Kendra, the query response is returned to the `AMAZON.KendraSearchIntent` fulfillment Lambda function\. The input event to the code hook contains the complete response from Amazon Kendra\. The query data is in the same structure as the one returned by the Amazon Kendra `Query` operation\. For more information, see [ Query response syntax](https://docs.aws.amazon.com/kendra/latest/dg/API_Query.html#API_Query_ResponseSyntax) in the *Amazon Kendra Developer Guide*\.

The fulfillment code hook is optional\. If one does not exist, or if the code hook doesn't return a message in the response, Amazon Lex uses the `conclusion` statement for responses\.