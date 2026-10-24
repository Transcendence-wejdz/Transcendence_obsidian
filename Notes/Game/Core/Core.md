---
graph-size: 200
fichiers:
  - "[[PauseManager.cs]]"
  - "[[GameSettings.cs]]"
  - "[[KeybindOverrides.cs]]"
  - "[[InputModeTracker.cs]]"
  - "[[LoadingScreenManager.cs]]"
  - "[[SortingLayer_Auto.cs]]"
  - "[[DeathProtectionZone.cs]]"
---
#module #game

Systèmes transversaux, pas spécifiques à un module gameplay.

## Scripts

- <a href="#vault://../UnityProject/Assets/Scripts/Core/PauseManager.cs" class="LinkRelativeTo">PauseManager.cs</a> : flag statique `IsPaused` lu par [[Player]] et d'autres ; gère les panneaux pause/settings, le bouton de sortie contextuel ("Return to Lobby" / "Leave Session") et `Back()` (B à la manette : Settings vers Pause, puis reprise)
- <a href="#vault://../UnityProject/Assets/Scripts/Core/Settings/GameSettings.cs" class="LinkRelativeTo">GameSettings.cs</a> : paramètres persistés (voir [[UI]]`/SettingsPanelUI`), dont `StickDeadzone` (5 à 50 %, 15 % par défaut)
- <a href="#vault://../UnityProject/Assets/Scripts/Core/Settings/KeybindOverrides.cs" class="LinkRelativeTo">KeybindOverrides.cs</a> — rebind touches/manette persisté
- <a href="#vault://../UnityProject/Assets/Scripts/Core/Settings/InputModeTracker.cs" class="LinkRelativeTo">InputModeTracker.cs</a> : créé au lancement ; mode manette dès qu'une manette est branchée ou utilisée, mode souris dès que la souris bouge ou clique ; applique `StickDeadzone` à la deadzone globale de l'Input System
- <a href="#vault://../UnityProject/Assets/Scripts/Core/LoadingScreenManager.cs" class="LinkRelativeTo">LoadingScreenManager.cs</a> — écran de chargement lors des transitions de scène
- <a href="#vault://../UnityProject/Assets/Scripts/Core/Rendering/SortingLayer_Auto.cs" class="LinkRelativeTo">SortingLayer_Auto.cs</a> — assignation automatique de sorting layer/order
- <a href="#vault://../UnityProject/Assets/Scripts/Player/DeathProtectionZone.cs" class="LinkRelativeTo">DeathProtectionZone.cs</a> — zone d'invulnérabilité temporaire après respawn

## Connexions

- `PauseManager.IsPaused` est vérifié par [[Player]]`/Player.Movement`
- `InputModeTracker.UsingGamepad` choisit entre visée souris et stick droit dans [[Player]]`/Player.Movement`, et pilote le navigateur manette et le curseur de [[UI]]
- `SortingLayer_Auto` est utilisé par le décor de [[Terrain]]
- `DeathProtectionZone` s'articule avec le flow de mort/mount de [[Player]]
