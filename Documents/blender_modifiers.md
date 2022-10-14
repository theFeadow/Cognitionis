---
id: D#d73iqq
date: 05/10/2022
type: node
status: digital
aliases: [D#d73iqq]
tags:
  - Blender
---

# Basics of Modifiers in Blender

In blender, using modifiers allows non-destructive operations to be performed on the model. For example, one can use the "Subdivision" modifier to add more detail to the mesh:

![[image-20221005145334010.png]]

The 'Levels Viewport' value controls the number of "subdivision operations" done and seen by the user during working in the viewport. The 'Render' value controls the subdivisions at render time.

What is really awesome is that these values could be changed at any time, even after doing some work on the model or adding other modifiers: they are non-destructive.

Modifiers are evaluated from top to bottom, so it is important to note the order of the modifiers applied to an object in the viewport. Checkout [[blender_modifier_order|D#sddx0c]].

Here's [an awesome video](https://www.youtube.com/watch?v=idcFMhoSdIc).

---

#### Bibliography

[prs]: [Beginner Donut Blender Tutorials, Blender Guru 2021 - part 3](https://youtube.com/watch?v=7wKnPclzYY8)