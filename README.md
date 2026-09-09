# 3dgs-unreal-example

[![Plugin](https://img.shields.io/badge/Plugin-LCC%20for%20UE-blueviolet?logo=github)](https://github.com/xgrids/LCC-3DGS-Unreal-Plugin)
[![Discord](https://img.shields.io/badge/Discord-Join%20Community-5865F2?logo=discord&logoColor=white)](https://discord.gg/b99H8wjRaH)
[![Forum](https://img.shields.io/badge/Forum-Developer%20Community-orange)](https://developer.xgrids.com/#/forum)
[![Website](https://img.shields.io/badge/Website-xgrids.com-blue)](https://www.xgrids.com/intl/lccUE)
[![UE5](https://img.shields.io/badge/Unreal%20Engine-5.4--5.8-black?logo=unrealengine)](https://www.xgrids.com/intl/lccUE)
[![Platform](https://img.shields.io/badge/Platform-Windows%20|%20Linux-lightgrey)]()

English | [中文](./README_zh.md)

Example project for 3D Gaussian Splatting (3DGS) in Unreal Engine, built on the [LCC-3DGS-Unreal-Plugin](https://github.com/xgrids/LCC-3DGS-Unreal-Plugin).

Split into 13 standalone levels (plus a `LCCWelcome` hub), each demonstrating exactly one thing: loading a 3DGS scene, comparing render modes, clipping, collision, navmesh, water, Sequencer output, GIS, and multi-display. Open the level you care about instead of digging through a pile of blueprints.

https://github.com/xgrids/3dgs-unreal-example/raw/main/Media/Demo.mp4

- Engine: Unreal Engine 5.4 ~ 5.8 (saved with 5.4, opens in newer versions)
- Plugin: LCC4Unreal 3.3.1 or newer (Win64 / Linux)
- Data formats: LCC, LCC2, SOG, SPZ, PLY

> This repo holds the project configuration only. The content pack (`Content/`) and the plugin (`Plugins/`) are downloaded separately to keep clones fast. Steps below.

## Getting Started

### 1. Clone the repo

```bash
git clone git@github.com:xgrids/3dgs-unreal-example.git
cd 3dgs-unreal-example
```

Or over HTTPS:

```bash
git clone https://github.com/xgrids/3dgs-unreal-example.git
```

The clone is small and quick, since it only carries `Config/` and the `.uproject`.

### 2. Download the content pack

Levels, blueprints, and 3DGS sample data (~470 MB) ship as a release asset rather than living in Git history. Grab `Content.zip` from the [Releases](https://github.com/xgrids/3dgs-unreal-example/releases) page and extract it at the repo root so you end up with a `Content/` folder next to the `.uproject`:

```
3dgs-unreal-example/
├── Config/
├── Content/          ← extracted from Content.zip
│   ├── 3DGSData/
│   ├── Global/
│   ├── Maps/
│   └── ...
└── LCCUnrealExampleDemo.uproject
```

Pick the release that matches your clone. Mixing a `Content.zip` from an older release with a newer `Config/` can produce missing asset references.

### 3. Download the LCC4Unreal plugin

The plugin is third-party redistributable content and is not bundled here. Get the installer from the XGRIDS developer portal (the GitHub repo hosts docs only, no binaries):

- Download: https://developer.xgrids.com/#/download?page=LCC_UNREAL_SDK_UE54
- Plugin repo: https://github.com/xgrids/LCC-3DGS-Unreal-Plugin
- User manual: https://docs.xgrids.com/en-us/07-plugin-sdk/01-unreal/v3.3.1/01-introduction.html
- Website: https://www.xgrids.com/intl/lccUE

The plugin comes in Free and Pro tiers. Every level in this project opens on the Free tier: multi-format loading, LoD, depth and DOF, collision, NavMesh, VR, nDisplay, and Cesium are all included. Proxy Mesh relighting, self-shadowing, the ACES / OCIO color pipeline, and unlimited clipping are Pro features. See the [plugin repo](https://github.com/xgrids/LCC-3DGS-Unreal-Plugin) for the full comparison.

One thing to watch: the plugin is built per engine version, so the package you download has to match the engine you actually run, or the module will fail to load.

| Item | Requirement |
| --- | --- |
| Plugin version | 3.3.1 or newer |
| Engine version | Must match your engine — grab the 5.4 / 5.5 / 5.6 / 5.7 / 5.8 build accordingly |
| Platform | Windows (win) or Linux |

### 4. Install the plugin

Create a `Plugins` folder at the repo root and drop the extracted plugin directory inside:

```
3dgs-unreal-example/
├── Content/
├── Config/
├── Plugins/
│   └── LCC4Unreal-v3.3.1-win-UE5_4/   ← extracted directory goes here (name varies by engine version)
│       ├── Binaries/
│       ├── Content/
│       ├── Resources/
│       ├── Shaders/
│       ├── Source/
│       └── LCC4Unreal.uplugin
└── LCCUnrealExampleDemo.uproject
```

The directory name doesn't have to match exactly. UE only needs to find `LCC4Unreal.uplugin` somewhere under `Plugins/`.

### 5. Open the project

Double-click `LCCUnrealExampleDemo.uproject`. The startup level is `LCCWelcome`, the hub for every example, and you can jump to any feature level from there.

The project file is saved with 5.4. Opening it in 5.5 ~ 5.8 triggers the "newer version" prompt; converting a copy or opening in place both work. Assets upgrade to the current engine version when saved and can no longer be opened in 5.4, so avoid committing upgraded assets if you want to keep 5.4 compatibility.

If you're asked to rebuild modules, choose yes. Binary-only releases usually don't need compilation.

### 6. Packaging (optional)

This is a blueprint-only project with no `Source/` directory. Packaging as-is fails, because LCC4Unreal ships C++ modules and the project itself has to take part in the build. Convert it to a C++ project first:

In the editor pick `Tools` → `New C++ Class` and create any class (an `Actor` with the default name is fine). UE generates the `Source/` directory and target files, then asks you to restart the editor. After that, package normally through `Platforms` → `Windows` → `Package Project`.

Once converted, the project needs Visual Studio installed (with the "Game development with C++" workload on Windows) to compile.

## Controls

In PIE (hit Play), all example levels share these keys:

| Key | Action |
| --- | --- |
| `W` `A` `S` `D` | Move |
| `E` | Interact with hotspots in the scene |
| `Tab` | Toggle the feature panel |
| `N` / `P` | Next / previous example |
| `H` | Back to the `LCCWelcome` hub |
| `F` | Toggle performance stats (FPS) and navmesh visualization |
| `Ctrl` | Toggle mouse mode (camera control / UI clicks) |

The same hint stays pinned to the bottom-left corner in every level.

## Example Levels

All levels live under `Content/Maps/`, from the content pack.

| Level | What it covers |
| --- | --- |
| `LCCWelcome` | Hub, entry point for every example |
| `01_Basics` | Minimal setup: load and display a 3DGS scene |
| `02_Rendering` | Render modes and rendering parameters side by side |
| `03_VisualSettings` | Visual tuning: color, brightness, and other appearance settings |
| `04_SceneEdit` | Scene editing: clipping boxes, transforms, local changes |
| `05_Performance` | Performance settings and the tradeoffs involved |
| `06_LightMode` | Light modes, pairing 3DGS with UE lighting |
| `07_NavMesh` | Building a navmesh over a 3DGS scene and driving an AI character |
| `08_LoadingAnimation` | Transition animation during loading |
| `09_Water` | Blending with the UE Water system (needs Water, WaterExtras) |
| `10_Sequencer` | Sequencer keyframing and Movie Render Pipeline output |
| `11_GIS_Cesium` | Geospatial scene with Cesium for Unreal (see optional dependency below) |
| `11_nDisplay` / `12_nDisplay` | Two nDisplay setups for multi-display / video wall output |

## Plugin Dependencies

These engine plugins are already enabled in the `.uproject`, nothing extra to install:

`ModelingToolsEditorMode`, `Water`, `WaterExtras`, `MovieRenderPipeline`, `MoviePipelineMaskRenderPass`, `nDisplay`

Optional:

- `11_GIS_Cesium` needs [Cesium for Unreal](https://cesium.com/platform/cesium-for-unreal/). It is not enabled in the `.uproject`, so install and enable it before opening that level, otherwise its Cesium actors fail to load. Other levels are unaffected.

## Sample Data

Formats the plugin supports:

| Format | Notes |
| --- | --- |
| `.lcc2` | XGRIDS in-house format, the current primary format. Supports depth, LOD, and octree structure |
| `.lcc` | XGRIDS in-house format, superseded by LCC2 |
| `.sog` | From PlayCanvas. Runs through the LCC2 pipeline, supports depth, no LOD |
| `.spz` | From Niantic Labs, compatible with v2 / v3 / v4. Runs through the LCC2 pipeline, supports depth, no LOD |
| `.ply` | Standard 3DGS point cloud format. Runs through the LCC2 pipeline, supports depth, no LOD |

LCC2 is the only format with LOD, which is why the large-scene streaming examples use it. The content pack carries one sample per format under `Content/3DGSData/`:

| Path | Format |
| --- | --- |
| `lcc2/LCC2.lcc2`, `LCC2_1/LCC2.lcc2` | LCC2 |
| `lcc/meta.lcc` | LCC |
| `Strawberry.sog` | SOG |
| `R12.spz` | SPZ |
| `scene/scene_0.ply` | PLY |

To use your own data, drop the files into `Content/3DGSData/` and repoint the data path on the corresponding actor in the level.

## Troubleshooting

The project reports a missing LCC4Unreal module

Two usual causes. Either `Plugins/` isn't laid out right — confirm the path `Plugins/<plugin dir>/LCC4Unreal.uplugin` exists — or the plugin build doesn't match the engine, for example a 5.4 package on a 5.6 engine. Swap in the matching build from the [download page](https://developer.xgrids.com/#/download?page=LCC_UNREAL_SDK_UE54).

The project opens but assets are missing, or levels aren't there

The content pack isn't extracted, or it landed in the wrong place. `Content/` has to sit next to `LCCUnrealExampleDemo.uproject`, not nested inside another folder.

The scene is empty, no splats visible

First check that the files under `Content/3DGSData/` are complete (large files can be truncated by a dropped connection), then verify the data path on the actor points at the right file.

Packaging fails with a missing target file

This is a blueprint project and needs converting to C++ first. See the packaging step above.

Cesium actors throw errors in a level

See the optional dependency above, Cesium for Unreal has to be installed separately.

The items above are specific to this example project. For plugin usage questions (rendering artifacts, performance tuning, format import) see the official [FAQ](https://docs.xgrids.com/en-us/07-plugin-sdk/01-unreal/v3.3.1/19-faq.html).

## Notes

This repo contains only the example project and its sample data. The LCC4Unreal plugin is developed and distributed by XGRIDS; refer to the official terms for licensing and usage.

- Plugin repo: https://github.com/xgrids/LCC-3DGS-Unreal-Plugin
- User manual: https://docs.xgrids.com/en-us/07-plugin-sdk/01-unreal/v3.3.1/01-introduction.html
- FAQ: https://docs.xgrids.com/en-us/07-plugin-sdk/01-unreal/v3.3.1/19-faq.html
- Developer forum: https://developer.xgrids.com/#/forum
- Discord: https://discord.gg/b99H8wjRaH
- Website: https://www.xgrids.com/intl/lccUE
