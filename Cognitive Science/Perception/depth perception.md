#cogsci126 

Our [[perception]] of *depth* largely comes from adjusting based on the size of objects in our perceived image. This is known as **discounting the distance**.
- **Size constancy**: the image of an object on our retina gets smaller the farther away the object is. Given our perceived distance to that object $x$, we can recover the perceived size $\alpha$ as
$$\alpha \propto x \cdot \text{size on retina}$$
>[!info] Emmert's Law
>Emmert's Law observes an illusion which demonstrates the brain's ability to discount the distance. It states that the perceived size of an afterimage is directly proportional to the perceived distance to the surface which you are viewing it on. This means that transferring an afterimage to a farther distance will cause you to perceive a larger image.

## pictorial depth cues
Pictorial cues are the features of 2D, static images that support depth perception. These are characteristics that can be manipulated by artists, for example, to create illusions of depth.
- **Occlusion**: T-junctions indicate which objects are in front of which others, but does not provide information on *how far* in front the object is, or any distance estimation
- **Linear perspective**: geometry dictates that parallel lines will appear to converge in the distance. This provides metric information about depth. 
	- Linear perspective is much easier to estimate with objects that are attached to a surface (i.e. the ground). Distance estimations often become ambiguous with hovering objects.

>[!tip] Ray Tracing
>Ray tracing is an optical technique for generating digital images which employs properties of **linear perspective**. Notice how by drawing a straight line between the observation viewpoint and any point on the object, the point's position on the image is where it intersects with the image plane.
>![img/ray-tracing.jpeg](img/ray-tracing.jpeg)

- **Known size**: uses prior object knowledge as a reference point to estimate the distance to the object or make inferences about other objects in the image.
	- This cue is often dominated by others.
- **Height in field**: the horizon line is about at eye level. Objects closer to the horizon are perceived to be further away.
- **Texture gradients**: if we assume that the texture or pattern of a specific surface remains uniform, then any perceived changes in size of the texture or pattern can be attributed to depth.
- **Atmospheric perspective**: distant surfaces have less contrast because an intervening atmosphere superimposes a haze
[[perception#light & shadow|Light & shadow]] also provide helpful pictorial clues. In general, pictorial cues are exceedingly strong, and dominate [[motion]] and binocular cues.

The interpretation that we choose to describe our perceived image is the one that agrees with the most cues.

---
## binocular depth cues
- **Accomodation**: objects closer to us tend to be more in focus. Your eye muscles need to work harder to focus on farther objects. That strain is perceived and taken into account by our visual system.
- **Convergence**: we can derive the distance to an object based on the angle between the direction our eyes are pointing to. For objects extremely close to us, we become cross-eyed.

#### disparity indicates depth
**Stereopsis** is the actual component of depth perception that arises from computing binocular disparity. The premise is that the disparity between the images received by the left and right eye gives depth cues.

**Binocular disparity** is the difference in perceived location of an object between your left and right eye, and is dictated by the angular difference between the projections of your left and right eye ($\theta_L$ and $\theta_R$ respectively).
	- The *horopter* is the locus of all points in the visual field for which there is no binocular disparity. The **fixation point** (where your fovea is pointed at) always lies on the horopter.
	- Uncrossed disparity lets us know that the object is further than the fixation point
	- Crossed disparity tells us that an object is closer than the fixation point

>[!info] Binocular cells
>Binocular cells are a type of neuron found in the primary [[visual cortex]]. They assist with stereopsis via their [[receptive fields]] which are sensitive to different ranges of separation between the receptive field centers relative to the fovea of each eye. This makes them *selective* for disparity, where each cell has a preferred disparity.

The final major indicator of depth is [[motion]], where we begin to integrate cues of a continuous, 4D world.