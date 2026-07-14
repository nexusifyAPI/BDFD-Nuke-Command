# 💣 Comando Nuke — Português

## 📋 Instruções

### 1. Criar a variável
Vá à seção **"Variáveis"** do seu bot no BDFD e crie a seguinte variável:

| Nome | Valor padrão |
|------|---------------|
| `NukeData` | `{}` |

### 2. Criar os comandos
Nesta pasta você encontrará 2 arquivos com o código necessário:

| Arquivo | Gatilho (Trigger) | Tipo |
|---------|-------------------|------|
| `Comando_Principal.md` | `!nuke` | Command (BDScript 2) |
| `Callback ($onInteraction).md` | `$onInteraction` | Command (BDScript 2) |

### 3. Configuração
- **Modo de script:** BDScript 2 (obrigatório em ambos os comandos)
- **Permissões do bot:** `managechannels`, `sendmessages`, `embedlinks`
- **Permissões do usuário:** `managechannels`

### 4. Uso
```
!nuke           → Nuke o canal atual
!nuke #canal    → Nuke o canal mencionado
```
