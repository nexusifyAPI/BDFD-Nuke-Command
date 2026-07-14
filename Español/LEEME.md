# 💣 Comando Nuke — Español

## 📋 Instrucciones

### 1. Crear la variable
Ve a la sección **"Variables"** de tu bot en BDFD y crea la siguiente variable:

| Nombre | Valor por defecto |
|--------|-------------------|
| `NukeData` | `{}` |

### 2. Crear los comandos
En esta carpeta encontrarás 2 archivos con el código necesario:

| Archivo | Disparador (Trigger) | Tipo |
|---------|----------------------|------|
| `Comando_Principal.md` | `!nuke` | Command (BDScript 2) |
| `Callback ($onInteraction).md` | `$onInteraction` | Command (BDScript 2) |

### 3. Configuración
- **Modo de script:** BDScript 2 (obligatorio en ambos comandos)
- **Permisos del bot:** `managechannels`, `sendmessages`, `embedlinks`
- **Permisos del usuario:** `managechannels`

### 4. Uso
```
!nuke           → Nukea el canal actual
!nuke #canal    → Nukea el canal mencionado
```
