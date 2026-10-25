# Limitations and Verification Boundaries

## Scope

The project is limited to selected rotational part families for 2-axis turning. It is not a universal drawing-to-NC system, a general AI manufacturing planner, or a replacement for a qualified CAM programmer.

Changing to milling, turn-mill, freeform surfaces, assemblies, or arbitrary drawings would require new geometry rules, templates, contracts, and validation.

## CAM and Machine Safety

The current project record does **not** establish:

- independent collision or gouge checking;
- fixture, chuck, tool-holder, or machine-envelope validation;
- controller-specific semantic validation for every NC command;
- physical cutting, dimensional measurement, surface-finish measurement, or cycle-time acceptance.

NC text scans can catch selected structural problems. They cannot prove that a program is safe to run.

## Where the Toolpaths Come From

These are not hand-written G-code blocks. The toolpaths are computed by the Mastercam kernel and the NC output is produced by Mastercam post processors. Toolpath planning, feed computation, and postprocessing therefore come from a commercial CAM system that has long been used in production environments, not from motion-planning code written for this project.

The author's personal assessment of usability is reasonably high on that basis. That is an assessment of the **source**, not a validation of the **result**: no run on a real machine has been performed, so the output remains unverified until an operator confirms it independently.

## SolidWorks and STEP

Automatic model generation is a generation step, not final engineering acceptance. A SolidWorks document still needs manual inspection for:

- sketch constraint status;
- arc and chamfer direction;
- feature validity;
- model dimensions and feature intent.

STEP parsing is restricted to supported rotational geometry. Cosmetic threads or geometry that is not represented in the STEP file cannot be recovered reliably from the file alone.

## Drawings

The drawing route is useful for producing a checked draft, but dense dimensions and multi-layer bores still need visual review. A generated PDF or DXF is not automatically a released manufacturing drawing.

Third-party drawing components can also impose their own geometry and annotation limitations. They are not a substitute for a drawing standard review.

## Test Numbers

The public README records the final local regression number only as historical evidence for the frozen phase:

```text
924 passed, 9 skipped, 1 deselected, 23 subtests passed
```

This number is version- and environment-specific. The public repository does not contain the source tree required to reproduce it, so it should not be interpreted as a badge for this documentation repository.

## Future Work

Before restarting development, the project should define:

1. one supported part family and a small acceptance set;
2. one known Mastercam machine/post setup;
3. a repeatable simulation procedure;
4. a controlled physical verification plan;
5. a publication and license review for any source code or third-party component.

