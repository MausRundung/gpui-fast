# gpui-fast

GPUI with gpui-fast rendering and layout optimizations.

Source and documentation: [https://github.com/longbridge/gpui-fast](https://github.com/longbridge/gpui-fast).

Forked from Zed's GPUI; distributed under Apache-2.0.

Use the core as `gpui = { package = "gpui-fast", version = "0.1.13" }` to preserve paths emitted by its macros.

## This fork

An unmodified copy of the published `gpui-fast` 0.1.13 crate plus one patch:
on Windows, rounded overflow scopes are painted without the GPU clip mask,
because the Direct3D 11 backend can evaluate that mask to zero coverage and
silently drop the scope's whole content (see `src/fast/rounded_clip.rs`).
The rectangular overflow mask still applies, so content is clipped to the
scope's bounds with square corners. `GPUI_ROUNDED_CLIPS=1` restores the
original masking for testing.
