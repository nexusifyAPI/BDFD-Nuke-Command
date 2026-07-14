# 💣 Hauptbefehl

## Trigger:
```
!nuke
```

## Code:
```
$nomention
$allowMention
$suppressErrors[❌ Beim Vorbereiten des Nukes ist ein Fehler aufgetreten. Überprüfe die Bot-Berechtigungen und versuche es erneut.]

$onlyPerms[managechannels;❌ Du hast keine **Kanäle verwalten**-Berechtigung, um diesen Befehl zu verwenden.]

$onlyBotPerms[managechannels;sendmessages;embedlinks;❌ Ich habe nicht die erforderlichen Berechtigungen (managechannels, sendmessages, embedlinks).]

$var[canal;$mentionedChannels[1;yes]]

$if[$serverChannelExists[$var[canal]]==false]
$sendMessage[❌ Der erwähnte Kanal existiert nicht auf diesem Server.]
$stop
$endif

$var[tipo;$channelType[$var[canal]]]
$if[$var[tipo]==category]
$sendMessage[❌ Du kannst keine Kategorie nuked. Nur Text-, Sprach-, Bühnen- oder Forumskanäle.]
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
$var[topic;Kein Thema]
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

$title[💣 Nuke-Bestätigung]
$description[
⚠️ **Bist du sicher, dass du diesen Kanal nuked willst?**

**Kanal:** <#$var[canal]> (#$var[nombre])
**Typ:** $var[tipo]
**Position:** $var[posicion]
**Kategorie:** $if[$var[categoria]==]Keine$else<#$var[categoria]>$endif
**NSFW:** $if[$var[nsfw]==true]Ja$elseNo$endif
**Slowmode:** $var[slowmode] Sekunden

📋 **Die gesamte Konfiguration wird beim Neuerstellen des Kanals erhalten.**

 Nur du kannst diese Buttons klicken.
]
$color[#ED4245]
$footer[💡 Nur wer den Befehl ausgeführt hat, kann bestätigen]
$addTimestamp

$addButton[no;nuke-aceptar-$authorID;✅ Akzeptieren;success;no;]
$addButton[no;nuke-rechazar-$authorID;❌ Abbrechen;danger;no;]
```
