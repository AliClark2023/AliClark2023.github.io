---
layout: post
title:  "Synaptic (Dare Academy)"
date:   2025-08-30 09:47:52 +0100
categories: Further Development
displayImage: assets/img/dareDemo.gif
---
Dare Academy 2025 project in UE 5.4
<!--more-->

## Skills Developed
- Creating controller functionality
- Reiterating on past code
- Animation blueprints
- Sound attenuation fields/attributes
- Light attenuation fields/attributes
- Identifying optimization areas

# ---Document-in-Progress---
![DCAEvent]({{ site.baseurl }}/assets/img/DCAEvent.jpg)
Continuing the project from DES315 my team (Bonny Bandits) have improved upon "Synaptic" during the summer and have showcased our game to the public at the Dundee Contempoary Arts (DCA) building during its annual Drop-in and Play event.

Link to the build used at the event: [DCAFinalBuild][build]

<iframe width="560" height="315" src="https://www.youtube.com/embed/GeDYPSRBskA?si=0DIg8njw1VeBaS0D" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
<br>



## Breakdown
##### Goals
During DARE feedback from the mentors and discussion with the team members it was decided that we would iterate on:
- Retool narrative 
- Record new narrative lines
- Redesign playable levels into a more shorter, segemented design
- Adjust target behaviours and add new ones
- Adjust weapon mechanics
- Add controller support

As system programmer for the team my job was to retool the systems to accomodate these proposed changes, starting with the major one: 

##### Level activation
Since the levels where being redesigned into shorter more intense segments the previous target activation system needed to be expanded upon.

Previously, upon activation, the level barriers would query the game world for all objects with the target interface. While this worked for the beta build it was very resource intensive and would not scale well.

![Barrier Target Trace]({{ site.baseurl }}/assets/img/BarrierTargetTrace.png)
*targets detected by barrier*

To remedy this, the barrier was modified to include an activation volume in which it will query this space for the targets.
This allows each level to be split into segments and allows the designer to add/remove as many targets as necessary.

As a consequence of this change, it was found that with the addition of these segments (and the number of targets increased dramatically) performance started to drop.
In investigating this problem it was found that it was the number of targets being rendered in the game level were causing the performance issues.
To fix this, a spawner object was created that did not render anything in-game. It allowed the designer what target to spawn, when to activate the target and which (when applicable) track for the target to traverse on.

#### Diary Page unlocks
Another system to iterate on was the diary page unlock system. Previously, a set number of pages to unlock (determined by designer) were assigned to each level and unlocked pages where then signaled to the game mode when the player travels back to the main hub area.
For this new segmented design, a singular lore page is unlocked after the end of each shooter segment. This page is then able to be displayed in game when the player interacts with a new object (statue) and also unlocks the entrance to the next area.

![Statue object]({{ site.baseurl }}/assets/img/Statue.png)
*Statue in-game*

[build]: https://bonny-bandits.itch.io/synaptic/devlog/1029909/final-synaptic-build