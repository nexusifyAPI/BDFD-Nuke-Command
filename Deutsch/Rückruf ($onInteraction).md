# 🔄 Rückruf ($onInteraction)

## Trigger:
```
$onInteraction
```

## Code:
```
$nomention
$suppressErrors[❌ Bei der Verarbeitung der Interaktion ist ein Fehler aufgetreten.]

$if[$checkContains[$customID;nuke-]==true]

$if[$checkContains[$customID;-$authorID]==false]
$ephemeral
$sendMessage[❌ Nur wer den !nuke-Befehl ausgeführt hat, kann diese Buttons verwenden.]
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
$sendMessage[❌ Keine ausstehenden Nuke-Daten. Führe zuerst !nuke aus.]
$stop
$endif

$if[$serverChannelExists[$var[c_id]]==false]
$ephemeral
$sendMessage[❌ Der Originalkanal existiert nicht mehr. Nuke kann nicht abgeschlossen werden.]
$stop
$endif

$if[$checkUserPerms[$botID;managechannels]==false]
$ephemeral
$sendMessage[❌ Ich habe keine managechannels-Berechtigung, um den Nuke abzuschließen.]
$stop
$endif

$try

$var[nsfw_final;no]
$if[$var[c_nsfw]==true]
$var[nsfw_final;yes]
$endif

$var[topic_final;]
$if[$var[c_topic]!=Kein Thema]
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

$sendMessage[✅ **Nuke erfolgreich abgeschlossen**

💣 Alter Kanal gelöscht und mit derselben Konfiguration neu erstellt:
**Neuer Kanal:** <#$var[nuevo_canal]>
**Name:** #$var[c_nombre]
**Position:** $var[c_posicion]
**Kategorie:** $if[$var[c_categoria]==none]Keine$else<#$var[c_categoria]>$endif
**NSFW:** $if[$var[c_nsfw]==true]Ja$elseNo$endif
**Slowmode:** $var[c_slowmode]s

Ausgeführt von: <@$authorID>]

$catch

$ephemeral
$sendMessage[❌ Bei der Verarbeitung des Nukes ist ein Fehler aufgetreten: $error[message]

Der Originalkanal wurde NICHT gelöscht. Versuche es erneut.]
$jsonParse[{}]
$setServerVar[NukeData;$jsonStringify]

$endtry

$stop
$endif

$if[$checkContains[$customID;rechazar]==true]

$jsonParse[{}]
$setServerVar[NukeData;$jsonStringify]

$sendMessage[❌ **Nuke abgebrochen**

Der Kanal wurde nicht geändert. Du kannst !nuke jederzeit erneut ausführen.]

$stop
$endif

$endif
```
