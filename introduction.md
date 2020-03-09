---
layout: page
title: Introduction
permalink: /Introduction/
---
# The Plenoptic Function
Light fields use the *plenoptic function* to describe a scene. The plenoptic function is a 7-D function that describes light rays from all angles, at all wavelengths, at all positions in space-time:

$$ \begin{equation} \label{eq:plen} P(x,y,z,\theta,\phi,\lambda,\tau) \end{equation} $$

Where $$ x,y,z $$ is the position of the viewer in 3-D space, $$ \theta, \phi $$ are the azimuthal and polar angles of the incoming light ray, respectively, $$ \lambda $$ is the wavelength of the light, and $$ \tau $$ is time. The collection of all light rays in a scene is referred to as a *light field*. The plenoptic function can be reduced to four dimensions by using the *two-plane parameterization*:

<p align="center">
  <img width="300" height="316" src="../images/stuv.png">
</p>

In this perspective, light rays are modeled as their point of intersection of two planes. $$(u,v)$$ denote the coordinates of intersection on the green plane, and $$(s,t)$$ are the coordinates of intersection on the red plane. The distance between the two planes, $$ d $$, is dependent on the camera model used to capture the light field. Most literature refers to light fields by this parameterization, $$l(s,t,u,v)$$.

# Camera Models
The simplest way to imagine capturing a light field is with a camera array. Using the two-plane parameterization, each coordinate on the $$(s,t)$$ plane is a different camera aligned on a grid, and $$(u,v)$$ is the image captured by each camera. Then, $$d$$ is the focal length of the camera lenses. If each camera were to take a photo at the exact same time, then each image will be of the same scene from slightly different viewpoints. The collection of all of these images is referred to as a *light field image*. The individual images are referred to as *sub-aperture views*.

It is also possible to use a single camera to capture a light field image. In this case, a micro-lenslet array is placed between the camera's lens and its image sensor. $$d$$ is the distance between the lens and the micro-lenslet array.

# Epi-polar Plane Images
To extract depth from a light field image, you need to look at how a row or column of pixels changes across a row or column of sub-aperture views.

<p align="center">
  <img width="300" height="294" src="../images/EPISlice.png">
</p>

Here's an example of a light field image. If you select the row of pixels in red across the row of sub-aperture views and stack them on top of each other, you arrive at a new 2-D image called an *epi-polar plane image* (EPI):

<p align="center">
  <img width="328" height="300" src="../images/TarotSmallEPI.png">
</p>

As you can see, an EPI shows the same row (column) of pixels from a row (column) of sub-aperture views. The position of the pixels are shifted slightly across each view, forming lines of different slopes. The slopes of these lines indicate the depth of the object that the pixels belong to. These lines are governed by the equations

$$
\begin{equation}
	(\frac{d}{P_{z}} - 1)s + u = \frac{P_{x}d}{P_{z}}
	\label{eq:suEPI}
\end{equation}
$$

$$
\begin{equation}
	(\frac{d}{P_{z}} - 1)t + v = \frac{P_{y}d}{P_{z}}
	\label{eq:tvEPI}
\end{equation}
$$

where $$P = (P_{x},P_{y},P_{z})$$ is the position of the object in 3-D space, and $$d$$ is the distance between the $$(s,t)$$ and $$(u,v)$$ planes. The intersection of $$\ref{eq:suEPI}$$ and $$\ref{eq:tvEPI}$$ in 4-D space gives the depth of the object.

It's also interesting to look at the frequency domain of an EPI:

{% include SurfacePlot.html %}

Can you see the lines crossing through the origin? Each of these represents a different depth found in the EPI. These lines are governed by the equations

$$
\begin{equation}
	\Omega_{s} + (1 - \frac{d}{P_{z}}) \Omega_{u} = 0
	\label{eq:suFreq}
\end{equation}
$$

$$
\begin{equation}
	\Omega_{t} + (1 - \frac{d}{P_{z}}) \Omega_{v} = 0
	\label{eq:tvFreq}
\end{equation}
$$

where $$(\Omega_{s},\Omega_{t},\Omega_{u},\Omega_{v})$$ are the frequency components for $$(s,t,u,v)$$. The above figure only shows the 2-D frequency domain of an EPI in $$(s,u)$$, denoted $$l(s,t^{*},u,v^{*})$$. The true depth of an object is again, the intersection of these two equations in 4-D frequency space. By examining the frequency domain of an EPI, we can build band-pass filters that can re-focus the light field onto an object based on its depth:

<p align="center">
  <img width="300" height="300" src="../images/Tarot_Center.png">
  <img width="300" height="300" src="../images/Tarot_Focused.png">
</p>








