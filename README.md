# 💣 Nuke Command for BDFD

A complete Nuke command for **Bot Designer for Discord** that deletes and recreates a channel while preserving its configuration (name, position, category, topic, NSFW, and slowmode).

## 🌍 Available Languages

Choose your preferred language folder:

| Folder | Language | README file |
|--------|----------|-------------|
| `Español/` | 🇪🇸 Spanish | `LEEME.md` |
| `English/` | 🇬🇧 English | `README.md` |
| `Deutsch/` | 🇩🇪 German | `LIESMICH.md` |
| `Italiano/` | 🇮🇹 Italian | `LEGGIMI.md` |
| `Português/` | 🇵🇹 Portuguese | `LEIAME.md` |

## 📋 How It Works

### 1. Create the variable
In your BDFD bot, go to **Variables** and create:

| Name | Default value |
|------|---------------|
| `NukeData` | `{}` |

### 2. Create 2 commands
Each language folder contains 2 files:
- **Main Command** → Trigger: `!nuke`
- **Callback** → Trigger: `$onInteraction` (without brackets)

### 3. Requirements
- **Script mode:** BDScript 2 (mandatory)
- **Bot permissions:** `managechannels`, `sendmessages`, `embedlinks`
- **User permissions:** `managechannels`

### 4. Usage
```
!nuke           → Nuke the current channel
!nuke #channel  → Nuke the mentioned channel
```

The bot will show a confirmation embed with **Accept** and **Cancel** buttons. Only the user who ran the command can click them.

## ✨ Features
- ✅ Channel configuration preservation (name, position, category, topic, NSFW, slowmode)
- ✅ Button confirmation restricted to the author
- ✅ Robust error handling with `$try`/`$catch`
- ✅ Bot and user permission verification
- ✅ 100% JSON storage (1 variable, no global variables)
- ✅ Available in 5 languages

## ⚠️ Important Notes
- The `$onInteraction` callback must be created **without brackets** (without ID)
- Only **one** `$onInteraction` command without ID can exist per bot
- If you already have one, integrate the code using `$if` conditionals

---

*For detailed instructions in your language, see the README file inside each language folder.*
