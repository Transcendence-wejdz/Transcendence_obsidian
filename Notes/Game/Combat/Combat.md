---
graph-size: 200
fichiers:
  - "[[IDamageable.cs]]"
  - "[[IHealthStats.cs]]"
  - "[[IAttackFX.cs]]"
  - "[[SlashAttackFX.cs]]"
  - "[[LayeredAttackFX.cs]]"
  - "[[ShieldHoldFX.cs]]"
  - "[[ArrowProjectile.cs]]"
  - "[[WorldHealthBar.cs]]"
  - "[[DamageNumberSpawner.cs]]"
  - "[[DamageNumberPopup.cs]]"
  - "[[SpriteHitFlash.cs]]"
  - "[[DummyStats.cs]]"
---
#module #game

Couche partagée entre [[Player]] et [[Enemies]] : interfaces de dégâts/santé, FX d'attaque, retours visuels.

## Scripts

- <a href="#vault://../UnityProject/Assets/Scripts/Combat/IDamageable.cs" class="LinkRelativeTo">IDamageable.cs</a> — contrat "peut recevoir des dégâts", implémenté par `Player.Stats`, `EnemyStats`, `DummyStats`
- <a href="#vault://../UnityProject/Assets/Scripts/Combat/IHealthStats.cs" class="LinkRelativeTo">IHealthStats.cs</a> — contrat lecture de vie/mana pour l'UI
- <a href="#vault://../UnityProject/Assets/Scripts/Combat/IAttackFX.cs" class="LinkRelativeTo">IAttackFX.cs</a> — contrat FX par capacité, piloté par [[ClassKit]]
- <a href="#vault://../UnityProject/Assets/Scripts/Combat/SlashAttackFX.cs" class="LinkRelativeTo">SlashAttackFX.cs</a> — FX de slash (attaque légère)
- <a href="#vault://../UnityProject/Assets/Scripts/Combat/LayeredAttackFX.cs" class="LinkRelativeTo">LayeredAttackFX.cs</a> — FX double-couche pour les Specials circulaires
- <a href="#vault://../UnityProject/Assets/Scripts/Combat/ShieldHoldFX.cs" class="LinkRelativeTo">ShieldHoldFX.cs</a> — FX du bouclier ultimate (Warrior)
- <a href="#vault://../UnityProject/Assets/Scripts/Combat/ArrowProjectile.cs" class="LinkRelativeTo">ArrowProjectile.cs</a> — projectile (Archer / ennemis à distance)
- <a href="#vault://../UnityProject/Assets/Scripts/Combat/WorldHealthBar.cs" class="LinkRelativeTo">WorldHealthBar.cs</a> — barre de vie au-dessus de la tête
- <a href="#vault://../UnityProject/Assets/Scripts/Combat/DamageNumberSpawner.cs" class="LinkRelativeTo">DamageNumberSpawner.cs</a> / <a href="#vault://../UnityProject/Assets/Scripts/Combat/DamageNumberPopup.cs" class="LinkRelativeTo">DamageNumberPopup.cs</a> — nombres de dégâts flottants
- <a href="#vault://../UnityProject/Assets/Scripts/Combat/SpriteHitFlash.cs" class="LinkRelativeTo">SpriteHitFlash.cs</a> — flash blanc au hit
- <a href="#vault://../UnityProject/Assets/Scripts/Combat/DummyStats.cs" class="LinkRelativeTo">DummyStats.cs</a> — cible d'entraînement (implémente `IDamageable`, variante `Dummy_Ally` pour tester heal/buff)

## Connexions

- Déclenché par [[Player]] (`Player.Actions`) et [[Enemies]] (`EnemyActions`)
- Cible toujours une `IDamageable` : joueur, ennemi, ou dummy
- FX réseau : la position d'un effet est **toujours recalculée localement**, jamais envoyée brute via RPC (piège connu, voir [[Networking]])
