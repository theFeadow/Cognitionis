---
id: D#d2d1rz
date: 06/10/2022
type: article
status: digital
aliases: [D#d2d1rz]
tags:
  - Blender
---

# Basics of Rendering in Blender

In Blender, there are different "views" where things are "rendered".

There is, of course, the "final output render" (F12) that provides a final image or animation.

However, there is also the rendering that happens in real-time in the viewport that allows the user to view and manipulate their objects and have these manipulations be immediately reflected on the object in the viewport.

Naturally, the "final output render" should in general be more "precise"/"detailed" than the one in the viewport. At the end of the day, the real-time rendering in the viewport is only for the user to know how their object(s) and their setup will more or less look like when properly rendered.

Having said that, there are 2 main **render engines** that come by default with Blender, these are:

- Eevee
- Cycles

Each has its advantages and disadvantages. And each of them can be used for **both** viewport and final rendering. In what follows, the performance and action of these 2 rendering engines will be briefly discussed.

---

#### Eevee

Eevee renders by basically faking. It doesn't do any real ray-tracing or such; it has other ways of processing the scene to produce something that is more than decent for a lot of purposes and use cases. However, Eevee renders will lack realism, unless specifically configured with complex settings to do what it needs to produce something that more resembles a truly ray-traced scene (see [prs]). Even then, Eevee will still fall short of accomplishing the realism attained by other render engines.

Eevee is great for doing graphic designs, cartoon-ish renders, or any scene that doesn't require the high levels of realism attained by true ray-tracing.

Finally, the biggest advantage of Eevee is that it is **truly** a real-time renderer. Which means that Eevee allows the user to manipulate the viewport in 'Rendered' mode and work on the scene while looking at exactly how the scene will look like after rendering without any delay or lag.

---

#### Cycles

Cycles performs true ray-tracing during rendering.

While Eevee requires special setup to make renders look somewhat realistic, Cycles outputs realistic renders by default.

On the other hand, Cycles is computationally intensive and does not - by default - work as a real-time renderer like Eevee. Final rendering using Cycles takes a lot longer than Eevee, and working in 'Rendered' mode in the viewport with Cycles requires the view to re-render every time the camera angle is changed!

Cycles makes use of a metric called 'Samples (per unit pixel)' in order to know the sufficient resolution quality to which to render the objects in a scene.


![[image-20221006134845168.png]]


As seen in the image, the number of 'Samples' can be set separately for the viewport and the final rendered output. If Cycles is used for viewport rendering, a few changes to the above configuration can help achieve a better workflow, for instance:

- It is wise to reduce the maximum number of samples in viewport rendering to something like 128, to allow for a faster workflow with less lag, since full-resolution is not typically needed during modelling and designing.
- Turning on 'Denoise' in viewport rendering is also a great idea to get rid of the "pixelations".

>Remember to set the 'Device' to the GPU and not leave it as the CPU!!

---

#### Pseudo-Eevee

It would be great if one can work in the viewport using Eevee and render using Cycles, without continuously switching between the 2 configurations. Well, that can be - in a way - accomplished using the 'Material Preview' mode!

![[image-20221006142932442.png]]

By setting the mode to 'Material Preview' and turning on the 'Scene Lights' and 'Scene World' options, one can navigate the viewport seamleslly as if in Eevee, even if the render engine is set to Cycles!

![[image-20221006143309181.png]]

![[image-20221006143320238.png]]

The 2 images above are not copies of the same view! The upper one is taken from the 'Material Preview' viewport using Cycles, and the lower one is taken from the 'Rendered' viewport using Eevee! As one can see, they are pretty much identical.

Which means, one can set the render engine to Cycles and switch to 'Material Preview' mode in order to work in the viewport as if in Eevee, sacrificing realism during editing in order to benefit from the fluidity that Eevee provides!

---

#### Bibliography

[prs]: [Beginner Donut Blender Tutorials, Blender Guru 2021 - part 6](https://www.youtube.com/watch?v=_WRUW_fs1g8)