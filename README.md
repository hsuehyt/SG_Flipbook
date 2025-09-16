# SG_Flipbook (Tiled Flipbook Shader Graph)

Unity Shader Graph for flipbook sprites, seamlessly tiling and scaling loops like rain or snow on GameObject-based skyboxes.

![Shader Graph](https://github.com/hsuehyt/SG_Flipbook/blob/main/images/ShaderGraph.png)

WHAT IT’S FOR
• Flipbook sprite rain, snow, sparkles, flowing noise, fireflies, etc.
• Works on any mesh (planes, domes, cubes), including GO-based skyboxes.

WHY A GAMEOBJECT-BASED SKYBOX
• Timeline/Activation friendly: animate, fade, or swap sky “layers” like any other object.
• Multiple layers: stack parallax clouds, rain, stars without custom skybox shaders.
• Post-processing and sorting: render order, transparency, and effects are easy to manage.
• Flipbook tiling: Shader Graph flipbooks need UVs; a dome/quad gives you clean UVs.

REQUIREMENTS
• Unity 6.x URP with Shader Graph
• A uniform grid sprite sheet (Columns × Rows), PNG preferred

![Inspector](https://github.com/hsuehyt/SG_Flipbook/blob/main/images/inspector.png)

QUICK START

1. Create a Material from SG\_Flipbook.
2. Assign FlipbookTex to your sprite sheet.
3. Set Columns and Rows to match the sheet.
4. Set FPS (e.g., 12–24).
5. Make the pattern smaller by increasing Repeat (e.g., 4,4 → 8,8).
6. If you see empty space inside each tile, raise InnerZoom (e.g., 1.2–1.6).
7. Use different StartFrame values per object to desync instances.

APPLYING IT TO A GAMEOBJECT-BASED SKYBOX
• Add a large sphere/dome mesh around the level (normals facing inward).
• UVs should be non-distorted; a proper skydome asset helps.
• Assign the SG\_Flipbook material.
• Tweak Repeat until streaks look right; adjust InnerZoom to tighten spacing.
• If rows play upside-down, toggle Invert Y in the graph or flip the texture.


MATERIAL PROPERTIES (what to tweak)
• FlipbookTex (Texture2D): your sprite sheet atlas.
• Columns, Rows (Float): grid size of the sheet.
• FPS (Float): playback speed in frames per second.
• StartFrame (Float): starting frame index; rounded to integer.
• Repeat (Vector2): tiles the animation across UVs; higher = smaller, denser pattern.
• Offset (Vector2): slides the tiled pattern to hide mesh seams.
• InnerZoom (Float): enlarges content inside each repeated cell to reduce visual gaps.
• Tint (Color) and Exposure (Float): quick look controls.

TEXTURE IMPORT TIPS (avoid seams)
• Wrap Mode: Repeat.
• Filter Mode: Bilinear (Point for pixel art).
• If thin lines appear between frames: disable Mip Maps and/or export the sheet with 2–4 px padding/extrude between frames; keep a uniform grid (don’t trim per-frame).

TIMELINE / LAYERING TIPS
• Put rain, clouds, and stars on separate GOs with their own SG\_Flipbook materials.
• Use Timeline activation or Animation clips to fade in/out, change Repeat/FPS/StartFrame.
• Sorting Group or render queues help ensure foreground rain draws over distant layers.

COMMON ISSUES
• Not animating: check FPS > 0 and Columns × Rows matches the atlas.
• Jumps or hangs: ensure Tile is driven by modulo of total frames (built into this graph).
• Wrong playback order: toggle Invert Y or flip texture vertically.
• Pattern too big: raise Repeat; still roomy inside each tile: raise InnerZoom.
• Visible lines: disable Mip Maps and re-export with padding/extrude.

EXAMPLE SETTINGS
• Rain on dome: Columns 6, Rows 4, FPS 18, Repeat 10,10, InnerZoom 1.35, StartFrame varied.
• Sparse snow on quad: Columns 4, Rows 4, FPS 12, Repeat 6,6, InnerZoom 1.2.

PERFORMANCE NOTES
• Prefer tiling (Repeat) over giant textures.
• Disable unnecessary mipmaps for thin, high-contrast lines to avoid shimmer.
• Vary StartFrame and Offset with Material Property Blocks for many instances.

LICENSE
MIT
