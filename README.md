# random-points-in-disk

How many random points does it take before a disk *looks* like a disk?

[**View the live visualizer**](https://concept-collection.github.io/random-points-in-disk/)

Draw *N* points uniformly at random from a disk, bin them into a grid of voxels, and
compare the resulting density map against the exact one. Each voxel's count is
essentially Poisson with mean μ = points per voxel, so its relative noise is 1/√μ —
which depends only on how many points land in a voxel, not on the size of the disk or
the resolution per se. The app plots three panels side by side:

- **Ideal** — exact density, each voxel shaded by the fraction of it inside the disk
- **Sampled** — counts from *N* random points, on the same color scale
- **Noise** — the error in units of its expected standard deviation, (count − ideal)/√ideal

Sliding *N* and the resolution shows the tradeoff directly: quadrupling the resolution
quadruples the number of voxels, so it takes 4× the points to hold the same noise level.
The stats row reports the measured coefficient of variation next to the 1/√μ prediction,
and how many points a target noise level would require.

Statistics are computed only over voxels lying *entirely* inside the disk; boundary
voxels have a smaller expected count and would otherwise inflate the measured spread.

## Motivation

This is the discretization question behind isochromat-based MRI simulation: a voxel's
signal is a sum over the isochromats that landed in it, so randomly placed isochromats
inject noise of order 1/√μ on top of the physics being modeled.

## Running locally

No build step — it is a single static `index.html`. Open it directly, or serve the
directory:

```bash
python3 -m http.server 8000
```
