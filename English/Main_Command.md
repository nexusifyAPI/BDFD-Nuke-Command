# 💣 Main Command

## Trigger:
```
!nuke
```

## Code:
```
$nomention
$allowMention
$suppressErrors[❌ An error occurred while preparing the nuke. Check the bot permissions and try again.]

$onlyPerms[managechannels;❌ You don't have **Manage Channels** permission to use this command.]

$onlyBotPerms[managechannels;sendmessages;embedlinks;❌ I don't have the necessary permissions (managechannels, sendmessages, embedlinks).]

$var[canal;$mentionedChannels[1;yes]]

$if[$serverChannelExists[$var[canal]]==false]
$sendMessage[❌ The mentioned channel doesn't exist in this server.]
$stop
$endif

$var[tipo;$channelType[$var[canal]]]
$if[$var[tipo]==category]
$sendMessage[❌ You can't nuke a category. Only text, voice, stage or forum channels.]
$stop
$endif

$var[nombre;$channelName[$var[canal]]]
$var[posicion;$channelPosition[$var[canal]]]

$var[categoria;$parentID[$var[canal]]]
$if[$var[categoria]==]
$var[categoria;none]
$endif

$var[topic;$channelTopic[$var[canal]]]
$if[$var[topic]==]
$var[topic;No topic]
$endif

$var[nsfw;$isNSFW[$var[canal]]]
$var[slowmode;$getSlowmode[$var[canal]]]

$jsonParse[{}]
$jsonSetString[canal_id;$var[canal]]
$jsonSetString[canal_nombre;$var[nombre]]
$jsonSetString[canal_tipo;$var[tipo]]
$jsonSetString[canal_posicion;$var[posicion]]
$jsonSetString[canal_categoria;$var[categoria]]
$jsonSetString[canal_topic;$var[topic]]
$jsonSetString[canal_nsfw;$var[nsfw]]
$jsonSetString[canal_slowmode;$var[slowmode]]
$jsonSetString[autor_id;$authorID]
$jsonSetString[mensaje_id;none]
$setUserVar[NukeData;$jsonStringify]

$title[💣 Nuke Confirmation]
$description[
⚠️ **Are you sure you want to nuke this channel?**

**Channel:** <#$var[canal]> (#$var[nombre])
**Type:** $var[tipo]
**Position:** $var[posicion]
**Category:** $if[$var[categoria]==]None$else<#$var[categoria]>$endif
**NSFW:** $if[$var[nsfw]==true]Yes$elseNo$endif
**Slowmode:** $var[slowmode] seconds

📋 **All configuration will be preserved when recreating the channel.**

 Only you can click these buttons.
]
$color[#ED4245]
$footer[💡 Only the user who ran the command can confirm]
$addTimestamp

$addButton[no;nuke-aceptar-$authorID;✅ Accept;success;no;]
$addButton[no;nuke-rechazar-$authorID;❌ Cancel;danger;no;]
```
