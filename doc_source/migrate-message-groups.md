# Message groups<a name="migrate-message-groups"></a>

Amazon Lex V2 supports only one message and two alternative messages per message group\. If you have more than three messages per message group in an Amazon Lex V1 bot, only the first three messages are migrated\. To use more messages in a message group, use a Lambda function to output various messages\.