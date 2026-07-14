# 🔄 Callback ($onInteraction)

## Trigger:
```
$onInteraction
```

## Code:
```
$nomention
$suppressErrors[❌ An error occurred while processing the interaction.]

$if[$checkContains[$customID;nuke-]==true]

$if[$checkContains[$customID;-$authorID]==false]
$ephemeral
$sendMessage[❌ Only the user who ran the !nuke command can use these buttons.]
$stop
$endif

$if[$checkContains[$customID;aceptar]==true]

$jsonParse[$getUserVar[NukeData]]
$var[c_id;$json[canal_id]]
$var[c_nombre;$json[canal_nombre]]
$var[c_tipo;$json[canal_tipo]]
$var[c_posicion;$json[canal_posicion]]
$var[c_categoria;$json[canal_categoria]]
$var[c_topic;$json[canal_topic]]
$var[c_nsfw;$json[canal_nsfw]]
$var[c_slowmode;$json[canal_slowmode]]
$var[c_autor;$json[autor_id]]
$var[c_mensaje;$json[mensaje_id]]

$if[$var[c_id]==]
$ephemeral
$sendMessage[❌ No pending nuke data. Run !nuke first.]
$stop
$endif

$if[$serverChannelExists[$var[c_id]]==false]
$ephemeral
$sendMessage[❌ The original channel no longer exists. Cannot complete the nuke.]
$stop
$endif

$if[$checkUserPerms[$botID;managechannels]==false]
$ephemeral
$sendMessage[❌ I don't have managechannels permission to complete the nuke.]
$stop
$endif

$try

$var[nsfw_final;no]
$if[$var[c_nsfw]==true]
$var[nsfw_final;yes]
$endif

$var[topic_final;]
$if[$var[c_topic]!=No topic]
$var[topic_final;$var[c_topic]]
$endif

$deleteChannels[$var[c_id]]

$if[$var[c_categoria]!=none]
$createChannel[$var[c_nombre];$var[c_tipo];$var[c_categoria]]
$else
$createChannel[$var[c_nombre];$var[c_tipo]]
$endif

$var[nuevo_canal;$findChannel[$var[c_nombre]]]

$replyIn[2s]
$modifyChannel[$var[nuevo_canal];!unchanged;$var[topic_final];$var[nsfw_final];$var[c_posicion];!unchanged]

$if[$var[c_slowmode]>0]
$slowmode[$var[nuevo_canal];$var[c_slowmode]s]
$endif

$jsonParse[{}]
$setUserVar[NukeData;$jsonStringify]

$sendMessage[✅ **Nuke completed successfully**

💣 Old channel deleted and recreated with the same configuration:
**New channel:** <#$var[nuevo_canal]>
**Name:** #$var[c_nombre]
**Position:** $var[c_posicion]
**Category:** $if[$var[c_categoria]==none]None$else<#$var[c_categoria]>$endif
**NSFW:** $if[$var[c_nsfw]==true]Yes$elseNo$endif
**Slowmode:** $var[c_slowmode]s

Executed by: <@$authorID>]

$catch

$ephemeral
$sendMessage[❌ An error occurred while processing the nuke: $error[message]

The original channel has NOT been deleted. Try again.]
$jsonParse[{}]
$setUserVar[NukeData;$jsonStringify]

$endtry

$stop
$endif

$if[$checkContains[$customID;rechazar]==true]

$jsonParse[{}]
$setUserVar[NukeData;$jsonStringify]

$sendMessage[❌ **Nuke cancelled**

The channel has not been modified. You can run !nuke again whenever you want.]

$stop
$endif

$endif
```
