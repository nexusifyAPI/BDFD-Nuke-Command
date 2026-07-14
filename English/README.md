# 💣 Nuke Command — English

## 📋 Instructions

### 1. Create the variable
Go to the **"Variables"** section of your bot in BDFD and create the following variable:

| Name | Default value |
|------|---------------|
| `NukeData` | `{}` |

### 2. Create the commands
In this folder you'll find 2 files with the necessary code:

| File | Trigger | Type |
|------|---------|------|
| `Main_Command.md` | `!nuke` | Command (BDScript 2) |
| `Callback ($onInteraction).md` | `$onInteraction` | Command (BDScript 2) |

### 3. Configuration
- **Script mode:** BDScript 2 (mandatory in both commands)
- **Bot permissions:** `managechannels`, `sendmessages`, `embedlinks`
- **User permissions:** `managechannels`

### 4. Usage
```
!nuke           → Nuke the current channel
!nuke #channel  → Nuke the mentioned channel
```
