# MiniMax H3 RefMod + OBVPM workflow

**Workflow 1: Create Character Reference** from Noncoder's ComfyUI tutorial.

Create a reusable character RefMod from your own portrait and full-body reference images, then load it in a compatible MiniMax H3 video workflow.

This release contains the reference-creation workflow only. The OBVPM video timeline, looping, bridging and upscaling workflow is not included in this release.

## Download and open

1. Download [01 - Create Character Reference.json](workflows/01%20-%20Create%20Character%20Reference.json), or use **Code > Download ZIP**.
2. Drag the JSON file onto your ComfyUI canvas.
3. Install [ComfyUI-MiniMaxH3Mod](https://github.com/Luisacaotica/ComfyUI-MiniMaxH3Mod), with standalone creator support from version 0.2.6 onward. Restart ComfyUI after installation.
4. Put a compatible H3 video VAE in `models/vae`. The selected filename is `minimax_h3_video_vae_fp16.safetensors`, available in [Comfy-Org's MiniMax-H3 VAE folder](https://huggingface.co/Comfy-Org/MiniMax-H3/tree/main/vae). Select the corresponding file in the VAE node.
5. Upload your own images into both blank image loaders. Use the same character in both references. For one image, remove the unused loader and its connection.
6. Set a unique RefMod name before running. Reusing a saved name can replace that file.
7. Run the workflow. With **save** enabled, the reference is written under your configured `models/refmods` directory. Refresh the RefMod list in your video workflow to select it.

## Starting settings

| Setting | Value |
|---|---|
| Mode | Full Reference |
| Concept type | identity |
| Reference resolution | 512 |
| Refinement steps | 0 |
| Maximum tokens | 5120 |
| Budget policy | error |
| Save | enabled |

The extraction stage uses the H3 video VAE; it does not require loading the H3 diffusion model. If a reference exceeds the token budget, reduce its resolution or adjust the budget to suit your available memory.

The workflow intentionally cannot run until you provide images. No sample images, character RefMod files, videos, model weights or personal project data are distributed here. See [PRIVACY.md](PRIVACY.md) for release checks.

## Credits and related tools

- RefMod extraction: [Luisacaotica / ComfyUI-MiniMaxH3Mod](https://github.com/Luisacaotica/ComfyUI-MiniMaxH3Mod).
- OBVPM timeline used in the tutorial's later video stage: [chanon / comfyui-obvpm-timeline](https://github.com/chanon/comfyui-obvpm-timeline).
- Model files: [Comfy-Org / MiniMax-H3](https://huggingface.co/Comfy-Org/MiniMax-H3).

This repository distributes a workflow configuration, not those projects' source code or model files. Their licenses and requirements apply separately.
