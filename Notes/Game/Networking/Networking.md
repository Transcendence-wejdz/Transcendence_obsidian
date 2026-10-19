---
graph-size: 200
fichiers:
  - "[[NetworkBootstrap.cs]]"
  - "[[ServicesAuth.cs]]"
  - "[[WebProfileBridge.cs]]"
  - "[[WebBackend.cs]]"
  - "[[GameModeLoader.cs]]"
  - "[[ModeReadyCheck.cs]]"
  - "[[OfflinePlayerGate.cs]]"
  - "[[PhantomPlayerCleanup.cs]]"
  - "[[SessionDisconnectHandler.cs]]"
  - "[[NetworkBehaviourExtensions.cs]]"
  - "[[TestClientProbe.cs]]"
---
#module #game

Couche multijoueur : Netcode for GameObjects + Unity Relay/Services. Transversale à presque tous les autres modules.

## Scripts

- <a href="#vault://../UnityProject/Assets/Scripts/Networking/NetworkBootstrap.cs" class="LinkRelativeTo">NetworkBootstrap.cs</a> — host/join via l'API Session Unity + Relay, lancé depuis le Lobby
- <a href="#vault://../UnityProject/Assets/Scripts/Networking/ServicesAuth.cs" class="LinkRelativeTo">ServicesAuth.cs</a> — authentification Unity Services ; en WebGL, profil Auth séparé par compte web + nom Unity (Friends) = display_name du site
- <a href="#vault://../UnityProject/Assets/Scripts/Networking/WebProfileBridge.cs" class="LinkRelativeTo">WebProfileBridge.cs</a> — reçoit le profil du site (`SendMessage("WebProfileBridge","SetProfile")` : id, nom, classe, couleur, réglages) et renvoie les changements faits en jeu
- <a href="#vault://../UnityProject/Assets/Scripts/Networking/WebBackend.cs" class="LinkRelativeTo">WebBackend.cs</a> — `PATCH /api/game/profile` via `Plugins/WebGL/WebBackend.jslib` (no-op hors build WebGL)
- <a href="#vault://../UnityProject/Assets/Scripts/Networking/GameModeLoader.cs" class="LinkRelativeTo">GameModeLoader.cs</a> — chargement de la scène de mode (Coop, …)
- <a href="#vault://../UnityProject/Assets/Scripts/Networking/ModeReadyCheck.cs" class="LinkRelativeTo">ModeReadyCheck.cs</a> — ready-check / sélection d'équipe avant lancement
- <a href="#vault://../UnityProject/Assets/Scripts/Networking/OfflinePlayerGate.cs" class="LinkRelativeTo">OfflinePlayerGate.cs</a> — garantit que le solo fonctionne sans hoster (pattern `IsLocallyControlled`, jamais `IsOwner` brut)
- <a href="#vault://../UnityProject/Assets/Scripts/Networking/PhantomPlayerCleanup.cs" class="LinkRelativeTo">PhantomPlayerCleanup.cs</a> — supprime les spawns fantômes de `NetworkObject` placés en scène
- <a href="#vault://../UnityProject/Assets/Scripts/Networking/SessionDisconnectHandler.cs" class="LinkRelativeTo">SessionDisconnectHandler.cs</a> — évite que le client freeze quand l'host quitte
- <a href="#vault://../UnityProject/Assets/Scripts/Networking/NetworkBehaviourExtensions.cs" class="LinkRelativeTo">NetworkBehaviourExtensions.cs</a> — helpers partagés
- <a href="#vault://../UnityProject/Assets/Scripts/Networking/TestClientProbe.cs" class="LinkRelativeTo">TestClientProbe.cs</a> — harnais de test 2 instances (Editor host + build standalone)

## Connexions

- Sous-couche de [[Player]] (spawn/ownership), [[Enemies]] (état répliqué des vagues), [[Friends]] (invite ↔ session hosting)
- Pont avec [[Web Overview]] : profil + réglages/keybinds synchronisés dans les deux sens avec la DB (`users.game_settings`)
- Pilote [[UI]] : `LobbyRosterUI`, `ReadyCheckUI`, `InviteToastUI`
- Piège récurrent : `NetworkVariable.Value` ne doit jamais être écrit en premier dans `Awake()` (crash WebGL/IL2CPP) ; ajouter/retirer une `NetworkVariable` nécessite un rebuild lockstep (sinon `OverflowException` sur un client avec un vieux build)
