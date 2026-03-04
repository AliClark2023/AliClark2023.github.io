---
layout: post
title:  "Honours Project: Hex Grid Procedural Generation"
date:   2026-03-04 09:47:52 +0100
categories: University Project
displayImage: assets/img/HPDemoGif.gif
---
UE 5.6 Cave Map Generation
<!--more-->

## Skills Developed
- c++ to blueprints
- pathway algorithms
- landscape algorithms
- UI implementation
- Save & loading system

Link to up-to-date project: [Up-to-date build][UBuild]

# ---Project-In-Progress---
## 04/03/26
<iframe width="560" height="315" src="https://www.youtube.com/embed/mPZAbz5Ou28?si=RAc1isJ5nh-6A1i7" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
<br>
Huge changes to project since November with the main changes being:
- Tighter focus on path generation instead of multiple layers
- All path techniques integrated into project (Perlin Worms, DLA & Cellular Automata)
- Save & loading system implemented to use generated map layouts on demand
- Player character implemented for playtest & exploring generated layouts
- Specific tiles added that trigger the end of a level or move player to next layer of map layout
- Playtest UI and system implemented

### Map Generation
Landscape, region and layer generation remains similar to the November build, with the main changes being how the path generation is performed.
Can now specify which pathway algorithm is being used as well as its unique parameters. When specified, the layout can then be saved to a data asset file which can then be used for loading and testing.

### Island detection & Joining
With the addition of multiple pathway techniques, a problem arose that the algorithms can generate pathways that were non-contiguous and isolated from each other. To fix this, a method of island detection using a flood-fill technique called Breadth-First Search (BFS) was implemented. 
After islands are detected a method was then employed to join them by: 
- calculating the centroids of the islands (noting that this can produce incorrect tiles if the island shape is concave)
- drawing a line between island centroids and returning all grid coords fall within that line (requires converting Even-Q grid coords to cube coords)
- changing these returned tiles into path tiles

### Path Generation
Drunkard Walk implementation remains the same but have added the following algorithms:

#### Perlin Worms
Modifies the Perlin noise function used by generating the landscape into a set amount of user defined "Worms" that create pathways either at random points within the grid or joins these worms together to create a singular pathway.
Number, length, frequency and seed parameters can all be adjusted to change the behaviours of these worms.
Island detection & joining is applied after generation to ensure valid layout.

#### Diffuse-Limited Aggregation (DLA)
Employs multiple specific drunkards walks around a starting "Seed" area to generate the pathways. Each walker travels until it comes into contact with a path tile, in which its previous tile becomes a path and the walker dies. Process is repeated until a layout size has been met.
3 types of DLA are implemented:
- Inwards: Walks are performed at random points throughout the map and travels towards the seed area.
- Outward: Walks are performed at random points within the starting seed area towards the map boundaries.
- Central: Similar to Inwards but a line is drawn from walkers starting point to the centre of the map and the walker follows this route.

#### Cellular Automata
Considers all tiles within a grid as either Path or non-Path. Changes the state of these tiles depending on the states of the surrounding neighbouring tiles. Many rules exist for this type of generation but only two methods are implemented within the project. Currently only considers immediate neighbours (1 tile away) and can progress iteration of generation to produce differing layouts.

- Wolfram codes: system that determines the existing tiles state based on the outcome of its Northwest, Central and Northeast neighbours. A config parameter was added that allows the editor to alter all possible neighbour states (8 combinations) and their resultant state. With this system known wolfram codes can be entered and performed on the current map layout.
- Game of Life: considers all neighbouring tile states to determine the current state according to the number of Path tiles (alive) or non-Path (dead) tiles. This depends on the following adjustable parameters: 
    - Death limit: determines number of dead tiles needed to kill central tile if it was alive.
    - Birth limit: determines number of alive tiles needed to make central tile also alive.

### Playtesting
UI environment:
![UIMenu]({{ site.baseurl }}/assets/img/MenuSS.png)

In-game environment:
![In-Game]({{ site.baseurl }}/assets/img/InGameSS1.png)
For the dissertation side of the project, a build is created that employs a testing environment containing a UI and multiple saved layouts for participants to explore. The goal of the environment is for the player to explore the layout with a controlled character and reach a specified exit tile. Questions about the layouts are then asked of the particpant regarding the nature and suitability of the layout.

Currently this aspect of the project is for internal University use only but may be opened up in the future.

## 27/11/25
<iframe width="560" height="315" src="https://www.youtube.com/embed/RQ8pqYNIEN0?si=CnMCo62koo0OrYL3" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
<br>

This project will look at the effectiveness of multiple procedural generation technqiues in generating a cave system for isometric games.
Goal of project is to create a continuous game map by stacking multiple layers of procedural generated levels.

Link to 27/11/25 build: [Demo][FBuild]

The current formation structure:

### pathway generation
Uses drunkards walk to generate a path from a designated start point until a specified path size or iteration limit has been met.
Iteration ends when path is no longer able to proceed (all surrounding neighbouring tiles have already been visited) or has met path size.

### landscape generation
Uses UE defualt perlin noise to adjust all height values of landscape tiles. This can be adjusted by modifying the noise scale and the height multipler which governs the max height of the generation.

### Region generaion
Voronoi regions are created by using seed locations planted at random within the grid. TIles calculate and are assigned to the seed location they are closest to. 
Number of seeds can be adjusted but currently there are only 5 unqiue biomes immplemented.

### Level formation
Combining each of the previous techniques generates a map with random characteristics

### World formation
Specifying how many layers to generate will perform the level formation for each layer. The result is that each layer will have its own unque properties. 

### Current development notes
At time of this post, all layered levels will share the same generation parameters (output still random) but will be individually assigned in later builds
Perlin noise is currently normalised to give a flat base, this is for testing and will be reverted in future builds.
Other notable developments are in the readme of the project files.

![LayerStack]({{ site.baseurl }}/assets/img/WorldGenGif2.gif)

[UBuild]: https://github.com/AliClark2023/HonorsTesting/tree/main
[FBuild]: https://github.com/AliClark2023/HonorsTesting/tree/FeasibilityDemo