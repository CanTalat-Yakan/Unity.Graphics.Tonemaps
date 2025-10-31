# Unity Essentials

This module is part of the Unity Essentials ecosystem and follows the same lightweight, editor-first approach.
Unity Essentials is a lightweight, modular set of editor utilities and helpers that streamline Unity development. It focuses on clean, dependency-free tools that work well together.

All utilities are under the `UnityEssentials` namespace.

```csharp
using UnityEssentials;
```

## Installation

Install the Unity Essentials entry package via Unity's Package Manager, then install modules from the Tools menu.

- Add the entry package (via Git URL)
    - Window → Package Manager
    - "+" → "Add package from git URL…"
    - Paste: `https://github.com/CanTalat-Yakan/UnityEssentials.git`

- Install or update Unity Essentials packages
    - Tools → Install & Update UnityEssentials
    - Install all or select individual modules; run again anytime to update

---

# Tonemaps

> Quick overview: A small pack of AgX-inspired tonemapping LUTs (EXR) for HDRP. Drop one into a Color Lookup override to get consistent filmic contrast variants: Very Low → Very High, Base, and Greyscale.

This package ships ready-to-use EXR LUTs that implement AgX-like looks at different contrast levels. Use them via the Volume "Color Lookup" override in HDRP to achieve a modern, filmic display transform without custom shaders.

![screenshot](Documentation/Screenshot.png)

## Features
- Curated looks
  - Very Low, Low, Medium High, High, Very High contrast variants
  - Base Contrast and a Greyscale variant
- High precision
  - Stored as EXR LUTs for stable gradients and highlights
- SRP friendly
  - Works with HDRP through the built-in Color Lookup post-process
- Simple integration
  - No custom render features or shaders; pure Volume overrides

## Requirements
- Unity 6000.0+
- URP or HDRP with the Volume system enabled
- Post-processing active in your camera/pipeline

Recommended
- Use a single tonemapping stage: set the Tonemapping override to None (or disable other transforms) when applying these LUTs to avoid double tonemapping

## Usage

HDRP (Volume)
1) Ensure a Global Volume is present and post-processing is enabled
2) Add the override: Post-process → Color Lookup
3) Assign one of the EXR LUTs from `Resources/AgX Luts/`
4) Adjust Contribution to taste
5) Optional: Add a Tonemapping override and set Mode to None (or Neutral) if you want the LUT to be the primary transform

### Import settings (LUT textures)
- Texture Type: Default
- sRGB (Color Texture): Off (EXR is typically handled as linear by Unity, but confirm in the Inspector)
- Mip Maps: Off
- Wrap Mode: Clamp

If colors look incorrect (crushed or washed-out), verify you are not stacking multiple tonemappers and that the project uses Linear color space.

## Notes and Limitations
- Single tonemapper: Avoid combining these LUTs with ACES/Neutral simultaneously to prevent double tonemapping
- Exposure: Filmic transforms assume a reasonable exposure; adjust Exposure/Auto Exposure to place midtones appropriately
- Color tweaks: Pair with Color Adjustments (White Balance, Contrast, Saturation) for final taste
- Greyscale look: Use the Greyscale LUT for preview or stylized scenes; it removes chroma after the transform

## Files in This Package
- `Resources/AgX Luts/AgX - Very Low Contrast.exr`
- `Resources/AgX Luts/AgX - Low Contrast.exr`
- `Resources/AgX Luts/AgX - Base Contrast.exr`
- `Resources/AgX Luts/AgX - Medium High Contrast.exr`
- `Resources/AgX Luts/AgX - High Contrast.exr`
- `Resources/AgX Luts/AgX - Very High Contrast.exr`
- `Resources/AgX Luts/AgX - Greyscale.exr`
- `Resources/AgX Luts/Look/` (reserved for custom looks)
- `package.json` – Package manifest metadata

## Tags
unity, hdrp, urp, tonemap, tonemapping, agx, lut, color grading, filmic, volume, post-processing
