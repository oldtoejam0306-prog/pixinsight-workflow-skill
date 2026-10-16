# Anonymous workflow case notes

These notes distill practical lessons from image-processing sessions. They do not identify users, machines, projects, or private conversations. They describe examples, not universal presets or guarantees.

## Observed preferences

- PixInsight (PI) refers to the astronomy image-processing application. Aim to use signal present in the source data and avoid inventing structure.
- When the user authorizes a complete delivery, compare a small set of evidence-based candidates and deliver a usable result with a concise record of changes and remaining limits.
- Common preferences include clear but natural dust and nebula structure, a balanced background, visible stars with color, and soft transitions around bright cores. Apply target-specific color preferences only to that target and only where the source signal supports them.
- Reference images can guide color and tonal relationships, but their pixels must not be inserted into the astronomical image.

## Example lessons

In one narrowband mosaic, the work involved per-panel correction, common-coordinate alignment, channel-by-channel integration, refinement, star separation and recombination, local halo work, color conversion, and export checks. A deconvolution strength that worked in that image is not a default for other data.

In one broadband reflection-nebula image, background candidates were compared over common regions, stronger deconvolution offered no clear benefit, and some stretch candidates increased blotchy color. These observations motivate careful comparisons; they do not establish a generally superior process.

Image dimensions, masks, coordinates, filter assumptions, parameter values, and hardware measurements from any particular session are not transferable presets. A passing run on stacked masters also does not establish that a WBPP workflow has been tested successfully.

## Evidence boundaries

- Distinguish a generated file, an agent's review, and user acceptance in delivery notes.
- Do not claim a workflow was completed when only a plan or tool availability was checked.
- Keep the unmodified inputs and meaningful recovery checkpoints until downstream outputs have been verified.
