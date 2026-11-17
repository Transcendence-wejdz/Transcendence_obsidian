---
graph-size: 150
---
#web #guide

Lien retour : [[Frontend]]

# Ajouter une clé i18n

Le site est traduit en anglais, français et espagnol avec **Paraglide**. Le sujet exige que **tout le texte visible** soit traduisible : chaque nouveau texte d'une page passe donc par une clé, jamais en dur dans le HTML.

## Où sont les textes

Dans `web/backend/sveltekit/messages/` :

| Fichier | Langue |
|---|---|
| `en.json` | Anglais, la langue de base |
| `fr.json` | Français |
| `es.json` | Espagnol |

Chaque fichier associe une **clé** à un texte :

```json
{
	"$schema": "https://inlang.com/schema/inlang-message-format",
	"nav_play": "Play",
	"footer_privacy": "Privacy Policy"
}
```

Le dossier `src/lib/paraglide/` est **généré** à partir de ces fichiers : ne jamais le modifier à la main. Il est dans le `.gitignore`.

## 1. Choisir le nom de la clé

Format `zone_élément`, en snake_case :

| Préfixe | Zone |
|---|---|
| `nav_` | Topbar |
| `account_` | Menu du compte |
| `footer_` | Footer |
| `<page>_` | Une page : `friends_`, `chat_`, `settings_`, `profile_`… |

Exemples : `friends_add_button`, `chat_empty_title`, `settings_save`.

Une clé = un texte. Si le même mot apparaît à deux endroits avec un sens différent, on fait deux clés.

## 2. L'ajouter dans les trois fichiers

La même clé, à la même place, dans `en.json`, `fr.json` et `es.json` :

```json
"friends_add_button": "Add friend",
```
```json
"friends_add_button": "Ajouter en ami",
```
```json
"friends_add_button": "Añadir amigo",
```

Attention aux virgules : chaque ligne finit par une virgule, sauf la dernière du fichier.

Si tu ne connais pas la traduction, mets le texte anglais dans les trois fichiers et signale-le dans ta PR : quelqu'un traduira.

## 3. L'utiliser dans un composant

```svelte
<script lang="ts">
	import { m } from '$lib/paraglide/messages.js';
</script>

<Button>{m.friends_add_button()}</Button>
```

Chaque clé devient une **fonction** : on l'appelle avec `()`.

**Dans un attribut**, sans guillemets :

```svelte
<nav aria-label={m.nav_main()}>
<input placeholder={m.friends_search_placeholder()} />
```

Les `aria-label`, `placeholder` et `title` se traduisent aussi : ils sont lus ou affichés.

## Un texte avec une variable

Dans les JSON, la variable s'écrit entre accolades :

```json
"friends_online_alert": "{name} just connected",
```
```json
"friends_online_alert": "{name} vient de se connecter",
```

Dans le composant, on passe sa valeur :

```svelte
{m.friends_online_alert({ name: friend.displayName })}
```

On ne découpe jamais une phrase en plusieurs clés (`"just"` + `"connected"`) : l'ordre des mots change d'une langue à l'autre.

## Ce qui ne se traduit pas

- Les **noms de langues** dans le sélecteur : « English », « Français », « Español » restent dans leur propre langue.
- Les **noms propres** : Transcendence, 42, Tiny Swords, les pseudos des joueurs.
- Les **données** venant de l'API ou de la base (`displayName`, scores…).

## Vérifier

1. `npm run check`, depuis `web/backend/sveltekit` : une clé mal écrite (`m.frineds_add_button()`) ou absente fait **échouer** la vérification.
2. `npm run dev`, puis changer de langue avec le sélecteur de la Topbar : la page se recharge dans la nouvelle langue.

Pour forcer une langue sans le sélecteur : dans les DevTools, onglet **Application** (ou **Stockage**), ajouter le cookie `PARAGLIDE_LOCALE` avec `fr` ou `es`, puis recharger.

## Connexions

- Mise en place et état des traductions : [[Frontend#Traductions (i18n)]].
