---
graph-size: 200
fichiers:
  - "[[PauseManager.cs]]"
  - "[[GameSettings.cs]]"
  - "[[KeybindOverrides.cs]]"
  - "[[LoadingScreenManager.cs]]"
  - "[[SortingLayer_Auto.cs]]"
  - "[[DeathProtectionZone.cs]]"
---
#module #game

Systèmes transversaux, pas spécifiques à un module gameplay.

## Scripts

- <a href="#vault://../UnityProject/Assets/Scripts/Core/PauseManager.cs" class="LinkRelativeTo">PauseManager.cs</a> — flag statique `IsPaused` lu par [[Player]] et d'autres ; gère les panneaux pause/settings et le bouton de sortie contextuel ("Return to Lobby" / "Leave Session")
- <a href="#vault://../UnityProject/Assets/Scripts/Core/GameSettings.cs" class="LinkRelativeTo">GameSettings.cs</a> — paramètres persistés (voir [[UI]]`/SettingsPanelUI`)
- <a href="#vault://../UnityProject/Assets/Scripts/Core/KeybindOverrides.cs" class="LinkRelativeTo">KeybindOverrides.cs</a> — rebind touches/manette persisté
- <a href="#vault://../UnityProject/Assets/Scripts/Core/LoadingScreenManager.cs" class="LinkRelativeTo">LoadingScreenManager.cs</a> — écran de chargement lors des transitions de scène
- <a href="#vault://../UnityProject/Assets/Scripts/Core/SortingLayer_Auto.cs" class="LinkRelativeTo">SortingLayer_Auto.cs</a> — assignation automatique de sorting layer/order
- <a href="#vault://../UnityProject/Assets/Scripts/Player/DeathProtectionZone.cs" class="LinkRelativeTo">DeathProtectionZone.cs</a> — zone d'invulnérabilité temporaire après respawn

## Connexions

- `PauseManager.IsPaused` est vérifié par [[Player]]`/Player.Movement`
- `SortingLayer_Auto` est utilisé par le décor de [[Terrain]]
- `DeathProtectionZone` s'articule avec le flow de mort/mount de [[Player]]
