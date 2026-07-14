# 📋 Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

---

## [1.2.0] - 2026-07-15

### 📄 Added
- **`LICENSE`** file added — project is now licensed under the **MIT License**.
  - Copyright (c) 2026 nexusifyAPI.
  - Allows any use (commercial, modification, distribution, sublicensing) as long as the original copyright notice and credits are preserved.
- **License section** added to the root `README.md` with a summary of the MIT License terms.

### 📊 Files Modified
| File | Changes |
|------|---------|
| `LICENSE` | Created — MIT License with copyright to nexusifyAPI |
| `README.md` | Added License section at the bottom |

---

## [1.1.0] - 2026-07-15

### 🔄 Changed
- **Variable type changed from Server to User**: `$setServerVar` → `$setUserVar` and `$getServerVar` → `$getUserVar` in all code files (Main Command and Callback).
  - This changes the variable scope from server-wide to user-specific.
  - Each user now has their own `NukeData` variable, allowing nukes to be tracked per user.
- **Removed "Type" column** from the variable table in all README files (root + 5 languages).
  - The table now only shows `Name` and `Default value` columns.
  - Applied to: `README.md`, `Español/LEEME.md`, `English/README.md`, `Deutsch/LIESMICH.md`, `Italiano/LEGGIMI.md`, `Português/LEIAME.md`.

### 📄 Added
- **`CHANGELOGS.md`** file created to track all project changes by commit, date (UTC+0), and time.

### 📊 Files Modified
| File | Changes |
|------|---------|
| `README.md` | Removed Type column from variable table |
| `Español/LEEME.md` | Removed Tipo column from variable table |
| `Español/Comando_Principal.md` | `$setServerVar` → `$setUserVar` |
| `Español/Callback ($onInteraction).md` | `$setServerVar` → `$setUserVar`, `$getServerVar` → `$getUserVar` |
| `English/README.md` | Removed Type column from variable table |
| `English/Main_Command.md` | `$setServerVar` → `$setUserVar` |
| `English/Callback ($onInteraction).md` | `$setServerVar` → `$setUserVar`, `$getServerVar` → `$getUserVar` |
| `Deutsch/LIESMICH.md` | Removed Typ column from variable table |
| `Deutsch/Hauptbefehl.md` | `$setServerVar` → `$setUserVar` |
| `Deutsch/Rückruf ($onInteraction).md` | `$setServerVar` → `$setUserVar`, `$getServerVar` → `$getUserVar` |
| `Italiano/LEGGIMI.md` | Removed Tipo column from variable table |
| `Italiano/Comando_Principale.md` | `$setServerVar` → `$setUserVar` |
| `Italiano/Callback ($onInteraction).md` | `$setServerVar` → `$setUserVar`, `$getServerVar` → `$getUserVar` |
| `Português/LEIAME.md` | Removed Tipo column from variable table |
| `Português/Comando_Principal.md` | `$setServerVar` → `$setUserVar` |
| `Português/Callback ($onInteraction).md` | `$setServerVar` → `$setUserVar`, `$getServerVar` → `$getUserVar` |

### 🔧 Technical Details
- **Total replacements**: 25 (`$setServerVar` and `$getServerVar` occurrences across all files)
- **Variable scope**: Changed from Server (shared across all users in a server) to User (unique per user per server)
- **Syntax**: `$setUserVar[Name;Value;(User ID;Guild ID)]` — the parameters in parentheses are optional

---

## [1.0.0] - 2026-07-14

### 🎉 Initial Release
- **Nuke Command** for Bot Designer for Discord (BDFD) released.
- Deletes and recreates a channel while preserving its configuration (name, position, category, topic, NSFW, slowmode).
- Button confirmation restricted to the command author.
- Robust error handling with `$try`/`$catch`/`$error`.
- Bot and user permission verification.
- 100% JSON storage with 1 variable (`NukeData`).
- Available in 5 languages:
  - 🇪🇸 Spanish (Español)
  - 🇬🇧 English
  - 🇩🇪 German (Deutsch)
  - 🇮🇹 Italian (Italiano)
  - 🇵🇹 Portuguese (Português)

### 📁 Project Structure
```
Documentation/
├── README.md
├── CHANGELOGS.md
├── Español/
├── English/
├── Deutsch/
├── Italiano/
└── Português/
```

### ✨ Features
- Automatic channel detection (mentioned or current)
- Confirmation with Accept/Cancel buttons
- Author restriction pattern (`customID-$authorID`)
- Configuration preservation (name, position, category, topic, NSFW, slowmode)
- Error handling with `$try`/`$catch`/`$error` + `$suppressErrors`
- Permission verification for bot and user
- No global variables (`$setVar`/`$getVar` not used)
- Components V2 ready (optional)

---

*Dates and times are in UTC+0.*
