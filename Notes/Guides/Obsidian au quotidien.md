---
graph-size: 300
---
#guide

Lien retour : [[Home]] · Aide : [[Aide]]

# Obsidian au quotidien

Ce vault réunit la doc technique, les guides et les comptes rendus de réunion de l'équipe. Les tâches sont suivies sur GitHub (voir [[Guide des issues GitHub]]).

L'installation et la première ouverture sont décrites dans le `README.md` du vault, à la racine de `Transcendence_obsidian/`.

## Récupérer la dernière version

Avant toute modification :

```sh
cd ft_transcendence/Transcendence_obsidian
git pull
```

Ou, depuis `ft_transcendence/` : `make setup`.

Sans cette étape, deux personnes risquent de modifier la même note, et git le signale par un conflit au moment du push.

## Où ranger une note

| Contenu | Dossier |
|---|---|
| Un module du jeu Unity | `Notes/Game/<module>/` |
| Le site, l'API, l'infra | `Notes/Web/<partie>/` |
| Un guide pour l'équipe | `Notes/Guides/` |
| Un compte rendu de réunion | `Notes/Réunions/` |
| Un modèle de note | `Notes/Modèles/` |

En cas de doute, s'aligner sur les notes voisines, ou poser la question sur Discord.

## Créer une note

1. Dans l'explorateur de fichiers (barre de gauche) : clic droit sur le dossier → **New note**.
2. Lui donner un nom explicite : c'est ce nom qui sert aux liens vers elle.
3. Reprendre l'en-tête des autres notes :

   ```markdown
   ---
   graph-size: 300
   ---
   #web

   Lien retour : [[Home]]
   ```

   Le tag (`#web`, `#game`, `#guide`, `#reunion`…) permet de filtrer les notes, et `graph-size` règle la taille du nœud dans le graphe.

## Créer des liens

| Syntaxe | Résultat |
|---|---|
| `[[Git Workflow]]` | Lien vers la note |
| `[[Git Workflow#Dépannage rapide]]` | Lien vers une section précise |
| `[[Git Workflow\|guide git]]` | Lien avec un autre texte affiché |

Après avoir tapé `[[`, Obsidian propose les notes existantes. **Ctrl+clic** sur un lien l'ouvre dans un nouvel onglet.

Les liens entre notes apparaissent dans le graphe (voir [[Graph Guide]]).

## Retrouver une note

| Raccourci | Effet |
|---|---|
| **Ctrl+O** | Ouvrir une note par son nom |
| **Ctrl+Shift+F** | Rechercher un mot dans tout le vault |
| **Ctrl+P** | Palette de commandes : toutes les actions d'Obsidian |

Le panneau **Outline**, dans la barre de droite, affiche le plan de la note ouverte : c'est le moyen le plus simple de naviguer dans une note longue.

## Préparer une réunion

1. Clic droit sur `Notes/Réunions/` → **New note**, nommée par exemple `2026-11-23 Réunion`.
2. **Ctrl+P** → **Templates: Insert template** → **Réunion**.
3. La note se remplit avec la date du jour et les sections habituelles : présents, ordre du jour, décisions, actions.
4. Ajouter un lien vers la note dans [[Home]].

## Publier ses modifications

Les notes se poussent **directement sur `main`** du vault, sans branche ni PR :

```sh
cd ft_transcendence/Transcendence_obsidian
git pull
git status                                  # vérifier la liste des fichiers modifiés
git add "Notes/Web/Ma note.md"              # n'ajouter que ses propres notes
git commit -m "docs(web): add the chat note"
git push
```

Le message suit le même format que dans le dépôt principal : `docs(<sujet>): <description>`, en anglais.

## Problèmes fréquents

**Git signale des changements dans `.obsidian/` qui n'ont pas été faits volontairement.**
Obsidian réécrit sa configuration de lui-même. Ces changements ne doivent pas entrer dans le commit : utiliser `git add` avec le chemin des notes, jamais `git add -A`. Pour les annuler : `git restore .obsidian/`.

**Un fichier de `.obsidian/` doit être modifié à la main.**
Quitter d'abord complètement Obsidian : il réécrit sa configuration en quittant, et écraserait la modification.

**Dans `ft_transcendence`, git affiche `Transcendence_obsidian` comme modifié.**
C'est normal : le pointeur du sous-module a avancé. **Ne pas le commiter** dans le dépôt principal.

**`git pull` signale un conflit sur une note.**
Ouvrir la note : git y a placé les deux versions entre les marqueurs `<<<<<<<`, `=======` et `>>>>>>>`. Garder le bon texte (souvent les deux), supprimer les marqueurs, puis :

```sh
git add "Notes/la note.md"
git commit
git push
```

**Les onglets ouverts ne sont pas partagés avec les autres membres.**
C'est voulu : `workspace.json` reste propre à chaque poste.
