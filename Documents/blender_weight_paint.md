---
id: D#5muz63
date: 12/10/2022
type: article
status: digital
aliases: [D#5muz63]
tags:
  - Blender
---

# Weight Painting Vertex Groups in Blender

In Blender, vertex groups allow tagging/assigning weight values to the vertices of a mesh, see [[blender_vertex_groups]].

Weight painting allows a quick and simple way of *assigning weights* to a vertex group ( / mesh ). While the most common use for weight painting is rigging meshes, other uses include controlling particle emissions and hair density. [^1]

The "assigned weights" range from 0 to 1.

---

## Using Weight Painting

Consider we have the following "donut icing" object:

![[image-20221012140444026.png]]

With the object selected, one could switch to the 'Weight Paint' interface:

![[image-20221012141144978.png]]
(..alternatively doing so using `Ctrl+Tab` and selecting the 'Weight Paint' option)

Now we "paint" different weights, like-a-so:

![[image-20221012142238403.png]]

Red colour keys for a value of '1', while dark blue is for '0'. The in-between colours key for for in-between values. Duh.

Note that with the "first stoke" of "weight-paint prush", a vertex group is created for the icing mesh:

![[image-20221012142537537.png]]


---

#### Bibliography

[^1]: info from [s1]

[prs]: [Beginner Donut Blender Tutorials, Blender Guru 2021 - part 9](https://www.youtube.com/watch?v=4WAxMI1QJMQ)
[s1]: [Weight Painting Introduction - Blender 3.3 Manual](https://docs.blender.org/manual/en/latest/sculpt_paint/weight_paint/introduction.html)