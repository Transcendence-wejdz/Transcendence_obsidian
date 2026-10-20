---
graph-size: 200
fichiers:
  - "[[ProceduralMapGenerator.cs]]"
  - "[[ProceduralMapGenerator.Noise.cs]]"
  - "[[ProceduralMapGenerator.Decor.cs]]"
  - "[[ProceduralMapGenerator.Preview.cs]]"
  - "[[ProceduralMapGeneratorEditor.cs]]"
  - "[[ProceduralMapGeneratorPreviewHooks.cs]]"
  - "[[SeaClouds.cs]]"
  - "[[DecorFlipbook.cs]]"
  - "[[SiblingRuleTile.cs]]"
  - "[[SortingLayer_AutoEditor.cs]]"
---
#module #game

Génération procédurale de la map. `ProceduralMapGenerator` est une classe `partial` éclatée par préoccupation. Le terrain est plat : terre, eau et décor (plus de plateformes, murs ni escaliers depuis le 2026-09-08).

## Fonctionnement

- **Seed** (section Generation) : pilote tous les bruits et choisit le biome de la map (`seed % nombre de biomes`).
- **Biomes** : un seul biome par map. Chaque biome a ses `groundTiles` (réparties en taches par le Ground Noise), son `decor` et son `spawnSafeRadius` (zone de terre sans décor autour du spawn).
- **Île** : `islandRadius` > 0 transforme la map en île à côte irrégulière (`islandEdgeVariation`, `islandEdgeNoiseScale`) ; tout est de l'eau au-delà. `decorCoastOffset` limite le décor à la côte plus N cases (négatif = reste dans les terres). 0 = map infinie.
- **Preview éditeur** : `previewInEditor` génère la map dans la Scene view et se met à jour à chaque changement d'inspecteur. Elle est effacée avant chaque sauvegarde et en Play mode, et ne marche que dans une scène (pas en Prefab mode).
- Les réglages se font dans la scène `Coop` (biomes Forest, Plains, Rocky). `MapGenerator.prefab` n'est utilisé par aucune scène.

## Scripts

- <a href="#vault://../UnityProject/Assets/Scripts/Terrain/Procedural/ProceduralMapGenerator.cs" class="LinkRelativeTo">Procedural/ProceduralMapGenerator.cs</a> : champs sérialisés, biomes, streaming de chunks autour du joueur local
- <a href="#vault://../UnityProject/Assets/Scripts/Terrain/Procedural/ProceduralMapGenerator.Noise.cs" class="LinkRelativeTo">Procedural/ProceduralMapGenerator.Noise.cs</a> : bruit Perlin pour l'eau, la côte de l'île et les tiles de sol ; `IsWaterAtWorldPosition` pour les autres systèmes
- <a href="#vault://../UnityProject/Assets/Scripts/Terrain/Procedural/ProceduralMapGenerator.Decor.cs" class="LinkRelativeTo">Procedural/ProceduralMapGenerator.Decor.cs</a> : placement et pooling du décor du biome
- <a href="#vault://../UnityProject/Assets/Scripts/Terrain/Procedural/ProceduralMapGenerator.Preview.cs" class="LinkRelativeTo">Procedural/ProceduralMapGenerator.Preview.cs</a> : preview en mode éditeur (`#if UNITY_EDITOR`)
- <a href="#vault://../UnityProject/Assets/Scripts/Terrain/Procedural/Editor/ProceduralMapGeneratorEditor.cs" class="LinkRelativeTo">Procedural/Editor/ProceduralMapGeneratorEditor.cs</a> : inspecteur custom par sections, bouton Regenerate Preview
- <a href="#vault://../UnityProject/Assets/Scripts/Terrain/Procedural/Editor/ProceduralMapGeneratorPreviewHooks.cs" class="LinkRelativeTo">Procedural/Editor/ProceduralMapGeneratorPreviewHooks.cs</a> : efface la preview avant sauvegarde et Play mode, la régénère après
- <a href="#vault://../UnityProject/Assets/Scripts/Terrain/SeaClouds.cs" class="LinkRelativeTo">SeaClouds.cs</a> : nuages qui dérivent autour de la caméra, sur le sorting layer `Sky` (au-dessus de tout)
- <a href="#vault://../UnityProject/Assets/Scripts/Terrain/DecorFlipbook.cs" class="LinkRelativeTo">DecorFlipbook.cs</a> : sprites de décor animés en flipbook
- <a href="#vault://../UnityProject/Assets/Scripts/Terrain/SiblingRuleTile.cs" class="LinkRelativeTo">SiblingRuleTile.cs</a> : RuleTile dont les voisins "sibling" sont les autres biomes de sol, pour que les biomes se touchent sans bordure
- <a href="#vault://../UnityProject/Assets/Scripts/Terrain/Editor/SortingLayer_AutoEditor.cs" class="LinkRelativeTo">Editor/SortingLayer_AutoEditor.cs</a> : inspecteur custom pour `SortingLayer_Auto` (voir [[Core]])

## Tiles de sol

Les `GroundToWater/Ground_N` (AutoTile 3x3) sont la source graphique. Les `GroundSiblingRule/Ground_N_Rule` (SiblingRuleTile) en sont générés : une règle par masque de l'AutoTile, les coins ne comptant que si leurs deux côtés sont présents. Si un AutoTile est retouché, il faut régénérer la règle correspondante.

## Connexions

- Le décor utilise [[Core]]`/SortingLayer_Auto` pour son tri de rendu
- [[Enemies]] : `WaveSpawner` évite l'eau via `IsWaterAtWorldPosition`
