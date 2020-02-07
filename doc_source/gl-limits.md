# Quotas<a name="gl-limits"></a>

This section describes current quotas in Amazon Lex\. These quotas are grouped by categories\. 

**Topics**
+ [Runtime Service Quotas](#gl-limits-runtime)
+ [Model Building Quotas](#gl-limits-model-building)

## Runtime Service Quotas<a name="gl-limits-runtime"></a>

In addition to the quotas described in the API reference, note the following:

### API Quotas<a name="gl-limits-runtime-api"></a>
+ Speech input to the [PostContent](API_runtime_PostContent.md) operation can be up to 15 seconds long\.

   
+ In both the runtime API operations [PostContent](API_runtime_PostContent.md) and [PostText](API_runtime_PostText.md), the input text size can be up to 1024 Unicode characters\.

   
+ The maximum size of `PostContent` headers is 16 KB\. The maximum size of request and session headers combined is 12 KB\.

   
+ The maximum input size to a Lambda function is 12 KB\. The maximum output size is 25 KB, of which 12 KB can be session attributes\.

   

### Using the `$LATEST` version<a name="gl-limits-runtime-latest"></a>
+ The `$LATEST` version of your bot should only be used for manual testing\. Amazon Lex limits the number of runtime requests that you can make to the `$LATEST` version of the bot\.

   
+ When you update the `$LATEST` version of the bot, Amazon Lex terminates any in\-progress conversations for any client application using the `$LATEST` version of the bot\. Generally, you should not use the `$LATEST` version of a bot in production because `$LATEST` version can be updated\. You should publish a version and use it instead\.

   
+ When you update an alias, Amazon Lex takes a few minutes to pick up the change\. When you modify the `$LATEST` version of the bot, the change is picked up immediately\.

   

### Session Timeout<a name="gl-limits-runtime-timeout"></a>
+ The session timeout set when the bot was created determines how long the bot retains conversation context, such as current user intent and slot data\.

   
+ After a user starts the conversation with your bot and until the session expires, Amazon Lex uses the same bot version, even if you update the bot alias to point to another version\.

   

## Model Building Quotas<a name="gl-limits-model-building"></a>

Model building refers to creating and managing bots\. This includes creating and managing bots, intents, slot types, slots, and bot channel associations\. 

**Topics**
+ [Bot Quotas](#gl-limits-bots)
+ [Intent Quotas](#gl-limits-intents)
+ [Slot Type Quotas](#gl-limits-slot-type)

### Bot Quotas<a name="gl-limits-bots"></a>
+ You configure prompts and statements throughout the model building API\. Each of these prompts or statements can have up to five messages and each message can contain from 1 to 1000 UTF\-8 characters\. 

   
+ When using message groups you can define up to five message groups for each message\. Each message group can contain a maximum of five messages, and you are limited to 15 messages in all message groups\.

   
+ You can define sample utterances for intents and slots\. You can use a maximum of 200,000 characters for all utterances\.

   
+ Each slot type can define a maximum of 10,000 values and synonyms\. Each bot can contain a maximum of 50,000 slot type values and synonyms\.

   
+ Bot, alias, and bot channel association names are case insensitive at the time of creation\. If you create `PizzaBot` and then try to create `pizzaBot`, you will get an error\. However, when accessing a resource, the resource names are case sensitive, you must specify `PizzaBot` and not `pizzaBot`\. These names must be between 2 and 50 ASCII characters\.

   
+ The maximum number of versions you can publish for all resource types is 100\. Note that there is no versioning for aliases\.

   
+ Within a bot, intent names and slot names must be unique, you can't have an intent and a slot by the same name\. 

   
+ You can create a bot that is configured to support multiple intents\. If two intents have a slot by the same name, then the corresponding slot type must be the same\.

   

  For example, suppose you create a bot to support two intents \(`OrderPizza` and `OrderDrink`\)\. If both these intents have the `size` slot, then the slot type must be the same in both places\.

   

  In addition, the sample utterances you provide for a slot in one of the intents applies to a slot with the same name in other intents\.

   
+ You can associate a maximum of 100 intents with a bot\.

   
+ When you create a bot, you specify a session timeout\. The session timeout can be between one minute and one day\. The default is five minutes\.

   
+ You can create up to five aliases for a bot\.

   
+ You can create up to 100 bots per AWS account\.

   
+ You cannot create multiple intents that extend from the same built\-in intent\.

   

### Intent Quotas<a name="gl-limits-intents"></a>
+ Intent and slot names are case insensitive at the time of creation\. That is, if you create `OrderPizza` intent and then again try to create another `orderPizza` intent, you will get an error\. However, when accessing these resources, the resource names are case sensitive, specify `OrderPizza` and not `orderPizza`\. These names must be between 1 and 100 ASCII characters\.

   
+ An intent can have up to 1,500 sample utterances\. A minimum of one sample utterance is required\. Each sample utterance can be up to 200 UTF\-8 characters long\. You can use up to 200,000 characters for all intent and slot utterances in a bot\. A sample utterance for an intent: 
  + Can refer to zero or more slot names\.
  + Can refer to a slot name only once\.

  For example:

  ```
  I want a pizza
  I want a {pizzaSize} pizza
  I want a {pizzaSize} {pizzaTopping} pizza
  ```

   
+ Although each intent supports up to 1,500 utterances, if you use fewer utterances Amazon Lex may have a better ability to recognize inputs outside your provided set\.

   
+ You can create up to five message groups for each message in an intent\. There can be a total of 15 messages in all message groups for a message\.

   
+ The console can only create message groups for the `conclusionStatement` and `followUpPrompt` messages\. You can create message groups for any other message using the Amazon Lex API\.

   
+ Each slot can have up to 10 sample utterances\. Each sample utterance must refer to the slot name exactly once\. For example:

  ```
  {pizzaSize} please
  ```

   
+  Each bot can have a maximum of 200,000 characters for intent and slot utterances combined\. 

   
+ You cannot provide utterances for intents that extend from built\-in intents\. For all other intents you must provide at least one sample utterance\. Intents contain slots, but the slot level sample utterances are optional\. 

   
+ Built\-in intents 
  + Currently, Amazon Lex does not support slot elicitation for built\-in intents\. You cannot create Lambda functions to return the `ElicitSlot` directive in the response with an intent that is derived from built\-in intents\. For more information, see [Response Format](lambda-input-response-format.md#using-lambda-response-format)\.
  + The service does not support adding sample utterances to built\-in intents\. Similarly, you cannot add or remove slots to built\-in intents\.

   
+ You can create up to 1,000 intents per AWS account\. You can create up to 100 slots in an intent\.

   

### Slot Type Quotas<a name="gl-limits-slot-type"></a>
+ Slot type names are case insensitive at the time of creation\. If you create the `PizzaSize` slot type and then again try to create the `pizzaSize` slot type, you will get an error\. However, when accessing these resources, the resource names are case sensitive \(you must specify `PizzaSize` and not `pizzaSize`\)\. Names must be between 1 and 100 ASCII characters\.

   
+ A custom slot type you create can have a maximum of 10,000 enumeration values and synonyms\. Each value can be up to 140 UTF\-8 characters long\. The enumeration values and synonyms cannot contain duplicates\.

   
+ For a slot type value, where appropriate, specify both upper and lower case\. For example, for a slot type called `Procedure`, if value is `MRI`, specify both "MRI" and "mri" as values\.

   
+ Built\-in slot types – Currently, Amazon Lex doesn't support adding enumeration values or synonyms for the built\-in slot types\. 