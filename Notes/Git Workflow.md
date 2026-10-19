---
graph-size: 300
---
#guide

Lien retour : [[Home]]. Tâches de l'équipe : [[Todo]].

Marche à suivre pour travailler sur le repo `ft_transcendence` (GitHub org **Transcendence-wejdz**). Le résumé officiel est dans la section *Project Management* du `README.md`.

## Les branches

```
main      protégée : PR uniquement, CI verte + 1 review : ce qu'on présente à l'éval
  ▲ PR "release: …"  →  Create a merge commit
develop   protégée : PR uniquement, CI verte : intégration web + jeu
  ▲ PR de feature    →  Squash and merge
feat/<scope>-<nom>   fix/<scope>-<nom>   docs/<nom>   (1 personne, courte durée)
```

- On ne pousse **jamais** directement sur `main` ni sur `develop`.
- Une branche = une tâche du [[Todo]]. Courte : quelques jours, pas des semaines.
- Scopes : `web`, `api`, `db`, `game`, `net`, `infra`, `ci`, `vault`, `docs`.
- Exemples : `feat/web-oauth`, `feat/game-2v2`, `fix/net-host-join-race`, `docs/readme-modules`.

## 1. Commencer une tâche

```sh
git fetch origin
git switch -c feat/web-oauth origin/develop
```

Déplace la carte dans **En cours** du [[Todo]] et mets ton login dessus.

## 2. Commiter

Format **Conventional Commits** : `type(scope): résumé court en anglais`

| Type | Quand |
|---|---|
| `feat` | nouvelle fonctionnalité |
| `fix` | correction de bug |
| `refactor` | réorganisation sans changer le comportement |
| `chore` | maintenance, build, dépendances |
| `docs` | documentation |
| `ci` | GitHub Actions |

```sh
git add <fichiers>          # éviter "git add ." : vérifier ce qu'on ajoute
git commit -m "feat(web): add OAuth login with 42"
```

- Un commit = une intention (une feature, un fix). Plusieurs petits commits valent mieux qu'un énorme.
- Corps du message optionnel : 3 à 6 puces max.
- **Unity** : un rebuild WebGL va dans son propre commit `chore(game): rebuild WebGL player`. Toujours commiter les `.meta` avec leurs assets. Ne pas commiter `ProjectSettings.asset` s'il n'a changé que tout seul (Unity le réécrit).
- Jamais de `.env`, de mot de passe ou de clé dans un commit.

## 3. Rester à jour avec develop

Avant d'ouvrir la PR (ou si `develop` a beaucoup bougé) :

```sh
git fetch origin
git rebase origin/develop
# en cas de conflit : corriger les fichiers, puis
git add <fichiers> && git rebase --continue
git push --force-with-lease      # seulement sur TA branche de feature
```

## 4. Ouvrir la Pull Request

```sh
git push -u origin feat/web-oauth
gh pr create --base develop      # ou bouton "Compare & pull request" sur GitHub
```

- **Base = `develop`** (jamais `main`).
- **Titre au format Conventional Commit** : il deviendra le commit sur `develop` après le squash. Ex. `feat(web): add OAuth login with 42`.
- Remplir le template (quoi / pourquoi, comment tester, checklist).
- Si le code touche un module, mettre à jour sa note dans ce vault (voir § Vault).

## 5. Review et merge

1. La CI doit être verte (Web CI + Unity Build Check).
2. Au moins un mate relit et approuve.
3. Merge avec **Squash and merge** : tous les commits de la branche deviennent un seul commit propre sur `develop`, ex. `feat(web): add OAuth login with 42 (#24)`.
   - Exception : **Create a merge commit** quand la PR a plusieurs auteurs ou des commits qu'on veut garder séparés.
4. Cliquer **Delete branch** sur GitHub après le merge.

Puis en local :

```sh
git switch develop
git pull
git branch -D feat/web-oauth     # -D car après un squash git ne voit pas la branche comme mergée
```

Déplace la carte dans **Fait** du [[Todo]].

## 6. Release vers main

À chaque jalon (ou avant une éval / réunion importante), le PO ou le SM ouvre :

```sh
gh pr create --base main --head develop --title "release: <résumé>"
```

Merge avec **Create a merge commit** (jamais squash ici). `git log --first-parent main` liste alors les releases.

## Vault (ce repo)

- Le vault est un repo séparé, monté en sous-module dans `Transcendence_obsidian/`.
- Les notes se poussent **directement sur `main` du vault** :
  ```sh
  cd Transcendence_obsidian
  git add Notes/... && git commit -m "docs(<module>): ..." && git push
  ```
- Puis, dans la PR du code concerné, mettre à jour le pointeur :
  ```sh
  cd .. && git add Transcendence_obsidian
  git commit -m "chore(vault): bump submodule"
  ```
- `make setup` met le vault sur le dernier `main`.

## Archiver une branche

On ne supprime jamais une branche qui contient des commits uniques sans l'archiver d'abord : la renommer en `archive/<nom>` (GitHub → Branches → icône crayon → Rename). Elle reste visible dans les graphes, ne bloque rien, et on la supprime quand tout le monde est d'accord.

## Interdits

- Push direct sur `main` / `develop`.
- `git push --force` sur `main` / `develop` (uniquement `--force-with-lease` sur sa propre branche).
- `git merge` d'une branche sans ancêtre commun (ex. une vieille branche d'avant la réécriture d'historique) : demander d'abord.
- `git checkout -- <asset Unity>` avec l'éditeur ouvert (Unity se désynchronise) : fermer Unity ou forcer un reimport.

## Dépannage rapide

| Problème | Commande |
|---|---|
| Annuler le dernier commit (garder les changements) | `git reset --soft HEAD~1` |
| Changer le message du dernier commit (pas encore poussé) | `git commit --amend` |
| Mettre de côté des changements | `git stash` puis `git stash pop` |
| Voir l'historique en graphe | `git log --oneline --graph --all` |
| J'ai commité sur `develop` par erreur (pas poussé) | `git switch -c feat/xxx` puis `git branch -f develop origin/develop` |
