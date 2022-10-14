---
id: D#sddx0c
date: 05/10/2022
type: node
status: digital
aliases: [D#sddx0c]
tags:
  - Blender
---

# Effect of Modifier Order in Blender

Modifiers are an amazing feature of Blender: [[blender_modifiers|D#d73iqq]].

The order in which modifiers is applied to an object affects its resulting mesh.

Consider we have a mesh that we need to:

1. Solidify
2. Subdivide

First we look at how the the object looks when the "solidify" modifier is "on top" (evaluated before) the "subdivide" modifier:

![[image-20221005151733907.png]]


Now let's reverse the order:

![[image-20221005151747497.png]]



Note how the second image shows a thicker "wall".

The reason this happens is because the "solidify" modifier adds blunt thickness, while the "subdivide modifier" is used to split the faces of a mesh into smaller faces, giving it a smooth appearance.

So simply put, the discrepancy is there because we "smoothed before adding thickness" instead of "adding thickness then smoothing". The latter causes the "newfound thickness" to be smoothed, while the former doesn't.

---

#### Bibliography

[prs]: [Beginner Donut Blender Tutorials, Blender Guru 2021 - part 3](https://youtube.com/watch?v=7wKnPclzYY8)