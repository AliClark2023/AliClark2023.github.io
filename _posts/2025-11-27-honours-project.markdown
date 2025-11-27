---
layout: post
title:  "Honours Project: Hex Grid Procedural Generation"
date:   2025-11-27 09:47:52 +0100
categories: University Project
displayImage: assets/img/WorldGenGif1.gif
---
UE 5.6 Cave Map Generation
<!--more-->

## Skills Developed
- c++ to blueprints
- pathway algorithms
- landscape algorithms
- gameplay mechanics generation

Link to up-to-date project: [Up-to-date build][UBuild]

# ---Project-In-Progress---
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