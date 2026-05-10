# 0001 — Coordinate system and parcel addressing

**Status:** locked
**Date:** 2026-05-10

## Decision

The world coordinate system for themetaverse.space is locked at protocol version 0:

1. **Origin:** the Black Sun sits at world coordinate (0, 0, 0).
2. **The Street axis:** the Street runs along the Z-axis. Positive Z is north. Negative Z is south.
3. **Up:** the Y-axis is up. Right-handed coordinates, matching A-Frame and Three.js defaults.
4. **Width:** the Street is 100 metres wide, centred on the Z-axis. Positive X is east; negative X is west.
5. **Units:** world units are metres. One A-Frame unit equals one metre. Avatar height is approximately 1.7m.
6. **Parcel addressing:** parcels are integers. A parcel address is a tuple `(side, index)` where `side` is `+x` or `-x` and `index` is a signed integer along Z. Parcel `(+x, 0)` is the first east-side parcel at the origin. Parcel `(+x, 1)` is the next parcel north on the east side.
7. **Parcel size:** each parcel is 25m wide (X) by 50m deep (Z). Buildings can occupy multiple parcels but the underlying grid is fixed.
8. **Finite world at protocol version 0:** no curvature. The Street extends along Z but does not loop. Avatar positions are 64-bit floats (sub-millimetre precision over launch-relevant lengths).
9. **Time:** it is always night. Skybox is pure black. The only light comes from emissive materials.

## Why these choices

- Z as the Street axis matches "walking forward along the Street" being +Z movement.
- 100m width is from the novel directly.
- 25m parcel width fits four parcels into the 100m Street width with room for the central monorail track in a future version.
- Integer parcel addressing keeps the protocol simple — no floats in addresses, no string keys, no UUIDs.
- Right-handed Y-up matches every browser 3D framework's default. No conversion math.
- Black skybox removes global illumination as a rendering concern entirely.

## What this forecloses

- Circular planet at protocol version 0. Curvature requires a protocol bump.
- Variable parcel sizes. All parcels are 25×50.
- Z-up coordinate systems. We are not those frameworks.
- Centring the world on anything other than the Black Sun.
