# MechForge

A browser-based parametric 3D engineering configurator for building valid mechanical
product variants from parameters, rules, and reusable components.

MechForge connects product parameters directly to a live 3D assembly, an engineering
rule set, a generated ordering code, and a resolved bill of materials:

```
Parameters -> Rules -> Geometry -> Assembly -> BOM
```

> **Closed source.** This repository is a public showcase. The source code is
> maintained in a private repository and is not published here.
> All rights reserved - see [LICENSE](LICENSE).

## Why

Industrial products routinely ship in hundreds or thousands of variants, governed by
part-number rules, CAD family tables, ERP data, and engineering knowledge that lives
in spreadsheets. Traditional web configurators reduce that to forms and static
images, while CAD systems represent it accurately but are too heavy for customers,
sales, or lightweight engineering workflows.

MechForge sits between the two: configuration logic and engineering rules are the
product, and Three.js is only the visualization layer.

## What it does

| Capability | Description |
| --- | --- |
| Product configuration | Four reference product families driven by declarative parameter definitions (enum, number, boolean) |
| Configuration engine | Shared normalization, defaulting, and validation across all product families |
| Live 3D assembly | Procedural three.js assemblies that rebuild as parameters change |
| Ordering codes | Generation and decoding of configurable part numbers |
| Engineering BOM | Resolved bill of materials with CSV export, traceable to parameters and components |
| Local-first persistence | Saved configurations, JSON project export/import, shareable configuration URLs |
| Workbench tooling | Fit-to-view, orbit camera presets, per-component visibility, section views, screenshot export |
| Verification | Unit and end-to-end test coverage over the engine, geometry, and workbench |

## Screenshots

_Coming soon - viewport captures of the workbench and each reference product family._

## Reference product families

Development is validated against several mechanically distinct families, which keeps
the engine reusable rather than hard-coded to one product:

- **Pneumatic cylinder** - bore, stroke, mounting, material, sensor options
- **Gearbox** - ratio, motor interface, shaft options, mounting positions
- **Valve manifold** - modular assemblies, repeated stations, accessories
- **Machine frame** - parametric profiles, dimensions, mounting hardware

## Architecture

Product logic is deliberately kept out of the UI and out of the renderer.

```
┌──────────────────────────────────────┐
│               Web UI                 │
│         React + TypeScript           │
└──────────────────┬───────────────────┘
                   │
          ┌────────▼────────┐
          │ Product Schema  │
          │ + UI Generator  │
          └────────┬────────┘
                   │
          ┌────────▼────────┐
          │ Configuration   │
          │ Engine          │
          │                 │
          │ Rules           │
          │ Dependencies    │
          │ Validation      │
          │ Derived Values  │
          └────────┬────────┘
                   │
        ┌──────────▼──────────┐
        │ Product Model       │
        │                     │
        │ Parameters          │
        │ Components          │
        │ Assembly            │
        │ Metadata            │
        └───────┬───────┬─────┘
                │       │
        ┌───────▼───┐ ┌─▼─────────────┐
        │ Three.js  │ │ Engineering   │
        │ Renderer  │ │ Outputs       │
        │           │ │               │
        │ Geometry  │ │ BOM           │
        │ Assembly  │ │ Part Number   │
        │ Materials │ │ Config Data   │
        └───────────┘ └───────────────┘
```

## Technology stack

| Layer | Technology |
| --- | --- |
| Language | TypeScript |
| Frontend | React |
| 3D | Three.js, React Three Fiber, drei |
| State | Zustand |
| Build | Vite |
| Product definitions | Declarative TypeScript/JSON schemas |
| Validation | Zod |
| Testing | Vitest, Playwright |

## Engineering principles

- **Configuration logic is independent from UI.** Rules are not buried in components.
- **Product data is declarative.** A new product is defined through schemas and data.
- **Geometry is not product logic.** The renderer visualizes the product model; it does not define it.
- **Invalid configurations are impossible or explainable.** The engine prevents invalid selections or states why.
- **Engineering data stays traceable.** Every rendered component maps to parameters, metadata, part number, and BOM entry.

## Roadmap

Delivered:

- **v1.0 - Configuration workbench.** Four reference families, shared validation engine, procedural 3D assemblies, ordering codes, BOM with CSV export, local-first persistence, project export/import, shareable URLs.
- **v1.1 - 3D workbench.** Camera presets and fit-to-view, per-component visibility, section views, screenshot export, end-to-end workbench coverage.

Planned:

- **v0.2 - Rules engine.** Conditional parameters, dependencies, exclusions, derived values, rule testing framework.
- **v0.3 - Parametric geometry.** Parameter-driven dimensions, reusable geometry generators, measurement tools.
- **v0.7 - CAD integration.** STEP import and OpenCascade/WASM geometry.
- **v0.8 - Engineering validation.** Interface compatibility, interference and clearance checks.

## License

Proprietary. All rights reserved. No part of this project may be copied, modified,
distributed, or used without prior written permission. See [LICENSE](LICENSE).

## Contact

Edward Nguyen - edward.nguyen.2854@gmail.com

For a guided demo or access to the source, get in touch.
