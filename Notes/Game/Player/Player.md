---
graph-size: 200
fichiers:
  - "[[Player.cs]]"
  - "[[Player.Movement.cs]]"
  - "[[Player.Actions.cs]]"
  - "[[Player.Stats.cs]]"
  - "[[Player.Customization.cs]]"
  - "[[Player.Feedback.cs]]"
  - "[[Player.LevelUp.cs]]"
  - "[[Player.Mount.cs]]"
  - "[[Player.PigForm.cs]]"
  - "[[Player.Shield.cs]]"
  - "[[ClassKit.cs]]"
  - "[[ClassKitEditor.cs]]"
  - "[[AbilityType.cs]]"
  - "[[LocalPlayer.cs]]"
  - "[[MouseDirectionIndicator.cs]]"
  - "[[PlayerCameraRig.cs]]"
  - "[[PlayerNameTag.cs]]"
  - "[[PlayerProfileStore.cs]]"
  - "[[PlayerSpawner.cs]]"
  - "[[PlayerSpawnPoint.cs]]"
---
#module #game

Tout ce qui concerne le joueur contrôlable. `Player.cs` est le hub : une classe `partial` éclatée en plusieurs fichiers par responsabilité (fusion effectuée lors du refactor "Player component merge").

## Scripts

- <a href="#vault://../UnityProject/Assets/Scripts/Player/Player.cs" class="LinkRelativeTo">Player.cs</a> — hub, état partagé entre les fichiers partiels ci-dessous
- <a href="#vault://../UnityProject/Assets/Scripts/Player/Player.Movement.cs" class="LinkRelativeTo">Player.Movement.cs</a> — input (New Input System), déplacement, flip sprite, orientation souris
- <a href="#vault://../UnityProject/Assets/Scripts/Player/Player.Actions.cs" class="LinkRelativeTo">Player.Actions.cs</a> — Attack/Special/Ultimate pilotés par [[ClassKit]]
- <a href="#vault://../UnityProject/Assets/Scripts/Player/Player.Stats.cs" class="LinkRelativeTo">Player.Stats.cs</a> — vie/mana, implémente `IDamageable`/`IHealthStats` (voir [[Combat]])
- <a href="#vault://../UnityProject/Assets/Scripts/Player/Player.Customization.cs" class="LinkRelativeTo">Player.Customization.cs</a> — classe/couleur/nom
- <a href="#vault://../UnityProject/Assets/Scripts/Player/Player.Feedback.cs" class="LinkRelativeTo">Player.Feedback.cs</a> — retours visuels (hit flash, etc.)
- <a href="#vault://../UnityProject/Assets/Scripts/Player/Player.LevelUp.cs" class="LinkRelativeTo">Player.LevelUp.cs</a> — réception des choix de level-up
- <a href="#vault://../UnityProject/Assets/Scripts/Player/Player.Mount.cs" class="LinkRelativeTo">Player.Mount.cs</a> — monter le cochon d'un allié pour le ressusciter
- <a href="#vault://../UnityProject/Assets/Scripts/Player/Player.PigForm.cs" class="LinkRelativeTo">Player.PigForm.cs</a> — forme "cochon" quand mort (se déplace, ne combat pas)
- <a href="#vault://../UnityProject/Assets/Scripts/Player/Player.Shield.cs" class="LinkRelativeTo">Player.Shield.cs</a> — ultimate bouclier du Warrior
- <a href="#vault://../UnityProject/Assets/Scripts/Player/ClassKit.cs" class="LinkRelativeTo">ClassKit.cs</a> — asset de données par classe (stats + FX par capacité)
- <a href="#vault://../UnityProject/Assets/Scripts/Player/Editor/ClassKitEditor.cs" class="LinkRelativeTo">Editor/ClassKitEditor.cs</a> — inspecteur custom pour `ClassKit`
- <a href="#vault://../UnityProject/Assets/Scripts/Player/AbilityType.cs" class="LinkRelativeTo">AbilityType.cs</a> — enum partagé avec `UI/CooldownIcon`
- <a href="#vault://../UnityProject/Assets/Scripts/Player/LocalPlayer.cs" class="LinkRelativeTo">LocalPlayer.cs</a> — référence/marqueur du joueur local
- <a href="#vault://../UnityProject/Assets/Scripts/Player/MouseDirectionIndicator.cs" class="LinkRelativeTo">MouseDirectionIndicator.cs</a> — rune au sol pointant la souris, teintée à la couleur de customisation
- <a href="#vault://../UnityProject/Assets/Scripts/Player/PlayerCameraRig.cs" class="LinkRelativeTo">PlayerCameraRig.cs</a> — caméra suiveuse / caméra de preview customisation
- <a href="#vault://../UnityProject/Assets/Scripts/Player/PlayerNameTag.cs" class="LinkRelativeTo">PlayerNameTag.cs</a> — nametag monde, visible seulement en multi
- <a href="#vault://../UnityProject/Assets/Scripts/Player/PlayerProfileStore.cs" class="LinkRelativeTo">PlayerProfileStore.cs</a> — sauvegarde locale JSON (classe/couleur/nom)
- <a href="#vault://../UnityProject/Assets/Scripts/Player/PlayerSpawner.cs" class="LinkRelativeTo">PlayerSpawner.cs</a> / <a href="#vault://../UnityProject/Assets/Scripts/Player/PlayerSpawnPoint.cs" class="LinkRelativeTo">PlayerSpawnPoint.cs</a> — placement au spawn réseau

## Connexions

- → [[UI]] : `Player.Stats`/level-up/ability-used exposés via **static C# events**, consommés par `StatBarUI`, `XPBarUI`, `CooldownIcon`
- → [[Combat]] : `Player.Actions` déclenche les FX d'attaque (`IAttackFX`), `Player.Stats` implémente `IDamageable`
- → [[Networking]] : spawn/ownership via `PlayerSpawner`, logique owner-only gated par `IsLocallyControlled` (offline-first)
- → [[Core]] : `Player.Movement` vérifie `PauseManager.IsPaused`
- → [[Enemies]] : cible/est ciblé par `EnemyActions` via `IDamageable`
