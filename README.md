# Black-hole lensing: Newtonian and GR-inspired ray models

This university notebook explores how a bundle of initially parallel light rays
can be visualised near a non-rotating black hole. It compares a Newtonian
corpuscular approximation with a deliberately stronger, GR-inspired bending
rule in both a Pygame animation and a static Matplotlib plot.

> **Scientific scope:** this is a qualitative teaching model, not a
> Schwarzschild null-geodesic solver. It cannot be used to calculate physical
> deflection angles, images, photon spheres, or observable black-hole parameters.

## The problem

Newtonian mechanics can be used to sketch a particle-like path for light, but it
does not describe relativistic lensing around a compact object. The project asks
whether a small interactive simulation can make that difference visible while
also showing which rays escape and which cross a model event horizon.

## The approach

The notebook uses scaled units with `G = c = M = 1` and a Schwarzschild radius
of `r_s = 2M`. Nine rays begin at `x = -30` with impact parameters from `-6` to
`6`. Their directions are advanced under an inverse-square acceleration proxy;
the GR-inspired panel multiplies that acceleration by `1.8` to produce stronger
bending.

The implementation adds four practical features to the initial AI-generated
sketch:

- ray capture when `r <= r_s`;
- a smaller integration step near the event horizon;
- side-by-side Newtonian and GR-inspired views;
- limits on ray count, stored path length, and rendered points.

The notebook ends with a separate Matplotlib trace of the same two models. That
static figure is the clearest result currently stored in the repository and is
rendered directly when GitHub displays the notebook.

## What I found

The GR-inspired multiplier produces visibly stronger curvature than the
Newtonian proxy. Rays with small impact parameters are captured, while more
distant rays are deflected and continue out of the plotting region. The exercise
therefore succeeds as a comparison of two *assumed numerical rules*.

It does not demonstrate a measured prediction of general relativity. The `1.8`
factor is chosen for visual contrast, the update is a simple time-step scheme,
and the accretion-disc circle is only a reference marker. A physically useful
next version would integrate null geodesics in Schwarzschild coordinates and
compare numerical deflection with the weak-field result.

## Current status

This is an unfinished formative project. The committed Pygame cells contain two
known logic problems:

- `Ray.update()` advances position twice during one update;
- the first panel-click branch resets both bundles, making the later click-to-add
  branch unreachable.

The notebook also repeats some setup code and has no automated tests. These
issues do not erase the modelling idea or the embedded static comparison, but
they mean the interactive animation should be treated as a draft until the event
loop and integrator are cleaned up.

## Run the notebook

Create an environment and install the notebook dependencies:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install jupyter matplotlib numpy pygame
jupyter notebook black_hole_lensing.ipynb
```

On macOS or Linux, activate the environment with
`source .venv/bin/activate`. Run the cells in order. The Pygame cell keeps the
notebook busy until its window is closed.

## AI-assisted development

The notebook records the prompts used to create the first model and the later
requests for animation, controls, comments, and performance safeguards. AI was
useful for producing a starting structure, but the remaining duplicated logic is
also a good example of why generated scientific code needs manual review before
its output is interpreted.
