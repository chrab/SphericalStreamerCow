# The Spherical Streamer Cow Model

## Introduction

The Spherical Streamer Cow model is a very simplistic toy model with the main aim to simulate the C/O ratio evolution of a protoplanetary disks, as function of time. The key feature is that the impact of streamers, which are stochastic events that can add material with a certain C/O ratio to the disk, hence changing the mass and overall C/O ratio of the disk. In the current state we do not aim to include proper physics, it should be just a toy model.

## Model Description

The model consists of a disk and should also simulate streamer (mass infall)
events. In the following we describe the simple disk evolution without the impact of streamers. After that we describe how streamers can be includes, and alter the disk mass and C/O ratio.

### Disk evolution

Description of the disk evolution without the impact of streamers:

- We start with a disk of mass $M_{disk}$ and a C/O ratio of $C/O_{disk}$.
- The disk can live for 2 Myr and has an initial mass of $M_{disk,0}$, with a typical value of 0.1 $M_{\odot}$.
- The mass of the disk decreases linearly with time so that after 2 Myr the disk is completely gone. This should be done by a constant mass loss rate $\dot{M}_{disk} = -\frac{M_{disk}}{2 Myr}$.
- Besides the mass loss also the C/O ratio of the disk changes with time. We start with an initial C/O ratio of $C/O_{disk,0}$, with a typical value of 0.5. We assume that the C/O ratio increases linearly with time. By the end of the disk lifetime, the C/O ratio has increased to $C/O_{disk,final}$, with a typical value of 1.5. This should be done by a constant C/O ratio increase rate $\dot{C/O}_{disk} = \frac{C/O_{disk,final} - C/O_{disk,0}}{2 Myr}$.

### Streamer events

- the events happen stochastically, where the probability of a streamer event decreases with time (quadratically by default, but the user can choose between linear, quadratic, and exponential decay), and should be 0 at the end of the disk lifetime or simulation time (2 Myr).

- a streamer has the following properties:
  - mass $M_{streamer}$; drawn log-uniformly from the range $10^{-9} - 0.1\,M_{\odot}$.
  - C/O ratio $C/O_{streamer}$, is fixed to a value of 0.4.
- The number of streamer events during the first 100 000 years, can be provided by the user, this number should decrease with time, so that at 2 Myr, no streamer envents happen any more.
- During a streamer event the total mass of a streamer is added to the disk gradually over the accretion duration (i.e. at each timestep, a fraction of the total streamer mass is added and the disk C/O is updated via complete mixing). This means two or more overlapping streamer events are handled naturally step by step.
- The accretion duration scales log-linearly with streamer mass: 1000 yr for $10^{-9}\,M_{\odot}$ and 10000 yr for $0.1\,M_{\odot}$.

## Numerical parameters

- Simulation timestep: 1000 yr.
- Brightness–C/O mapping: the spherical cow image is shown at full brightness when C/O = C/O_disk,0 (0.5) and at 20% brightness when C/O = C/O_disk,final (1.5). Intermediate values are interpolated linearly in brightness.

- The model should be implemented in Python, within a Jupyter notebook.
- There should be a way so that the user can easily input/adapt the parameters of the model.
- Once the user has set the parameters, the simulation can be started by hitting a "Run" button.
- After the model is run the notebook should show the time evolution of the disk mass and the C/O ratio of the disk, as function of time. In to plots, possibly as an animation.
- A third plot should show the spherical cow image. Whenever a streamer event happens, draw a filled circle (random position in the image) with a certain size (depending on the mass of the streamer) and a random color. After the streamer event happened, the circle should be removed. So that one can also see if two streamers are overlapping.
- If possible the color or brightness of the background spherical cow image should change with the C/O ratio of the disk, where higer C/O means a darker image.
