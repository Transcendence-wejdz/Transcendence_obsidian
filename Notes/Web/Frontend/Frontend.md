---
graph-size: 200
fichiers:
  - "[[web/backend/sveltekit/src/routes/+layout.svelte|+layout.svelte]]"
  - "[[web/backend/sveltekit/src/hooks.server.ts|hooks.server.ts]]"
  - "[[web/backend/sveltekit/src/lib/styles/tokens.css|tokens.css]]"
---
#module #web

Lien retour : [[Web Overview]]

Le site est une app **SvelteKit** (Svelte 5, TypeScript, `adapter-node`) dans `web/backend/sveltekit/`. Elle sert à la fois les pages et l'API `/api/…`. État au 19/11/2026.

## Stack

| Rôle | Outil |
|---|---|
| Framework | SvelteKit 2, Svelte 5 (runes) |
| Composants interactifs (menus, listes, fenêtres) | Bits UI |
| Toasts | svelte-sonner |
| Traductions | Paraglide (en, fr, es) |
| Polices | `@fontsource` (Pirata One, Pixelify Sans, Inter), servies par le site |
| Maquette de référence | V3, en HTML statique (hors repo). Accueil et how-to-play dans `Notes/Web/` |

## Arborescence

- <a href="#vault://../web/backend/sveltekit/src/routes" class="LinkRelativeTo">src/routes/</a>
  - `(public)/` : accueil, `login`, `register`, `about`, `privacy`, `terms`, `styleguide` (dev seulement)
  - `(app)/` : pages réservées aux joueurs connectés : `game`, `settings`, `friends-list`
  - `api/` : les endpoints
  - `+error.svelte` (404 / 500) et `src/error.html` (secours si le layout plante)
- <a href="#vault://../web/backend/sveltekit/src/hooks.server.ts" class="LinkRelativeTo">src/hooks.server.ts</a> : à chaque requête, lit la session et redirige vers `/login?redirectTo=…` pour les pages de `(app)/`
- <a href="#vault://../web/backend/sveltekit/src/lib/components/ui" class="LinkRelativeTo">src/lib/components/ui/</a> : composants réutilisables
- `src/lib/components/` : composants propres au site (Topbar, menu du compte, Footer, `LegalPage`, `PixelNumber`)
- <a href="#vault://../web/backend/sveltekit/src/lib/styles/tokens.css" class="LinkRelativeTo">src/lib/styles/tokens.css</a> : les design tokens (couleurs, tailles, polices)
- `src/lib/assets/emblems/` : emblèmes pixel-art des 5 classes
- `src/lib/types.ts` : types partagés front / back (le contrat d'API en code)

## Pages

| Page | État |
|---|---|
| `+error.svelte`, `/about`, `/privacy`, `/terms` | ✅ Faites d'après la maquette. `/about` : CTA et équipe à finaliser |
| `/` | Refaite d'après la maquette V3, traduite (branche `feat/web-home-page`, PR à ouvrir) |
| `/how-to-play` | Maquette faite (`Notes/Web/Maquette how-to-play.html`), page à coder |
| `/login`, `/register` | Anciennes versions, à refaire avec les composants |
| `/settings` | Ancienne version. Prévue en 3 sections : Profil, Compte, Préférences |
| `/game` | ✅ Charge le build Unity ; la Topbar n'apparaît qu'au survol |
| `/friends-list` | Faite par A et erbuffet |
| `/profile/[name]`, `/leaderboard` | À faire |
| `/chat`, notifications | À faire (A) |

**Décidé le 17/11/2026 : pas d'OAuth 42 ni de 2FA**, seulement email et mot de passe. Les maquettes `login-2fa` et `settings-security` sont gardées au cas où.

## Design system

- **`ui/`** : `Button` (4 variantes, 2 tailles, lien, occupé), `Input`, `Label`, `Card` (parchment / board), `Avatar`, `Tag`, `Ribbon`, `Modal` (Bits UI `AlertDialog`), `Toaster` (svelte-sonner).
- **Topbar** : navigation invité / connecté, sélecteur de langue, menu du compte (Bits UI `DropdownMenu`).
- **`/styleguide`** : montre chaque composant dans tous ses états, seulement avec `npm run dev`.

## Traductions (i18n)

Fusionnée dans `develop` (PR #119).

- Les textes sont dans `messages/en.json`, `fr.json`, `es.json`. Dans un composant : `{m.nav_play()}`.
- La langue vient du cookie `PARAGLIDE_LOCALE`, sinon de la langue du navigateur, sinon l'anglais. Pas de langue dans l'URL.
- Traduits : Topbar, menu du compte, Footer et l'accueil. Le reste des pages est encore en anglais en dur.
- Noms des classes partagés : `class_warrior` … `class_pawn` (en français, le Pawn devient « Péon »).
- Pour ajouter un texte traduit : voir [[Ajouter une clé i18n]].

## Conventions

- Couleurs et tailles toujours via les tokens (`var(--color-gold)`). `rem` pour ce qui se lit, `px` pour bordures, arrondis et ombres.
- Chaque page est comparée à la maquette avant d'être commitée.
- `npm run check` doit rester à 0 erreur. Après un pull qui modifie le schéma Prisma : `npm run db:generate`.
- Navigateur de référence : Chrome.

## Connexions

- Sert aussi l'API et lit la base via Prisma : voir [[Server]].
- Derrière nginx, en HTTPS : voir [[Infra]].
- `/game` charge le build WebGL de [[Game Overview]] depuis `static/public/game/`, et lui envoie le profil du joueur.
- Tâches en cours : [[Todo]].
