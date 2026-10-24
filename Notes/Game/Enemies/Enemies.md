---
graph-size: 200
fichiers:
  - "[[Enemy.cs]]"
  - "[[EnemyAI.cs]]"
  - "[[EnemyActions.cs]]"
  - "[[EnemyStats.cs]]"
  - "[[EnemyKit.cs]]"
  - "[[EnemyKitEditor.cs]]"
  - "[[EnemyFlowFieldManager.cs]]"
  - "[[EnemyFlowField.cs]]"
  - "[[ObstacleQuery.cs]]"
  - "[[AttackTelegraph.cs]]"
  - "[[RangedAttackVisual.cs]]"
  - "[[WaveSpawner.cs]]"
  - "[[XPManager.cs]]"
  - "[[LevelUpManager.cs]]"
  - "[[GameOverCheck.cs]]"
---
#module #game

IA de la horde. Même pattern de découpage que [[Player]] : un hub `Enemy.cs` + `EnemyAI`/`EnemyActions` séparés, un seul prefab de base configuré par un asset de données (`EnemyKit`, l'équivalent de `ClassKit` côté joueur). L'IA est dans `AI/` ; la boucle de run (vagues, XP, level-up, score, game over, `RunCarryOver`) vit dans `Scripts/Run/`.

## Scripts

- <a href="#vault://../UnityProject/Assets/Scripts/Enemies/Enemy.cs" class="LinkRelativeTo">Enemy.cs</a> — hub
- <a href="#vault://../UnityProject/Assets/Scripts/Enemies/AI/EnemyAI.cs" class="LinkRelativeTo">EnemyAI.cs</a> — décision/déplacement (flow field)
- <a href="#vault://../UnityProject/Assets/Scripts/Enemies/AI/EnemyActions.cs" class="LinkRelativeTo">EnemyActions.cs</a> — attaques, inflige des dégâts via `IDamageable`
- <a href="#vault://../UnityProject/Assets/Scripts/Enemies/EnemyStats.cs" class="LinkRelativeTo">EnemyStats.cs</a> — vie, implémente `IDamageable`/`IHealthStats` (voir [[Combat]])
- <a href="#vault://../UnityProject/Assets/Scripts/Enemies/EnemyKit.cs" class="LinkRelativeTo">EnemyKit.cs</a> — asset de données par type d'ennemi (tier, portée, stats)
- <a href="#vault://../UnityProject/Assets/Scripts/Enemies/Editor/EnemyKitEditor.cs" class="LinkRelativeTo">Editor/EnemyKitEditor.cs</a> — inspecteur custom
- <a href="#vault://../UnityProject/Assets/Scripts/Enemies/AI/EnemyFlowFieldManager.cs" class="LinkRelativeTo">EnemyFlowFieldManager.cs</a> / <a href="#vault://../UnityProject/Assets/Scripts/Enemies/AI/EnemyFlowField.cs" class="LinkRelativeTo">EnemyFlowField.cs</a> — un flow field partagé par joueur pour le pathing de masse
- <a href="#vault://../UnityProject/Assets/Scripts/Enemies/AI/ObstacleQuery.cs" class="LinkRelativeTo">ObstacleQuery.cs</a> — requêtes d'obstacles pour le flow field
- <a href="#vault://../UnityProject/Assets/Scripts/Enemies/AttackTelegraph.cs" class="LinkRelativeTo">AttackTelegraph.cs</a> — tell visuel avant une attaque
- <a href="#vault://../UnityProject/Assets/Scripts/Enemies/RangedAttackVisual.cs" class="LinkRelativeTo">RangedAttackVisual.cs</a> — visuel d'attaque à distance
- <a href="#vault://../UnityProject/Assets/Scripts/Run/WaveSpawner.cs" class="LinkRelativeTo">WaveSpawner.cs</a> — spawn autour des joueurs (pas au centre de la map), scale avec le nombre de joueurs
- <a href="#vault://../UnityProject/Assets/Scripts/Run/XPManager.cs" class="LinkRelativeTo">XPManager.cs</a> / <a href="#vault://../UnityProject/Assets/Scripts/Run/LevelUpManager.cs" class="LinkRelativeTo">LevelUpManager.cs</a> — gain d'XP, écran de choix de level-up (solo illimité / multi 20s+ready-list)
- <a href="#vault://../UnityProject/Assets/Scripts/Run/GameOverCheck.cs" class="LinkRelativeTo">GameOverCheck.cs</a> — réplique un wipe total, l'host choisit Restart/Lobby

## Connexions

- → [[Combat]] : inflige/reçoit des dégâts via `IDamageable`
- → [[UI]] : `LevelUpManager`/`GameOverCheck` pilotent `LevelUpUI`/`GameOverUI`, `CoopHUD` affiche timer+vague depuis l'état répliqué de `WaveSpawner`
- → [[Networking]] : état répliqué (vagues, wipe) synchronisé par Netcode
