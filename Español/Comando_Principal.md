# 💣 Comando Principal

## Disparador:
```
!nuke
```

## Código:
```
$nomention
$allowMention
$suppressErrors[❌ Ha ocurrido un error al preparar el nuke. Verifica los permisos del bot e inténtalo de nuevo.]

$onlyPerms[managechannels;❌ No tienes permiso de **Gestionar Canales** para usar este comando.]

$onlyBotPerms[managechannels;sendmessages;embedlinks;❌ No tengo los permisos necesarios (managechannels, sendmessages, embedlinks).]

$var[canal;$mentionedChannels[1;yes]]

$if[$serverChannelExists[$var[canal]]==false]
$sendMessage[❌ El canal mencionado no existe en este servidor.]
$stop
$endif

$var[tipo;$channelType[$var[canal]]]
$if[$var[tipo]==category]
$sendMessage[❌ No puedes hacer nuke a una categoría. Solo a canales de texto, voz, escenario o foro.]
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
$var[topic;Sin topic]
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
$setServerVar[NukeData;$jsonStringify]

$title[💣 Confirmación de Nuke]
$description[
⚠️ **¿Estás seguro de que quieres hacer nuke a este canal?**

**Canal:** <#$var[canal]> (#$var[nombre])
**Tipo:** $var[tipo]
**Posición:** $var[posicion]
**Categoría:** $if[$var[categoria]==]Ninguna$else<#$var[categoria]>$endif
**NSFW:** $if[$var[nsfw]==true]Sí$elseNo$endif
**Slowmode:** $var[slowmode] segundos

📋 **Se conservará toda la configuración al recrear el canal.**

 Solo tú puedes pulsar estos botones.
]
$color[#ED4245]
$footer[💡 Solo quien ejecutó el comando puede confirmar]
$addTimestamp

$addButton[no;nuke-aceptar-$authorID;✅ Aceptar;success;no;]
$addButton[no;nuke-rechazar-$authorID;❌ Cancelar;danger;no;]
```
