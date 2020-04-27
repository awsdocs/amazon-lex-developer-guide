# Tagging Resources \(AWS CLI\)<a name="tags-cli"></a>

You can use the AWS CLI to manage tags on a bot, a bot alias, or a bot channel resource\. You can add tags when you create a bot or a bot alias, or you can add, modify, or remove tags from a bot, a bot alias, or a bot channel\.

All of the examples are formatted for Linux and macOS\. To use the command in Windows, replace the Linux continuation character \(\\\) with a caret \(^\)\.

**To add a tag when you create a bot**
+ The following abbreviated `put-bot` AWS CLI command shows the parameters that you must use to add a tag when you create a bot\. To actually create a bot, you must supply other parameters\. For more information, see [Step 4: Getting Started \(AWS CLI\)](gs-cli.md)\.

  ```
  aws lex-models put-bot \
      --tags '[{"key": "key1", "value": "value1"}, \
               {"key": "key2", "value": "value2"}]'
  ```

**To add a tag when you create a bot alias**
+ The following abbreviated `put-bot-alias` AWS CLI command shows the parameters that you must use to add a tag when you create a bot alias\. To actually create a bot alias, you must supply other parameters\. For more information, see [Exercise 5: Create an Alias \(AWS CLI\)](gs-cli-create-alias.md)\.

  ```
  aws lex-models put-bot \
      --tags '[{"key": "key1", "value": "value1"}, \
               {"key": "key2", "value": "value2"}]"
  ```

**To list tags on a resource**
+ Use the `list-tags-for-resource` AWS CLI command to show the resources associated with a bot, bot alias, bot channel\. 

  ```
  aws lex-models list-tags-for-resource \
      --resource-arn bot, bot alias, or bot channel ARN
  ```

**To add or modify tags on a resource**
+ Use the `tag-resource` AWS CLI command to add or modify a bot, bot alias, or bot channel\.

  ```
  aws lex-models tag-resource \
      --resource-arn bot, bot alias, or bot channel ARN \
      --tags '[{"key": "key1", "value": "value1"}, \
               {"key": "key2", "value": "value2"}]'
  ```

**To remove tags from a resource**
+ Use the `untag-resource` AWS CLI command to remove tags from a bot, bot alias, or bot channel\.

  ```
  aws lex-models untag-resource \
      --resource-arn bot, bot alias, or bot channel ARN \
      --tag-keys '["key1", "key2"]'
  ```