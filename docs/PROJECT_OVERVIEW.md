# Project Overview

## Identity

`new-sw-mc` is a personal engineering prototype for a narrow CAD/CAM workflow:

```text
structured turning parameters
→ profile and process data
→ semantic DXF
→ isolated Mastercam case copy
→ operation binding and regeneration
→ per-operation NC output
```

The target is a limited family of stepped shafts, bushings, stepped bores, grooves, threads, chamfers, and two-setup turning cases. The project does not claim arbitrary drawing recognition or general-purpose AI process planning.

## Why This Shape

The project deliberately keeps design geometry, machining intent, and CAM execution as separate layers:

- parameters are easier to inspect than hidden mouse actions;
- semantic DXF layers make chain binding explicit;
- `process.json` records why an operation exists;
- an isolated case copy protects the manually tuned Mastercam template;
- per-operation output makes missing or stale NC files easier to detect.

This is a student-scale attempt to connect mechanical engineering knowledge with software automation. It is useful as a learning and portfolio record even where industrial validation is still missing.

## Phase Closeout

The current phase was frozen on **October 25, 2026** and paused until **March–April 2027**. The pause is a schedule and scope decision, not a claim that every technical issue has been solved.

The local record contains evidence for:

- parameter-to-profile and process-package generation;
- semantic DXF layers for setup-one and setup-two turning;
- case-copy Mastercam handoff;
- selected operation binding and per-operation NC generation;
- structured input, STEP parsing, thread, groove, edge-break, and drawing checks.

The strongest public statement is therefore:

> A bounded SW-to-Mastercam turning workflow was built and tested locally for selected cases; the project is not yet a production-safe machining system.

## Evidence Rules

When describing this project, keep these evidence levels separate:

| Evidence | What it proves |
| --- | --- |
| JSON/package test | Input validation and offline artifact generation |
| DXF inspection | Profile geometry, layer names, and chain structure |
| Mastercam case copy | Template intake and operation-level interaction |
| NC text scan | File structure and selected token checks |
| Mastercam simulation | Toolpath behavior within the simulated setup |
| Physical cut and measurement | Real machine, tooling, material, and dimensional evidence |

The public record currently includes the first four levels for selected cases. It does not claim the last two.

