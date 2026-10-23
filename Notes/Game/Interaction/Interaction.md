---
graph-size: 200
fichiers:
  - "[[InteractableZone.cs]]"
  - "[[InteractionManager.cs]]"
  - "[[InteractPromptUI.cs]]"
---
#module #game

Système "press E" générique pour interagir avec les PNJ/objets du monde.

## Scripts

- <a href="#vault://../UnityProject/Assets/Scripts/Interaction/InteractableZone.cs" class="LinkRelativeTo">InteractableZone.cs</a> — marque un PNJ/objet comme interactible
- <a href="#vault://../UnityProject/Assets/Scripts/Interaction/InteractionManager.cs" class="LinkRelativeTo">InteractionManager.cs</a> : suit la zone la plus proche à portée du joueur ; la touche Interact referme le panneau qu'elle a ouvert, sauf si elle est aussi une touche de l'UI (ex. Croix), laissée alors à l'UI
- <a href="#vault://../UnityProject/Assets/Scripts/Interaction/InteractPromptUI.cs" class="LinkRelativeTo">InteractPromptUI.cs</a> — prompt "press E" en World Space, fixe par PNJ

## Connexions

- Les 4 PNJ du Lobby (Customize / Upgrades / Mode Select / Multiplayer) ouvrent chacun un [[UI]]`/MenuPanel` via ce système
