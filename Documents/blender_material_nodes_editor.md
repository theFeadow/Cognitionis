---
id: D#yb497j
date: 07/10/2022
type: article
status: digital
aliases: [D#yb497j]
tags:
  - Blender
---

# Texturing using the Material Nodes Editor in Blender

The Node Editor (found in the 'Shading' tab) is an excellent way to add texture and colour maps to objects in Blender.

The idea is to use 'nodes' to combine and manipulate different "data streams" to create textures and colours that will then be fed to the "object's surface".

Here's how it looks when an object is simply assigned a colour and a roughness from the 'Material Properties' menu.

![[image-20221007170125760.png]]

Notice the coloured dots on the left, each of these is ready to receive an "incoming data link" that can override its value. For now, we focus our attention on the 'Base Color' box at the top and how it controls the colour of our object.. Here's how the object looks like:

![[image-20221007170516612.png]]

Note that the "icing of the donut" is selected and thus actions in the node editor will reflect on the icing and not the body of the donut.

---

Let's now play around with the body of the donut, we hide the icing by selecting it and tapping 'H' and then select the donut's body so we can begin working on it.

![[image-20221007173012828.png]]

Since no work has been on the donut body's material, the Node Editor will appear empty. Let's use the 'Material Properties' menu (on the right) to quickly assign some base colour to the donut to see if it affects the Node Editor. The changes instantly appear in the Node Editor:

![[image-20221007173109388.png]]

Note that assigning a base colour could also have been done through the Node Editor itself.

Now let's see if we can add a block that controls the 'Base Color' box shown above by feeding a link to its input. For example, let's use a 'Varonoi Texture' block and use it's colour output as an input to our object's 'Base Color'.

![[image-20221007173151426.png]]

![[image-20221007173344214.png]]

Nice! The "size of the coloured spots" can be controlled through the "Scale" box. This is the case for all nodes: tweakable values allow non-destructive manipulation of the texture. See 'Procedural Texturing'.

>One can also connect the 'Distance' box in the Voronoi Texture block to the 'Base Color' of the 'Principled BSDF' box, it would affect the donut in some way, because in THIS case, a compatible data stream is being input to the 'Base Color'. However, it doesn't make much sense to do things like this. The point is, you can do that if you - for some reason - want to.

---

A great texture block that is very commonly used is the 'Noise Texture' block. One can use it to generate a noise map that can in turn be used to generate a "noisy" or "textured" colour map using the 'ColorRamp' block, whose output is then finally fed to 'Base Color'.

![[image-20221007180134364.png]]

>Pro tip: use the 'Node Wrangler' add-on to view the output of each block independantly.

That's cool. But notice how there's some sort of stretching in the side of the donut. The "noise patches" are a bit.. horizontal. That stretching happens because of the technique used to map a 2D texture to a 3D object. But what if we didn't want that? What can we do? Well, we can use a different "2D-to-3D" mapping technique.

We can add another block called a 'Texture Coordinate' to enforce a certain "mapping technique":

![[image-20221007181236816.png]]

The "horizontal stretching" is now gone!

---

Now texturing is not only about colour maps, real donuts have "bumps" and "grooves" protruding from their surface. To accomplish a similar effect, we can make the 'Noise Texture' node drive the 'Normal' property in 'Principles BSDF' node by using a 'Bump' node between them, which converts the texture output to an input that the vector input can read.

![[image-20221007182236584.png]]

Now our donut looks like this:

![[image-20221007182311175.png]]

..notice how the "surface roughness" is clearly "painted" on the donut. And I say PAINTED because this is what is really happening. The 'Normal' attribute didn't add geometry to the donut that represents the "bumps". Instead, the presence of a rough surface is faked by "painting" on the donut's body!

---

#### Bibliography

[prs]: [Beginner Donut Blender Tutorials, Blender Guru 2021 - part 7](https://www.youtube.com/watch?v=CmrAv8TSAao)