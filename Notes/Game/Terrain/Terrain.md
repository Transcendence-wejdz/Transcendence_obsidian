---
graph-size: 200
fichiers:
  - "[[ProceduralMapGenerator.cs]]"
  - "[[ProceduralMapGenerator.Noise.cs]]"
  - "[[ProceduralMapGenerator.Decor.cs]]"
  - "[[ProceduralMapGeneratorEditor.cs]]"
  - "[[DecorFlipbook.cs]]"
  - "[[SiblingWallRuleTile.cs]]"
  - "[[SortingLayer_AutoEditor.cs]]"
---
#module #game

Génération procédurale de la map. `ProceduralMapGenerator` est une classe `partial` éclatée par préoccupation. **Note** : la génération de plateformes/murs/escaliers a été supprimée (2026-09-08) — le terrain actuel est uniquement land/water/décor plat.

## Scripts

- <a href="#vault://../UnityProject/Assets/Scripts/Terrain/Procedural/ProceduralMapGenerator.cs" class="LinkRelativeTo">Procedural/ProceduralMapGenerator.cs</a> — boucle de streaming de chunks, `System.Random` seedé par chunk pour une régénération déterministe
- <a href="#vault://../UnityProject/Assets/Scripts/Terrain/Procedural/ProceduralMapGenerator.Noise.cs" class="LinkRelativeTo">Procedural/ProceduralMapGenerator.Noise.cs</a> — sampling de bruit Perlin pour biomes/eau
- <a href="#vault://../UnityProject/Assets/Scripts/Terrain/Procedural/ProceduralMapGenerator.Decor.cs" class="LinkRelativeTo">Procedural/ProceduralMapGenerator.Decor.cs</a> — placement du décor
- <a href="#vault://../UnityProject/Assets/Scripts/Terrain/Procedural/Editor/ProceduralMapGeneratorEditor.cs" class="LinkRelativeTo">Procedural/Editor/ProceduralMapGeneratorEditor.cs</a> — inspecteur custom
- <a href="#vault://../UnityProject/Assets/Scripts/Terrain/DecorFlipbook.cs" class="LinkRelativeTo">DecorFlipbook.cs</a> — sprites de décor animés en flipbook
- <a href="#vault://../UnityProject/Assets/Scripts/Terrain/SiblingWallRuleTile.cs" class="LinkRelativeTo">SiblingWallRuleTile.cs</a> — `TileBase` pour le matching de tiles de mur (hérité de l'époque où les murs existaient — à vérifier si encore utilisé)
- <a href="#vault://../UnityProject/Assets/Scripts/Terrain/Editor/SortingLayer_AutoEditor.cs" class="LinkRelativeTo">Editor/SortingLayer_AutoEditor.cs</a> — inspecteur custom pour `SortingLayer_Auto` (voir [[Core]])

## Connexions

- Le décor utilise [[Core]]`/SortingLayer_Auto` pour son tri de rendu
- Testable isolément via la scène `Test/MapGenTest.unity` (voir [[Game Overview]])
