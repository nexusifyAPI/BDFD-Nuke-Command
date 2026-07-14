# 🔄 Callback ($onInteraction)

## Trigger:
```
$onInteraction
```

## Codice:
```
$nomention
$suppressErrors[❌ Si è verificato un errore durante l'elaborazione dell'interazione.]

$if[$checkContains[$customID;nuke-]==true]

$if[$checkContains[$customID;-$authorID]==false]
$ephemeral
$sendMessage[❌ Solo chi ha eseguito il comando !nuke può usare questi pulsanti.]
$stop
$endif

$if[$checkContains[$customID;aceptar]==true]

$jsonParse[$getServerVar[NukeData]]
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
$sendMessage[❌ Nessun dato nuke in sospeso. Esegui prima !nuke.]
$stop
$endif

$if[$serverChannelExists[$var[c_id]]==false]
$ephemeral
$sendMessage[❌ Il canale originale non esiste più. Impossibile completare il nuke.]
$stop
$endif

$if[$checkUserPerms[$botID;managechannels]==false]
$ephemeral
$sendMessage[❌ Non ho il permesso managechannels per completare il nuke.]
$stop
$endif

$try

$var[nsfw_final;no]
$if[$var[c_nsfw]==true]
$var[nsfw_final;yes]
$endif

$var[topic_final;]
$if[$var[c_topic]!=Senza argomento]
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
$setServerVar[NukeData;$jsonStringify]

$sendMessage[✅ **Nuke completato con successo**

💣 Canale vecchio eliminato e ricreato con la stessa configurazione:
**Nuovo canale:** <#$var[nuevo_canal]>
**Nome:** #$var[c_nombre]
**Posizione:** $var[c_posicion]
**Categoria:** $if[$var[c_categoria]==none]Nessuna$else<#$var[c_categoria]>$endif
**NSFW:** $if[$var[c_nsfw]==true]Sì$elseNo$endif
**Slowmode:** $var[c_slowmode]s

Eseguito da: <@$authorID>]

$catch

$ephemeral
$sendMessage[❌ Si è verificato un errore durante l'elaborazione del nuke: $error[message]

Il canale originale NON è stato eliminato. Riprova.]
$jsonParse[{}]
$setServerVar[NukeData;$jsonStringify]

$endtry

$stop
$endif

$if[$checkContains[$customID;rechazar]==true]

$jsonParse[{}]
$setServerVar[NukeData;$jsonStringify]

$sendMessage[❌ **Nuke annullato**

Il canale non è stato modificato. Puoi eseguire !nuke di nuovo quando vuoi.]

$stop
$endif

$endif
```
