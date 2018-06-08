# Amazon Lex API Permissions: Actions, Resources, and Conditions Reference<a name="lex-api-permissions-ref"></a>

Use the following table as a reference when setting up [Access Control](auth-and-access-control.md#access-control) and writing a permissions policy that you can attach to an IAM identity \(an identity\-based policy\)\. The list includes each Amazon Lex API operation, the corresponding action for which you can grant permissions to perform the action, and the AWS resource for which you can grant the permissions\. You specify the actions in the policy's `Action` field, and you specify the resource value in the policy's `Resource` field\. 

To express conditions, you can use AWS\-wide condition keys in your Amazon Lex policies\. For a complete list of AWS\-wide keys, see [Available Keys](http://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#AvailableKeys) in the *IAM User Guide*\. 

**Note**  
To specify an action, use the `lex:` prefix followed by the API operation name, for example, `lex:PostText`\.

If you see an expand arrow \(**↗**\) in the upper\-right corner of the table, you can open the table in a new window\. To close the window, choose the close button \(**X**\) in the lower\-right corner\.


**Amazon Lex API and Required Permissions for Actions**  

| Amazon Lex API Operations | Required Permissions \(API Actions\) | Resources | 
| --- | --- | --- | 
|   [CreateBotVersion](API_CreateBotVersion.md)   | lex:CreateBotVersion |  `arn:aws:lex:region:account-id:bot:bot-name:$LATEST`  | 
|   [CreateIntentVersion](API_CreateIntentVersion.md)   | lex:CreateIntentVersion |  `arn:aws:lex:region:account-id:intent:intent-name:$LATEST`  | 
|   [CreateSlotTypeVersion](API_CreateSlotTypeVersion.md)   | lex:CreateSlotTypeVersion |  `arn:aws:lex:region:account-id:slottype:slottype-name:$LATEST`  | 
|   [DeleteBot](API_DeleteBot.md)   | lex:DeleteBot |  `arn:aws:lex:region:account-id:bot:bot-name:*`  | 
|   [DeleteBotAlias](API_DeleteBotAlias.md)   | lex:DeleteBotAlias |  `arn:aws:lex:region:account-id:bot:bot-name:alias-name`  | 
|   [DeleteBotChannelAssociation](API_DeleteBotChannelAssociation.md)   | lex:DeleteBotChannelAssociation |  `arn:aws:lex:region:account-id:bot-channel:bot-name:alias-name:channel-name`  | 
|   [DeleteBotVersion](API_DeleteBotVersion.md)   | lex:DeleteBotVersion |  `arn:aws:lex:region:account-id:bot:bot-name:version`  | 
|   [DeleteIntent](API_DeleteIntent.md)   | lex:DeleteIntent |  `arn:aws:lex:region:account-id:intent:intent-name:*`  | 
|   [DeleteIntentVersion](API_DeleteIntentVersion.md)   | lex:DeleteIntentVersion |  `arn:aws:lex:region:account-id:intent:intent-name:version`  | 
|   [DeleteSlotType](API_DeleteSlotType.md)   | lex:DeleteSlotType |  `arn:aws:lex:region:account-id:slottype:slottype-name:*`  | 
|   [DeleteSlotTypeVersion](API_DeleteSlotTypeVersion.md)   | lex:DeleteSlotTypeVersion |  `arn:aws:lex:region:account-id:slottype:slottype-name:version`  | 
|  [DeleteUtterances](API_DeleteUtterances.md)   | lex:DeleteUtterances | `arn:aws:lex:region:account-id:bot:bot-name:*` | 
|   [GetBot](API_GetBot.md)   | lex:GetBot |  `arn:aws:lex:region:account-id:bot:bot-name:version`  | 
|   [GetBotAlias](API_GetBotAlias.md)   | lex:GetBotAlias |  `arn:aws:lex:region:account-id:bot:bot-name:alias-name`  | 
|   [GetBotAliases](API_GetBotAliases.md)   | lex:GetBotAliases |  `arn:aws:lex:region:account-id:bot:bot-name:*`  | 
|   [GetBotChannelAssociation](API_GetBotChannelAssociation.md)   | lex:GetBotChannelAssociation |  `arn:aws:lex:region:account-id:bot-channel:bot-name:alias-name:channel-name`  | 
|   [GetBotChannelAssociations](API_GetBotChannelAssociations.md)   | lex:GetBotChannelAssociations |  arn:aws:lex:region:account\-id:bot\-channel:bot\-name:alias\-name:\*  | 
|   [GetBots](API_GetBots.md)   | lex:GetBots |  `arn:aws:lex:region:account-id:bot:*`  | 
|   [GetBotVersions](API_GetBotVersions.md)   | lex:GetBotVersions |  `arn:aws:lex:region:account-id:bot:bot-name:*`  | 
|   [GetBuiltinIntent](API_GetBuiltinIntent.md)   | lex:GetBuiltinIntent |  \*  | 
|   [GetBuiltinIntents](API_GetBuiltinIntents.md)   | lex:GetBuiltinIntents |  \*  | 
|   [GetBuiltinSlotTypes](API_GetBuiltinSlotTypes.md)   | lex:GetBuiltinSlotTypes |  \*  | 
|   [GetExport](API_GetExport.md) \(see note\)   | lex:GetExport |  `arn:aws:lex:region:account-id:bot:bot-name:bot-version`  | 
|   [GetIntent](API_GetIntent.md)   | lex:GetIntent |  `arn:aws:lex:region:account-id:intent:intent-name:version`  | 
|   [GetIntents](API_GetIntents.md)   | lex:GetIntents |  `arn:aws:lex:region:account-id:intent:*`  | 
|   [GetIntentVersions](API_GetIntentVersions.md)   | lex:GetIntentVersions |  `arn:aws:lex:region:account-id:intent:intent-name:*`  | 
|   [GetSlotType](API_GetSlotType.md)   | lex:GetSlotType |  `arn:aws:lex:region:account-id:slottype:slottype-name:version`  | 
|   [GetSlotTypes](API_GetSlotTypes.md)   | lex:GetSlotTypes |  `arn:aws:lex:region:account-id:slottype:*`  | 
|   [GetSlotTypeVersions](API_GetSlotTypeVersions.md)   | lex:GetSlotTypeVersions |  `arn:aws:lex:region:account-id:slottype:slottype-name:*`  | 
| [GetUtterancesView](API_GetUtterancesView.md) | `lex:GetUtterancesView` | `arn:aws:lex:region:account-id:bot:bot-name:version` | 
|   [PostContent](API_runtime_PostContent.md)   | lex:PostContent |  `arn:aws:lex:region:account-id:bot:bot-name:alias`  | 
|   [PostText](API_runtime_PostText.md)   | lex:PostText |  `arn:aws:lex:region:account-id:bot:bot-name:alias-name`  | 
|   [PutBot](API_PutBot.md)   | lex:PutBot |  `arn:aws:lex:region:account-id:bot:bot-name:$LATEST`  | 
|   [PutBotAlias](API_PutBotAlias.md)   | lex:PutBotAlias |  `arn:aws:lex:region:account-id:bot:bot-name:alias-name`  | 
|   [PutIntent](API_PutIntent.md)   | lex:PutIntent |  `arn:aws:lex:region:account-id:intent:intent-name:$LATEST`  | 
|   [PutSlotType](API_PutSlotType.md)   | lex:PutSlotType |  `arn:aws:lex:region:account-id:slottype:slottype-name:$LATEST`  | 

**Note**  
The `GetExport` function checks permission at the bot level and, if authorized, exports all relevant intent and slot type information associated with the specified bot\. GetExport does not check intent\-level and slot type\-level permissions\. 