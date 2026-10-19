# Transcendence_obsidian

Vault Obsidian de l'équipe ft_transcendence. Il vit comme sous-module dans `ft_transcendence/Transcendence_obsidian/` et ses notes pointent vers les vrais fichiers du projet (`UnityProject/`, `web/`), donc il doit être ouvert **depuis le repo principal**, pas cloné seul.

## Premier setup

1. **Récupérer le vault avec le repo principal**

   ```sh
   git clone --recurse-submodules --remote-submodules git@github.com:Transcendence-wejdz/ft_transcendence.git
   cd ft_transcendence
   make setup
   ```

   Déjà cloné sans le vault : `make setup` suffit (il le récupère et le met sur le dernier `main`).

2. **Installer Obsidian** : [obsidian.md](https://obsidian.md/download).

3. **Ouvrir le vault** : Obsidian → *Open folder as vault* → choisir `ft_transcendence/Transcendence_obsidian` (le dossier dans le repo principal).

4. **Activer les plugins** : à l'ouverture, Obsidian demande si tu fais confiance à l'auteur du vault → **Trust author and enable plugins**. Les plugins sont déjà dans le repo, rien à installer :
   - Extended Graph et Sync Graph Settings : couleurs du graphe
   - Kanban : tableau `Todo`
   - External File Embed and Link : liens vers les fichiers du projet
   - Git History

   Si tu as cliqué sur l'autre bouton : Settings → Community plugins → *Turn on community plugins*.

5. **Charger le layout de l'équipe** : palette de commandes (`Ctrl+P`) → *Manage workspace layouts* → `ft_transcendence` → **Load**. Ça ouvre le tableau Todo, le graphe local et les panneaux comme pour tout le monde.

6. **Vérifier** :
   - le graphe local (panneau de droite) est en couleurs, une couleur par dossier ;
   - les colonnes du tableau `Todo` sont colorées (snippet CSS `kanban-lanes`, déjà activé dans Settings → Appearance → CSS snippets) ;
   - les liens vers les fichiers `.cs` / `.ts` s'ouvrent.

   Graphe sans couleurs : recharger le layout `ft_transcendence` (étape 5).

7. Commencer par la note **Home**, puis **Git Workflow** (règles git de l'équipe, et la config email à faire une fois pour que tes commits comptent sur GitHub).

## Au quotidien

- Mettre à jour le vault : `make setup` depuis `ft_transcendence/` (ou `git pull` dans `Transcendence_obsidian/`).
- Modifier une note : commit et push **directement sur `main` de ce repo**, pas de PR, et pas de commit dans le repo principal pour le pointeur du sous-module.
- `workspace.json` (onglets ouverts, état de ta fenêtre) reste local, c'est voulu. Pour partager un nouveau layout : *Manage workspace layouts* → **Save** sous `ft_transcendence`, puis commit `.obsidian/workspaces.json`.
- Toujours **quitter Obsidian** avant de modifier à la main un fichier de `.obsidian/` : il réécrit sa config en quittant.
