---
graph-size: 300
---
#guide

Lien retour : [[Home]] · Aide : [[Aide]]

# Relire une PR

Chaque Pull Request vers `develop` doit être relue par **deux autres membres** avant le merge, comme le demande le modèle de PR. La relecture vérifie que la PR fait ce que décrit l'issue, qu'elle ne casse rien, et que le code reste compréhensible par toute l'équipe : en correction, chaque membre doit pouvoir expliquer le projet.

Voir aussi : [[Git Workflow]] pour ouvrir une PR, [[Guide des issues GitHub]] pour le cycle d'une tâche.

## 1. Trouver les PR à relire

- GitHub envoie une notification à chaque demande de relecture.
- La liste complète s'obtient dans l'onglet **Pull requests** du dépôt, avec la recherche `is:open review-requested:@me`.
- Une PR en attente depuis longtemps peut être relue sans demande explicite.

## 2. Lire la PR

1. Onglet **Conversation** : lire la description et ouvrir l'issue liée. Sa section *Done when* indique ce que la PR doit accomplir.
2. Vérifier en bas de la page que la **CI est verte**. Si elle est rouge, le signaler à l'auteur avant d'aller plus loin.
3. Onglet **Files changed** : lire les fichiers un par un, et cocher **Viewed** en haut de chaque fichier lu.

## 3. Tester en local

Le code se lit, mais une page se teste. Récupérer la branche de la PR (son nom figure en haut de la PR, à côté de `develop`) :

```sh
cd ft_transcendence
git fetch origin
git switch feat/web-basic-chat      # nom de la branche de la PR
make up
```

Ouvrir https://localhost:4443 et reproduire les étapes de la section *How was this tested?* de la PR, en gardant la console du navigateur ouverte (F12) : le sujet exige zéro erreur.

Pour revenir ensuite sur `develop` :

```sh
git switch develop
```

## 4. Commenter

Dans l'onglet **Files changed** :

- **Commenter une ligne** : survoler la ligne, cliquer sur le **+** bleu, rédiger le commentaire, puis **Start a review**. Les commentaires suivants s'ajoutent à la même relecture avec **Add review comment**, et l'auteur les reçoit tous ensemble.
- **Proposer une correction** : dans le commentaire, cliquer sur l'icône **±** (*Add a suggestion*) et modifier la ligne. L'auteur peut l'appliquer en un clic.
- **Indiquer l'importance** : un commentaire qui commence par `nit:` signale un détail facultatif (nom de variable, mise en forme). Sans préfixe, le commentaire est à traiter.

Un commentaire porte sur le code, jamais sur la personne, et explique toujours pourquoi. Par exemple : « ce `fetch` n'a pas de gestion d'erreur : la page reste blanche si l'API ne répond pas », plutôt que « ça ne va pas ».

## 5. Rendre son verdict

En haut à droite de **Files changed** → **Review changes** (ou **Finish your review**), puis choisir :

| Choix | Quand |
|---|---|
| **Approve** | Tout est correct, ou il ne reste que des `nit:` |
| **Request changes** | Au moins un problème doit être corrigé avant le merge |
| **Comment** | Des questions restent ouvertes, sans verdict pour l'instant |

Valider avec **Submit review**.

## 6. Points à vérifier

- [ ] La CI est verte
- [ ] Le titre suit le format Conventional Commit, par exemple `feat(web): add the basic chat`
- [ ] La PR est liée à son issue et remplit la section *Done when*
- [ ] Testé en local dans Chrome, sans erreur dans la console
- [ ] Les formulaires sont validés côté serveur, pas seulement dans la page
- [ ] Aucun secret, mot de passe ou fichier `.env` dans le diff
- [ ] Aucun `console.log` ni code commenté oublié
- [ ] Une fois l'i18n en place : aucun texte visible écrit en dur
- [ ] Tout est rédigé en anglais : code, commentaires, description

## 7. Traiter les retours sur sa propre PR

1. Répondre à chaque commentaire : corriger, ou expliquer pourquoi le code reste tel quel.
2. Pousser les corrections sur la même branche : la PR se met à jour automatiquement.
3. Cliquer sur **Resolve conversation** sous chaque commentaire traité.
4. Redemander une relecture : icône ↻ à côté du nom du relecteur, dans la section **Reviewers** de la barre latérale.

Un commit poussé après une approbation doit être relu à son tour. Le relecteur retrouve les changements avec le menu **Changes from** → **Changes since your last review**, dans **Files changed**.

## 8. Après les deux approbations

L'auteur de la PR :

1. clique sur **Squash and merge**, en gardant le titre de la PR comme message ;
2. clique sur **Delete branch** ;
3. ferme l'issue liée, comme l'explique [[Guide des issues GitHub#6.6 Clôturer]].
