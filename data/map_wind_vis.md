# Wind Vector Tiles

This map visualizes wind vectors (U, V). It is **not** intended for direct display — rather, it serves as a data source for flow animations.

## Encoding

The vectorized wind speed (North/East components) is encoded in RGBA as follows:

-   **Red ( R )** channel — U component
-   **Blue ( B )** channel — V component

Since RGBA channels are 8-bit unsigned integers (`UInt8`, range 0–255), each channel alone cannot represent negative values or high resolution. To support negative wind speeds (opposite direction) and finer resolution, each channel is **linearly scaled** between a minimum and maximum value.

This scaling information is provided per timestep in the tile JSON, using the following parameters:

`umin`

Minimum U wind speed (km/h)

`umax`

Maximum U wind speed (km/h)

`vmin`

Minimum V wind speed (km/h)

`vmax`

Maximum V wind speed (km/h)

## Decoding

Given a pixel's R and B values, the actual wind speed is reconstructed by linearly mapping the 0–255 range back to `[umin, umax]` and `[vmin, vmax]`:

```
U = umin + (R / 255) * (umax - umin)
V = vmin + (B / 255) * (vmax - vmin)

```

So an R value of `0` corresponds to `umin`, and an R value of `255` corresponds to `umax` — and equivalently for the B channel with `vmin` / `vmax`.




## Map Data (Tiles)

Wind Vector Map Alps

### Available upon Request

(change `{t}` to a number of an available time step)
