# 💣 Comando Principal

## Gatilho:
```
!nuke
```

## Código:
```
$nomention
$allowMention
$suppressErrors[❌ Ocorreu um erro ao preparar o nuke. Verifique as permissões do bot e tente novamente.]

$onlyPerms[managechannels;❌ Você não tem permissão de **Gerenciar Canais** para usar este comando.]

$onlyBotPerms[managechannels;sendmessages;embedlinks;❌ Não tenho as permissões necessárias (managechannels, sendmessages, embedlinks).]

$var[canal;$mentionedChannels[1;yes]]

$if[$serverChannelExists[$var[canal]]==false]
$sendMessage[❌ O canal mencionado não existe neste servidor.]
$stop
$endif

$var[tipo;$channelType[$var[canal]]]
$if[$var[tipo]==category]
$sendMessage[❌ Você não pode fazer nuke em uma categoria. Apenas em canais de texto, voz, palco ou fórum.]
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
$var[topic;Sem tópico]
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

$title[💣 Confirmação de Nuke]
$description[
⚠️ **Tem certeza de que quer fazer nuke neste canal?**

**Canal:** <#$var[canal]> (#$var[nombre])
**Tipo:** $var[tipo]
**Posição:** $var[posicion]
**Categoria:** $if[$var[categoria]==]Nenhuma$else<#$var[categoria]>$endif
**NSFW:** $if[$var[nsfw]==true]Sim$elseNo$endif
**Slowmode:** $var[slowmode] segundos

📋 **Toda a configuração será preservada ao recriar o canal.**

 Apenas você pode clicar nestes botões.
]
$color[#ED4245]
$footer[💡 Apenas quem executou o comando pode confirmar]
$addTimestamp

$addButton[no;nuke-aceptar-$authorID;✅ Aceitar;success;no;]
$addButton[no;nuke-rechazar-$authorID;❌ Cancelar;danger;no;]
```
