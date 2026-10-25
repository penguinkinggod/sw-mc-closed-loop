# SW→MC Lathe Closed Loop | Project Record

**Language / 语言:** [简体中文](README.md) | English

> [Watch the demo on Bilibili](https://www.bilibili.com/video/BV1mSHg6NERB/)
>
> This is a personal learning record developed with AI assistance.
> The author received First Prize in the Jiangsu Provincial Vocational College Skills Competition, “Modern Machining Technology”.
> Contact: [2014170845@qq.com](mailto:2014170845@qq.com)

This project is a CAD/CAM automation prototype for a limited family of stepped shafts and bushings on a 2-axis lathe.

It explores the following pipeline:

```text
Parameter JSON
    ↓
Profile geometry and process plan
    ↓
Semantic DXF + process.json
    ↓
Isolated copy of a Mastercam template
    ↓
Operation filtering, cloning, chain binding, regeneration
    ↓
Per-operation NC files
```

SolidWorks models and STEP files are parallel design-side verification branches. Engineering drawings are generated separately from STEP data. This is not a universal AI system that programs arbitrary drawings; it is a scoped, rule-driven personal engineering prototype.

## What This Repository Contains

This is a **public project-record repository**, separate from the actual development workspace.

- `README.md` / `README.en.md`: project overview
- `docs/PROJECT_OVERVIEW.md`: scope, phase, and evidence boundaries
- `docs/ARCHITECTURE.md`: source-independent architecture notes
- `docs/LIMITATIONS.md`: known limitations and incomplete verification
- `media/`: selected workflow screenshots
- `NOTICE.md`: third-party software, content scope, and responsibility notice

Source code, C++/C# plugins, SolidWorks models, Mastercam master templates, NC/NCI files, commercial software installers, and local runtime folders are **excluded**.

## Current Status

As of **October 25, 2026**, this phase has been closed and paused. A new scope review is planned for **March–April 2027**.

The local project record for this phase includes:

- parameter-driven profile, process data, and semantic DXF generation;
- two-setup turning and stepped-bore handling;
- isolated case copies of the Mastercam template;
- contract-based operation filtering, cloning, and DXF-layer binding;
- per-operation NC generation with input and result records;
- separate checks for structured input, STEP input, threads, grooves, edge breaks, and drawings.

The final local regression record at code freeze was:

```text
924 passed, 9 skipped, 1 deselected, 23 subtests passed
```

This number describes one local test scope. It does not mean every part was accepted on a machine, and it does not mean that an NC file is safe to run without further verification.

## Key Design Ideas

### 1. DXF layers carry machining intent

DXF layers are not only geometry groups. They provide explicit names for Mastercam operation binding, for example:

```text
S1_OD_ROUGH
S1_OD_FINISH_01
S1_ID_FINISH_02
S1_THREAD_EXT_M10
```

Each bound layer is also checked for chain continuity and minimum entity counts. This makes regenerated profiles traceable instead of relying on old interactive selections.

### 2. Master template and case copy are separate

The Mastercam template contains a manually adjusted set of turning operations. A case-specific copy is created before filtering, cloning, chain binding, or postprocessing. This prevents one case from silently changing the source template.

### 3. Shared parameters do not remove the need for validation

The model, DXF, process JSON, and drawing are driven by the same input parameters or derived data, but they serve different purposes:

- SolidWorks owns the design-side model;
- DXF carries turning profiles and semantic chains;
- `process.json` records process intent;
- drawings read geometry from STEP and add annotations.

Matching parameters are therefore not a substitute for checking the model, chains, toolpaths, NC, and drawing separately.

## Evidence Screenshots

### Mastercam semantic layers and operations

![Mastercam semantic layers](media/01-mastercam-layers.png)

### STEP-derived engineering drawing

![Engineering drawing](media/02-engineering-drawing.png)

These screenshots document workflow and interface state. They are not proof of collision safety, dimensional acceptance, or real machining.

## Current Boundaries

- The scope is a limited family of 2-axis turning parts, not a general CAD/CAM system.
- Mastercam toolpath simulation, independent collision checking, and physical test cutting have not been completed.
- NC files received structural text checks, which cannot guarantee machine safety.
- Automatically generated SolidWorks models still require manual inspection; some cases need further sketch-constraint review.
- Complex stepped-bore drawings and dense annotations still have layout limitations.
- Machine vision, PLC, digital twins, and multi-axis machining are not completed capabilities of this repository.

See [`docs/LIMITATIONS.md`](docs/LIMITATIONS.md) for the full boundary statement.

## Project State

This repository preserves the public explanation of one project phase. Any future development should first define:

1. the supported part family;
2. the available Mastercam simulation and NC verification conditions;
3. a repeatable school or machine-shop validation environment;
4. which materials can be published without exposing commercial software files or licensing risks.

See [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md) for the architecture notes.

## License and Responsibility

This repository does not include the actual source code, commercial software files, or a directly runnable machining package. See [`NOTICE.md`](NOTICE.md) for third-party software and responsibility notes.

