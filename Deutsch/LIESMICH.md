# 💣 Nuke Befehl — Deutsch

## 📋 Anweisungen

### 1. Variable erstellen
Gehe zum Abschnitt **"Variablen"** deines Bots in BDFD und erstelle die folgende Variable:

| Name | Typ | Standardwert |
|------|-----|--------------|
| `NukeData` | Server | `{}` |

### 2. Befehle erstellen
In diesem Ordner findest du 2 Dateien mit dem notwendigen Code:

| Datei | Trigger | Typ |
|-------|---------|-----|
| `Hauptbefehl.md` | `!nuke` | Command (BDScript 2) |
| `Rückruf ($onInteraction).md` | `$onInteraction` | Command (BDScript 2) |

### 3. Konfiguration
- **Skriptmodus:** BDScript 2 (obligatorisch in beiden Befehlen)
- **Bot-Berechtigungen:** `managechannels`, `sendmessages`, `embedlinks`
- **Benutzerberechtigungen:** `managechannels`

### 4. Verwendung
```
!nuke           → Nuke den aktuellen Kanal
!nuke #kanal    → Nuke den erwähnten Kanal
```
