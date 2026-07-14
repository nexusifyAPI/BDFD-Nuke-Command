# 💣 Comando Principale

## Trigger:
```
!nuke
```

## Codice:
```
$nomention
$allowMention
$suppressErrors[❌ Si è verificato un errore durante la preparazione del nuke. Controlla i permessi del bot e riprova.]

$onlyPerms[managechannels;❌ Non hai il permesso di **Gestisci Canali** per usare questo comando.]

$onlyBotPerms[managechannels;sendmessages;embedlinks;❌ Non ho i permessi necessari (managechannels, sendmessages, embedlinks).]

$var[canal;$mentionedChannels[1;yes]]

$if[$serverChannelExists[$var[canal]]==false]
$sendMessage[❌ Il canale menzionato non esiste in questo server.]
$stop
$endif

$var[tipo;$channelType[$var[canal]]]
$if[$var[tipo]==category]
$sendMessage[❌ Non puoi fare nuke a una categoria. Solo a canali di testo, voce, palco o forum.]
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
$var[topic;Senza argomento]
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

$title[💣 Conferma Nuke]
$description[
⚠️ **Sei sicuro di voler fare nuke a questo canale?**

**Canale:** <#$var[canal]> (#$var[nombre])
**Tipo:** $var[tipo]
**Posizione:** $var[posicion]
**Categoria:** $if[$var[categoria]==]Nessuna$else<#$var[categoria]>$endif
**NSFW:** $if[$var[nsfw]==true]Sì$elseNo$endif
**Slowmode:** $var[slowmode] secondi

📋 **Tutta la configurazione verrà conservata durante la ricreazione del canale.**

 Solo tu puoi premere questi pulsanti.
]
$color[#ED4245]
$footer[💡 Solo chi ha eseguito il comando può confermare]
$addTimestamp

$addButton[no;nuke-aceptar-$authorID;✅ Accetta;success;no;]
$addButton[no;nuke-rechazar-$authorID;❌ Annulla;danger;no;]
```
