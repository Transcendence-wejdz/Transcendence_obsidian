---
graph-size: 200
fichiers:
  - "[[StatBarUI.cs]]"
  - "[[XPBarUI.cs]]"
  - "[[CooldownIcon.cs]]"
  - "[[PerfStatsHUD.cs]]"
  - "[[PlayerNameUI.cs]]"
  - "[[CoopHUD.cs]]"
  - "[[AllyIndicatorManager.cs]]"
  - "[[ScreenEdgeFlash.cs]]"
  - "[[MenuPanel.cs]]"
  - "[[CharacterCustomizationMenu.cs]]"
  - "[[SettingsPanelUI.cs]]"
  - "[[SettingsTabGroup.cs]]"
  - "[[KeybindsPanelUI.cs]]"
  - "[[GameOverUI.cs]]"
  - "[[LevelUpUI.cs]]"
  - "[[LobbyRosterUI.cs]]"
  - "[[LobbyRosterEntryUI.cs]]"
  - "[[ReadyCheckUI.cs]]"
  - "[[ReadyCheckEntryUI.cs]]"
  - "[[BackgroundColorUI.cs]]"
  - "[[AvatarUI.cs]]"
  - "[[CursorManager.cs]]"
  - "[[DebugLogger.cs]]"
---
#module #game

Tous les scripts d'interface. Pattern dominant : les composants gameplay ([[Player]], [[Enemies]]) exposent l'état via des **static C# events**, et l'UI s'abonne en `OnEnable`/se désabonne en `OnDisable`.

## HUD en jeu

- <a href="#vault://../UnityProject/Assets/Scripts/UI/StatBarUI.cs" class="LinkRelativeTo">StatBarUI.cs</a> — barre vie/mana générique, pilotée par `Player.Stats`
- <a href="#vault://../UnityProject/Assets/Scripts/UI/XPBarUI.cs" class="LinkRelativeTo">XPBarUI.cs</a> — barre d'XP
- <a href="#vault://../UnityProject/Assets/Scripts/UI/CooldownIcon.cs" class="LinkRelativeTo">CooldownIcon.cs</a> — cooldown radial par `AbilityType` (voir [[Player]])
- <a href="#vault://../UnityProject/Assets/Scripts/UI/PerfStatsHUD.cs" class="LinkRelativeTo">PerfStatsHUD.cs</a> — overlay FPS/ping
- <a href="#vault://../UnityProject/Assets/Scripts/UI/PlayerNameUI.cs" class="LinkRelativeTo">PlayerNameUI.cs</a> — label de nom HUD
- <a href="#vault://../UnityProject/Assets/Scripts/UI/CoopHUD.cs" class="LinkRelativeTo">CoopHUD.cs</a> — timer + vague en haut de l'écran (état répliqué de `WaveSpawner`, voir [[Enemies]])
- <a href="#vault://../UnityProject/Assets/Scripts/UI/AllyIndicatorManager.cs" class="LinkRelativeTo">AllyIndicatorManager.cs</a> — flèches en bord d'écran vers les alliés hors-champ
- <a href="#vault://../UnityProject/Assets/Scripts/UI/ScreenEdgeFlash.cs" class="LinkRelativeTo">ScreenEdgeFlash.cs</a> — flash d'écran (dégâts reçus, etc.)

## Menus / panneaux

- <a href="#vault://../UnityProject/Assets/Scripts/UI/MenuPanel.cs" class="LinkRelativeTo">MenuPanel.cs</a> — composant générique d'ouverture/fermeture animée (scale+alpha via `CanvasGroup`, unscaled time), base des 4 menus PNJ du Lobby (voir [[Interaction]])
- <a href="#vault://../UnityProject/Assets/Scripts/UI/CharacterCustomizationMenu.cs" class="LinkRelativeTo">CharacterCustomizationMenu.cs</a> — choix classe/couleur/nom, lié à `Player.Customization`
- <a href="#vault://../UnityProject/Assets/Scripts/UI/SettingsPanelUI.cs" class="LinkRelativeTo">SettingsPanelUI.cs</a> / <a href="#vault://../UnityProject/Assets/Scripts/UI/SettingsTabGroup.cs" class="LinkRelativeTo">SettingsTabGroup.cs</a> — onglets Général/Keybinds
- <a href="#vault://../UnityProject/Assets/Scripts/UI/KeybindsPanelUI.cs" class="LinkRelativeTo">KeybindsPanelUI.cs</a> — rebind touches/manette
- <a href="#vault://../UnityProject/Assets/Scripts/UI/GameOverUI.cs" class="LinkRelativeTo">GameOverUI.cs</a> — écran de défaite (Restart/Lobby)
- <a href="#vault://../UnityProject/Assets/Scripts/UI/LevelUpUI.cs" class="LinkRelativeTo">LevelUpUI.cs</a> — écran de choix de montée de niveau

## Multijoueur

- <a href="#vault://../UnityProject/Assets/Scripts/UI/LobbyRosterUI.cs" class="LinkRelativeTo">LobbyRosterUI.cs</a> / <a href="#vault://../UnityProject/Assets/Scripts/UI/LobbyRosterEntryUI.cs" class="LinkRelativeTo">LobbyRosterEntryUI.cs</a> — liste des joueurs dans le Lobby
- <a href="#vault://../UnityProject/Assets/Scripts/UI/ReadyCheckUI.cs" class="LinkRelativeTo">ReadyCheckUI.cs</a> / <a href="#vault://../UnityProject/Assets/Scripts/UI/ReadyCheckEntryUI.cs" class="LinkRelativeTo">ReadyCheckEntryUI.cs</a> — ready-check avant lancement de mode

## Divers

- <a href="#vault://../UnityProject/Assets/Scripts/UI/BackgroundColorUI.cs" class="LinkRelativeTo">BackgroundColorUI.cs</a> — icône d'épée qui s'adapte à la couleur de personnage choisie
- <a href="#vault://../UnityProject/Assets/Scripts/UI/AvatarUI.cs" class="LinkRelativeTo">AvatarUI.cs</a> — portrait avatar
- <a href="#vault://../UnityProject/Assets/Scripts/UI/CursorManager.cs" class="LinkRelativeTo">CursorManager.cs</a> — curseur logiciel custom (pulse au clic, handoff vers le curseur OS hors fenêtre)
- <a href="#vault://../UnityProject/Assets/Scripts/UI/DebugLogger.cs" class="LinkRelativeTo">DebugLogger.cs</a> — overlay de logs debug

## Connexions

- → [[Player]], [[Enemies]] : consomme leurs static events
- → [[Networking]] : roster/ready-check reflètent l'état de session
- → [[Interaction]] : les 4 menus PNJ du Lobby sont des `MenuPanel`
