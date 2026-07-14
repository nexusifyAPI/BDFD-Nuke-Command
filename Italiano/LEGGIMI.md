# 💣 Comando Nuke — Italiano

## 📋 Istruzioni

### 1. Creare la variabile
Vai alla sezione **"Variabili"** del tuo bot in BDFD e crea la seguente variabile:

| Nome | Valore predefinito |
|------|---------------------|
| `NukeData` | `{}` |

### 2. Creare i comandi
In questa cartella troverai 2 file con il codice necessario:

| File | Trigger | Tipo |
|------|---------|------|
| `Comando_Principale.md` | `!nuke` | Command (BDScript 2) |
| `Callback ($onInteraction).md` | `$onInteraction` | Command (BDScript 2) |

### 3. Configurazione
- **Modalità script:** BDScript 2 (obbligatorio in entrambi i comandi)
- **Permessi del bot:** `managechannels`, `sendmessages`, `embedlinks`
- **Permessi dell'utente:** `managechannels`

### 4. Utilizzo
```
!nuke           → Nuke il canale attuale
!nuke #canale   → Nuke il canale menzionato
```
