---
title: "Mini Jam 121: Reflection"
date: 2023-03-09
---

Mini jam is a 72-hour-long video game development jam that occurs every two weeks on Itch.io. I took part in the #121 Jam and successfully submitted a game which you can [play here](https://smallmiracles.itch.io/asteroid-storm). 

The jam's theme was Reflection. The limitation that games had to follow was: Windows as a Mechanic.

The [reflection](https://commons.wikimedia.org/wiki/File:F%C3%A9nyvisszaver%C5%91d%C3%A9s.jpg#/media/File:Fényvisszaverődés.jpg) theme immediately made me think of bouncing some form of laser from a surface. At first I implemented a quick prototype for bullets that reflect when they hit an object. I struggled with how the platforms should be arranged to give the player enough interesting options for targeting to take advantage of bullets bouncing multiple times. It started to come together when the plattforms where arranged around the player. At this point I had the idea of making the player control a space station with revolving platforms. The space station would shoot a laser which could be reflected and bounce of from these platforms. The "enemies" would be asteroids that threaten to crash into the space station and the player would have to use the laser to keep the station from getting destroyed. What follows is the code to make this reflection laser work in Unity, how to detect collisions with asteroid to determine which should get destroyed and how to show the laser in game using Unity's LineRenderer with an emissive material. The full repository is [here](https://github.com/Small-Miracles/asteroid-storm).

{% gist 8f98635924d5fce8d2562db0fcb81b2f ShootLaser.cs %}

Visualize the laser by creating a GameObject with attached LineRenderer component. Add a script which draws line segments between each entry in the resulting `List<Vector2> hitPoints`. 

To give the LineRender a glowing look:
* create a new URP shader graph "Lit Shader Graph"
* add Color input with mode set to HDR
* connect this color node to the Fragment base color
* create a material for this shader and assign it to the line-renderer
* add "Bloom" as a post-processing effect using URP
* increase the color intensity in the material to add more glow

That's it. Overall I really enjoyed this jams theme and limitation, although I wouldn't say that my game followed the "Windows as a Mechanic" that closely.
