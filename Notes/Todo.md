---

kanban-plugin: board

---

## À faire

- [ ] **OAuth 42 + 2FA** : connexion distante + double authentification (exigé, réunion 13/09) #web
- [ ] **Fonctionnalités temps réel** : major Web (statuts en ligne, notifications…) #web
- [ ] **Messagerie / chat** : major Web #web
- [ ] **Chat avancé** : minor UX (bloquer, inviter à une partie, profils depuis le chat) #web
- [ ] **i18n** : minor Accessibilité (au moins 3 langues) #web
- [ ] **Navigateurs supplémentaires** : minor Accessibilité, documenter les tests (Svelte s'en charge en partie) #web
- [ ] **Historique des parties + scoreboard + achievements** : minor Gestion utilisateurs #web #game
- [ ] **Gamification** : minor UX : achievements, leaderboards, XP #web #game
- [ ] **Mode 2 vs 2** : conçu, pas encore codé #game
- [ ] **Mode 3 vs 1 horde leader** : conçu, pas encore codé #game
- [ ] **Site + jeu responsive** : y compris touch devices pour le jeu #web #game
- [ ] **Zéro erreur dans la console Chrome** : vérifier toutes les pages (exigé) #web
- [ ] **Validation côté serveur partout** : revoir toutes les routes API #web
- [ ] **Secrets hors du repo** : `.env` généré / injecté par la CI #infra #ci
- [ ] **Typer `game/+page.svelte`** : 24 erreurs `svelte-check` (JS sans types) #web
- [ ] **Licence Unity dans les secrets GitHub** : pour que Unity Build Check compile vraiment #ci
- [ ] **Protections de branches** : `main` et `develop` : PR obligatoire, CI verte, 1 review #ci
- [ ] **Réécrire les notes Web du vault** : `Server`/`Frontend` décrivent encore l'ancien `server.js` #vault
- [ ] **Finaliser les modules du README** : liste + points, à valider contre le sujet #docs
- [ ] **Contributions individuelles du README** : jureix-c, dabuchhe, willda-s #docs
- [ ] **Bug : « The player is already signing in »** : clic Host/Join juste après le lancement #game
- [ ] **Perf : culling NetworkTransform** : ~300 ennemis répliqués #game


## Optionnel (modules « ? », pas nécessaires)

- [ ] **IA adverse** : major IA (course de cochons ?) #game
- [ ] **Modération par IA** : minor IA #web
- [ ] **WAF + Vault (secrets)** : major Cybersécurité, durcissement #infra
- [ ] **Health check** : minor DevOps #infra
- [ ] **Second jeu, course de cochons** : major UX avec matchmaking + stats séparées #game


## En cours



## Fait

**Complete**
- [x] **Site SvelteKit** : comptes, sessions Argon2id, Prisma/PostgreSQL, profil (erbuffet) #web
- [x] **Jeu intégré au site** : page `/game`, compte obligatoire pour jouer #web #game
- [x] **Profil partagé site ↔ jeu** : personnage, nom, réglages, keybinds sauvés en DB #web #game
- [x] **Unity Friends** : nom = display name du site, identité par compte #game
- [x] **Organisation git** : `main` ← `develop` ← `feat/*`, voir [[Git Workflow]] #ci
- [x] **README** : refait pour l'équipe de 5 #docs




%% kanban:settings
```
{"kanban-plugin":"board","show-checkboxes":false,"tag-colors":[{"tagKey":"#web","color":"rgba(255, 255, 255, 1)","backgroundColor":"rgba(59, 130, 246, 0.8)"},{"tagKey":"#game","color":"rgba(255, 255, 255, 1)","backgroundColor":"rgba(224, 62, 62, 0.8)"},{"tagKey":"#infra","color":"rgba(255, 255, 255, 1)","backgroundColor":"rgba(147, 51, 234, 0.8)"},{"tagKey":"#ci","color":"rgba(0, 0, 0, 1)","backgroundColor":"rgba(245, 158, 11, 0.8)"},{"tagKey":"#docs","color":"rgba(0, 0, 0, 1)","backgroundColor":"rgba(148, 163, 184, 0.8)"},{"tagKey":"#vault","color":"rgba(255, 255, 255, 1)","backgroundColor":"rgba(191, 62, 224, 0.8)"}],"list-collapse":[null,null,null,false]}
```
%%