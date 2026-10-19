---
graph-size: 400
---
#home

Point d'entrée du vault. Ce vault vit dans le sous-module `Transcendence_obsidian` de `ft_transcendence` : les notes ci-dessous pointent directement vers les fichiers réels du projet (liens relatifs), et se lient entre elles en `[[wikilinks]]` pour que la vue **Graph** d'Obsidian dessine les connexions entre modules.

## Zones du projet

- [[Game Overview]] : jeu Unity (`UnityProject/`)
- [[Web Overview]] : webapp (`web/`)
- [[Todo]] : liste de tâches de l'équipe (tableau Kanban)
- [[Git Workflow]] : marche à suivre GitHub (branches, commits, PR, squash, release)

## Références

- <a href="#vault://../CLAUDE.md" class="LinkRelativeTo">CLAUDE.md</a> : instructions projet pour Claude Code (archi, conventions, workflow)
- <a href="#vault://../README.md" class="LinkRelativeTo">README.md</a> : readme du repo

## Comment lire ce vault

- Les notes d'index (une par module/dossier de scripts) listent les fichiers clés avec un lien direct vers le `.cs`/`.js` réel, et une section **Connexions** qui explique comment ce module parle aux autres.
- Clique sur l'onglet **Graph view** (icône de nœuds dans la barre latérale) pour visualiser tout ça : les notes de module seront des hubs, et tu verras visuellement quels modules sont couplés. Voir [[Graph Guide]] pour le code couleur et la navigation.
- Comme le vault = le repo, toute note créée ici est versionnée sur GitHub avec le reste du projet. `.obsidian/` est aussi versionné (config des plugins, couleurs, layout) sauf `workspace.json` qui reste local à chacun.
