---
id: D#dmh1a0
date: 08/10/2022
type: article
status: digital
aliases: [D#dmh1a0]
tags:
  - Blender
---

# Texture Painting in Blender

Texture painting in Blender allows "painting on" the 3D-object, just as one would do using Photoshop or MS-paint.

Texture painting is normally done through the 'Texture Paint' tab at the top. However, accessing this tab without having "some texture loaded" will show nothing to do:

![[image-20221008150926723.png]]

One way to get around this problem is to create an image texture and assign it to the donut from the node editor:

![[image-20221008151436911.png]]

Now we can actually do something in the 'Texture Paint' tab:

![[image-20221008151848609.png]]

The right-hand-side panel allows painting on top of the 3D-object directly, while the left-hand-side panel allows painting on the UV-projection of the object.

---

**So let's paint!**

Let's create the "white ring" that appears around cooked donuts, can be seen here:

![[image-20221008151711904.png]]
One can simply choose a colour, set brush size using 'F' and brush strength using 'shift-F'.

![[image-20221008155634460.png]]

And we have a painted donut!

---

Notice that we have lost the effect of the "noise texture" in colouring the donut after we got rid of the 'ColorRamp' node. We need a way to "infuse" the painted texture with the noise texture.

And we can accomplish that via a 'MixRGB' node.

We choose the 'Blend Mode' to be 'Overlay' and simply combine the 2 textures.

![[image-20221008160919547.png]]

And we've got ourselves a painted, noisy, textured donut!

![[image-20221008161051428.png]]

---

#### Bibliography

[prs]: [Beginner Donut Blender Tutorials, Blender Guru 2021 - part 7](https://www.youtube.com/watch?v=_LeTDpNrdbg)