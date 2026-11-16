---
graph-size: 300
---
#guide

Lien retour : [[Home]] · Aide : [[Aide]]

# Guide des issues GitHub

| | |
|---|---|
| **Objet** | Organiser et suivre le travail de l'équipe avec GitHub Issues et le Project `ft_transcendence` |
| **Public** | Tous les membres de l'équipe, sans prérequis sur GitHub |
| **Dépôt** | [`Transcendence-wejdz/ft_transcendence`](https://github.com/Transcendence-wejdz/ft_transcendence) |
| **Voir aussi** | [[Git Workflow]] (branches, commits, PR) · [[Relire une PR]] |
| **Dernière mise à jour** | 16 novembre 2026 |

Tout se fait sur le site GitHub, sauf les commandes `git` pour récupérer une branche.

---

## 1. Principes

- **Une tâche, une issue.** Aucun travail ne commence sans issue. C'est ce qui permet de montrer, en correction, comment le travail a été organisé et réparti.
- **Un module, une epic.** Chaque module retenu a une issue parent, et la partie obligatoire en a une aussi (#74). Le travail se fait dans les sous-issues.
- **Le Project fait référence.** L'état du projet se lit dans le Project : qui fait quoi, ce qui avance, ce qui bloque.
- **Tout est rédigé en anglais** : titres, descriptions et commentaires, comme le reste du dépôt.

---

## 2. Vocabulaire

| Terme | Définition |
|---|---|
| **Issue** | Fiche qui décrit un travail à faire : une tâche, un bug ou une décision. Elle porte un numéro, par exemple `#81`. |
| **Epic** | Issue parent qui regroupe tout le travail d'un module. |
| **Sous-issue** (*sub-issue*) | Issue rattachée à une epic. C'est l'unité de travail : on la code, on la relit, on la ferme. |
| **Assignee** | Personne responsable de l'issue. |
| **Label** | Étiquette qui sert à classer et filtrer les issues. |
| **Milestone** (jalon) | Ensemble de tâches à terminer pour une date donnée. |
| **Project** | Tableau de suivi qui réunit toutes les issues du dépôt. |

Les issues et les Pull Requests partagent le même compteur. Si la dernière PR est la `#72`, la prochaine issue sera la `#73`.

---

## 3. Organisation des issues

```
module-3: feat: User interaction: chat, profiles, friends     epic
 ├─ [x] feat(web): add the friends system                      sous-issue (fermée)
 ├─ [ ] feat(web): add the basic chat                          sous-issue (en cours)
 └─ [ ] feat(web): add the player profile page                 sous-issue (à faire)
                                             Progression : 1 / 3
```

### 3.1 Types d'issues

| Type | Rôle | Labels | Exemple de titre |
|---|---|---|---|
| **Epic** | Regroupe un module : critères du sujet et sous-issues | `epic` + `module:major` ou `module:minor` | `module-2: feat: Real-time features with WebSockets (Web, Major, 2 pts)` |
| **Tâche** | Travail concret, rattaché à une epic | zone + jalon | `feat(web): add the basic chat` |
| **Décision** | Choix à faire en équipe avant de coder | `decision` + zone | `Decide where the WebSocket server runs` |
| **Bug** | Dysfonctionnement à corriger | `bug` + zone | `fix(web): reject avatars over 500 KB` |

### 3.2 Labels

| Label | Usage |
|---|---|
| `epic` | Issue parent d'un module |
| `module:major` · `module:minor` | Module majeur (2 points) · mineur (1 point) |
| `decision` | Choix à trancher en équipe |
| `bug` | Dysfonctionnement |
| `web` · `game` · `infra` · `ci` · `docs` | Partie du projet concernée |

### 3.3 Les epics

- Chaque epic reprend les **critères du sujet** sous forme de cases à cocher. Ce sont exactement les points vérifiés en correction.
- **On ne travaille jamais directement sur une epic** : ni branche, ni Pull Request. Le travail se fait dans ses sous-issues.
- La personne assignée à l'epic est le **responsable du module** (voir §4).
- L'epic **`mandatory`** ([#74](https://github.com/Transcendence-wejdz/ft_transcendence/issues/74)) regroupe la partie obligatoire du sujet : pages légales, console propre, validation des formulaires, README…

---

## 4. Rôles et responsabilités

| Rôle | Qui | Responsabilités sur les issues |
|---|---|---|
| **Responsable de module** | La personne assignée à l'epic | Crée les sous-issues de son module au début de chaque jalon. Coche les critères du sujet dans l'epic au fur et à mesure. Signale les blocages. |
| **Product Owner** | zsonie (`SaruM4N3`) | Range le Backlog et fixe les priorités. Décide ce qui passe en « À faire » et dans quel jalon. Valide qu'un module est terminé avant qu'on ferme son epic. |
| **Tech Lead** | jureix-c (`E-B3rry`) | Aide à trancher les décisions techniques. Relit les changements critiques. |
| **Scrum Master** | dabuchhe (`dabuchhe`) | Crée les sous-issues de l'epic `mandatory`. À chaque réunion, vérifie que les modules du jalon ont leurs sous-issues, que le tableau est à jour et que personne n'est bloqué. Accompagne les membres qui débutent. |
| **Tous les membres** | Toute l'équipe | Créent une issue pour tout bug ou toute tâche repérée, et la rattachent à la bonne epic. Tiennent à jour le statut de leurs tâches. |

**Démarrage d'un module.** La première fois, le responsable crée les sous-issues de son module avec le Scrum Master, par exemple en partage d'écran après la réunion. Ensuite, il le fait seul.

**À surveiller.** Si une epic du jalon en cours n'a toujours aucune sous-issue quelques jours après la réunion, le responsable a probablement besoin d'aide. Le Scrum Master fait le point avec lui.

---

## 5. Le Project

**Accès** : page de l'organisation `Transcendence-wejdz` → onglet **Projects** → **ft_transcendence**.

| Vue | Contenu | Usage |
|---|---|---|
| **Tableau** | Les tâches en colonnes par statut, en bandes par jalon (J1, J2), sans les epics | Suivi au quotidien |
| **Équipe** | Les tâches ouvertes, en bandes par personne | Répartition, en réunion |
| **Modules** | Une ligne par epic, avec sa progression | Suivi global, en réunion |

La progression de chaque jalon (pourcentage, échéance) se lit sur la page [Milestones](https://github.com/Transcendence-wejdz/ft_transcendence/milestones) du dépôt.

Colonnes de la vue **Tableau** :

| Colonne | Signification | Qui y place la carte |
|---|---|---|
| **Backlog** | Tâche pas encore prête : floue ou pas prioritaire | Automatique à la création |
| **À faire** | Tâche prête, que n'importe qui peut prendre | Le Product Owner |
| **En cours** | Tâche prise par quelqu'un | La personne assignée, quand elle commence |
| **En review** | Pull Request ouverte, en attente de relecture | La personne assignée, quand elle ouvre la PR |
| **Terminé** | PR fusionnée, issue fermée | Automatique à la fermeture |

Pour changer le statut d'une carte : la faire glisser d'une colonne à l'autre, ou ouvrir l'issue → barre latérale → **Projects** → champ **Status**.

---

## 6. Cycle de vie d'une tâche

### 6.1 Choisir une tâche
1. Ouvrir le Project, vue **Tableau**, colonne **À faire**.
2. Choisir de préférence une tâche du jalon en cours.
3. Une tâche déjà assignée à quelqu'un ne se prend pas : en parler d'abord avec cette personne.

Autre méthode : dans l'onglet **Issues**, rechercher `is:open no:assignee -label:epic`.

### 6.2 S'assigner la tâche
1. Ouvrir l'issue.
2. Barre latérale → **Assignees** → **assign yourself**.
3. Passer la carte en **En cours**.

### 6.3 Créer la branche depuis l'issue
1. Barre latérale de l'issue → section **Development** → **Create a branch**.
2. Nommer la branche selon la convention du README :

   | Type | Format | Exemple |
   |---|---|---|
   | Fonctionnalité | `feat/<scope>-<nom>` | `feat/web-friends-list` |
   | Correction | `fix/<scope>-<nom>` | `fix/game-wave-spawn` |
   | Documentation | `docs/<nom>` | `docs/readme-modules` |

   Scopes : `web`, `api`, `db`, `game`, `net`, `infra`, `ci`, `vault`, `docs`.
3. **Change branch source** → choisir **`develop`**. Jamais `main`.
4. Choisir **Checkout locally** → **Create branch**, puis lancer dans un terminal les commandes affichées par GitHub :
   ```sh
   git fetch origin
   git checkout feat/web-friends-list
   ```

La branche apparaît alors dans la section **Development** de l'issue.

### 6.4 Développer
Faire de petits commits, au format du README : `type(scope): summary`, en anglais.
```sh
git commit -m "feat(web): add the friends list page"
git push
```

### 6.5 Ouvrir la Pull Request
1. Sur GitHub, cliquer sur le bandeau **Compare & pull request**.
2. Choisir **base : `develop`**.
3. Écrire le titre au format Conventional Commit, par exemple `feat(web): add the friends list page`.
4. Remplir le modèle de PR. Dans la partie **What & why**, ajouter `Issue: #81` (le numéro de l'issue) : la PR apparaîtra dans l'historique de l'issue.
5. Dans la barre latérale → **Reviewers** : demander deux relecteurs. Voir [[Relire une PR]].
6. Passer la carte en **En review**.

> **Important.** Le mot-clé `Closes #81` ne ferme l'issue que pour une PR fusionnée dans `main`. Nos PR visent `develop`, donc l'issue se ferme à la main (§6.6).

### 6.6 Clôturer
Une fois la PR fusionnée :
1. Ouvrir l'issue et ajouter un commentaire, par exemple `Merged in #95`.
2. Cliquer sur **Close issue**.
3. La carte passe automatiquement dans **Terminé**, et la progression de l'epic se met à jour.
4. Si le comportement de l'application a changé, mettre à jour la note Obsidian du module.

---

## 7. Créer une issue

### 7.1 Tâche d'un module
1. Ouvrir l'epic du module : vue **Modules** du Project, ou recherche `label:epic`.
2. Sous la description, cliquer sur **Create sub-issue**.
3. Écrire le titre au format Conventional Commit, en anglais, par exemple `feat(web): add the friends list page`. Il servira aussi de titre à la PR.
4. Reprendre ce modèle de description :
   ```markdown
   ## Context
   <!-- Why are we doing this? Which subject requirement does it cover? -->

   ## To do
   - [ ] 

   ## Done when
   - [ ] 
   ```
5. Remplir la barre latérale :
   - **Labels** : la zone (`web`, `game`, `infra`…) ;
   - **Milestone** : le jalon visé ;
   - **Projects** : `ft_transcendence` ;
   - **Assignees** : seulement si quelqu'un commence tout de suite.
6. Cliquer sur **Create**.

Une tâche qui dépasse 2 jours de travail se découpe en plusieurs sous-issues.

### 7.2 Bug ou issue existante
1. Onglet **Issues** → **New issue** : créer l'issue (label `bug` pour un dysfonctionnement).
2. Si elle concerne un module : ouvrir l'epic → flèche à côté de **Create sub-issue** → **Add existing issue**.
3. Si elle concerne la partie obligatoire, la rattacher à l'epic **`mandatory`** (#74).

### 7.3 Décision
Une issue `decision` sert à faire un choix qui engage l'équipe (architecture, librairie, règle du jeu…) et à garder une trace écrite de ce choix.

1. **Création** : n'importe quel membre la crée comme sous-issue de l'epic concernée, avec le label `decision` et sans assignee.
2. **Préparation** : chacun donne son avis en commentaire avant la réunion.
3. **Arbitrage** : la décision est prise en réunion. Les issues `decision` ouvertes forment l'ordre du jour (§10).
4. **Trace écrite** : on complète la section *Decision* (bouton `⋯` de la description → **Edit**), puis on ferme l'issue.
5. **Suite** : le responsable du module crée les sous-issues qui découlent de la décision.

Modèle de description :
```markdown
## Context
<!-- Why do we need to decide? What depends on it? -->

## Options
- **A.** 
- **B.** 

## Questions to answer
- [ ] 

## Decision
_To fill in once decided: what we chose, and why._
```

---

## 8. Suivre l'avancement

| Besoin | Où regarder |
|---|---|
| État d'un module | La page de l'epic : progression des sous-issues (« x of y ») et critères cochés |
| État global du projet | Project → vue **Modules** |
| Avancement d'un jalon | Onglet **Issues** → **Milestones** |
| Charge de chacun | Project → vue **Équipe** |
| Mes tâches en cours | Onglet **Issues** → `is:open assignee:@me` |
| Décisions en attente | Onglet **Issues** → `is:open label:decision` |

---

## 9. Règles d'équipe

| # | Règle | Raison |
|:-:|---|---|
| 1 | Aucun code sans issue | Le travail est traçable et sa répartition peut être démontrée en correction |
| 2 | S'assigner avant de commencer | Deux personnes ne font pas la même chose |
| 3 | Deux tâches « En cours » au maximum par personne | On termine avant de commencer autre chose |
| 4 | Aucune branche ni PR sur une epic | Une epic regroupe des tâches, ce n'est pas une tâche |
| 5 | En cas de blocage : l'écrire dans l'issue et prévenir sur Discord | Personne ne reste bloqué seul |
| 6 | Toute décision qui engage l'équipe passe par une issue `decision` | Les choix restent écrits et justifiés |
| 7 | Une epic ne se ferme que quand tous les critères du sujet sont cochés et validés par le Product Owner | Un module incomplet vaut 0 point en correction |
| 8 | Tout le contenu GitHub est rédigé en anglais | Convention du dépôt |

---

## 10. Recherches utiles

À saisir dans la barre de recherche de l'onglet **Issues** :

| Objectif | Recherche |
|---|---|
| Tâches disponibles | `is:open is:issue no:assignee -label:epic` |
| Mes tâches ouvertes | `is:open assignee:@me` |
| Tous les modules | `is:issue label:epic` |
| Ordre du jour de la réunion | `is:open label:decision` |
| Bugs ouverts | `is:open label:bug` |

---

## 11. Questions fréquentes

**Le bouton *Create sub-issue* n'apparaît pas, ou je ne peux pas m'assigner.**
Il manque le droit d'écriture sur le dépôt. Demander à un administrateur de l'organisation.

**Une sous-issue est rattachée à la mauvaise epic.**
Dans la mauvaise epic : menu `⋯` de la sous-issue → **Remove sub-issue**. Puis, dans la bonne epic : **Add existing issue**.

**Une issue a été fermée par erreur.**
Ouvrir l'issue et cliquer sur **Reopen issue**, en bas de la page.

**La PR n'apparaît pas dans l'issue.**
Ajouter `Issue: #81` dans la description de la PR, ou, dans la barre latérale de la PR → **Development** → choisir l'issue.

**Je ne sais pas à quelle epic rattacher une tâche.**
Poser la question en réunion ou sur Discord. En attendant, créer l'issue sans parent : le Product Owner la rangera.
