# 🔄 Callback ($onInteraction)

## Disparador:
```
$onInteraction
```

## Código:
```
$nomention
$suppressErrors[❌ Ha ocurrido un error al procesar la interacción.]

$if[$checkContains[$customID;nuke-]==true]

$if[$checkContains[$customID;-$authorID]==false]
$ephemeral
$sendMessage[❌ Solo quien ejecutó el comando !nuke puede usar estos botones.]
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
$sendMessage[❌ No hay datos de nuke pendientes. Ejecuta !nuke primero.]
$stop
$endif

$if[$serverChannelExists[$var[c_id]]==false]
$ephemeral
$sendMessage[❌ El canal original ya no existe. No se puede completar el nuke.]
$stop
$endif

$if[$checkUserPerms[$botID;managechannels]==false]
$ephemeral
$sendMessage[❌ No tengo permiso de managechannels para completar el nuke.]
$stop
$endif

$try

$var[nsfw_final;no]
$if[$var[c_nsfw]==true]
$var[nsfw_final;yes]
$endif

$var[topic_final;]
$if[$var[c_topic]!=Sin topic]
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

$sendMessage[✅ **Nuke completado correctamente**

💣 Canal antiguo eliminado y recreado con la misma configuración:
**Nuevo canal:** <#$var[nuevo_canal]>
**Nombre:** #$var[c_nombre]
**Posición:** $var[c_posicion]
**Categoría:** $if[$var[c_categoria]==none]Ninguna$else<#$var[c_categoria]>$endif
**NSFW:** $if[$var[c_nsfw]==true]Sí$elseNo$endif
**Slowmode:** $var[c_slowmode]s

Ejecutado por: <@$authorID>]

$catch

$ephemeral
$sendMessage[❌ Ha ocurrido un error al procesar el nuke: $error[message]

El canal original NO ha sido eliminado. Inténtalo de nuevo.]
$jsonParse[{}]
$setUserVar[NukeData;$jsonStringify]

$endtry

$stop
$endif

$if[$checkContains[$customID;rechazar]==true]

$jsonParse[{}]
$setUserVar[NukeData;$jsonStringify]

$sendMessage[❌ **Nuke cancelado**

El canal no ha sido modificado. Puedes ejecutar !nuke nuevamente cuando quieras.]

$stop
$endif

$endif
```
