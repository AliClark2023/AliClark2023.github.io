---
layout: post
title:  "Synaptic (Dare Academy)"
date:   2025-08-30 09:47:52 +0100
categories: Dare Academy
displayImage: assets/img/dareDemo.gif
---
# ---Work-in-Progress---
![DCAEvent]({{ site.baseurl }}/assets/img/DCAEvent.jpg)
Continuing the project from DES315 my team (Bonny Bandits) have improved upon "Synaptic" during the summer and have showcased our game to the public at the Dundee Contempoary Arts (DCA) building during its annual Drop-in and Play event.

Link to the build used at the event: [DCAFinalBuild][build]

<iframe width="560" height="315" src="https://www.youtube.com/embed/GeDYPSRBskA?si=0DIg8njw1VeBaS0D" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
<br>
The following is a breakdown on what was improved upon during the DARE event.

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

To remedy this, the barrier was modified to include an activation volume () in which it query this space alone for the targets.


[build]: https://bonny-bandits.itch.io/synaptic/devlog/1029909/final-synaptic-build