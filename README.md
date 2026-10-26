# MiniMax H3 RefMod + OBVPM workflows

Two cleaned workflows from Noncoder's ComfyUI tutorial: create reusable character references, then build a video with ChanonDevs' OBVPM timeline.

Create a reusable character RefMod from your own portrait and full-body reference images, then load it in a compatible MiniMax H3 video workflow.

## What's new in Workflow 2 (October 2026)

- **Character maker built in.** Group **0 · New character** makes a character RefMod from two photos, so you no longer need to switch to Workflow 1.
- **Voice maker (experimental).** The same group makes a voice RefMod from a clean voice clip. Pick it next to the character, and the character speaks in that voice.
- **Faster runs with the `lightx2v` preset.** 8 steps instead of 20. A 10-second take at 0.5 megapixels took 161 s instead of 372 s on a 16 GB RTX 5070 Ti. See [Faster runs](#faster-runs-the-lightx2v-preset).
- **Megapixel table restored.** The note listing the resolution of each megapixel setting is back; the first public copy replaced it by mistake.

## Downloads

- [Workflow 1 - Create Character Reference](workflows/01%20-%20Create%20Character%20Reference.json)
- [Workflow 2 - Make and Extend Video](workflows/02%20-%20Make%20and%20Extend%20Video.json)

Use the file page's **Download raw file** button, or **Code > Download ZIP** for both files. Drag a workflow JSON onto the ComfyUI canvas.

Workflow 2 is Noncoder's RefMod-integrated adaptation of the OBVPM timeline, based on the later corrected-upscale copy. It includes generation, extension, looping, prepending, bridging and upscaling. Its corrected upscaler connection and compatibility sockets are preserved. This is a community adaptation; the original OBVPM workflow is by ChanonDevs.

## Workflow 1 - create character references

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

Workflow 1 intentionally cannot run until you provide images.

## Workflow 2 - make and extend video

1. Install the dependencies below and restart ComfyUI. Open Workflow 2.
2. Make your character RefMods in group **0 · New character** (see below) or with Workflow 1. Refresh the RefMod list and select your own characters in **Characters - pick your RefMods**. All eight selections start at `(none)`.
3. In **Prompt & Seed**, write your scene prompt and replace `my_film` with a new project folder name. The prompt is deliberately blank.
4. Select model files installed on your machine in the generation and upscale settings. Public model basenames are provided as starting selections; folders and available models can differ between installations.
5. Start with a short generation at **0.5 megapixels**, **16:9**, and **10 seconds**. The timeline is empty and upscaling is off.
6. Review each result and add accepted clips to the timeline. Choose extend, loop, prepend or bridge for subsequent runs, and update the prompt to describe the next action.
7. Build and inspect the full timeline before upscaling. Check that the timeline contains every intended clip and that the next-run indicator describes the operation you want.

The starting upscale target is **2 megapixels, not 4K**. Choose a suitable target for your GPU, and verify the exported pixel dimensions before calling a result 4K. RefMod helps reuse character references; identity, motion and audio still need review.

### Make a character or a voice (group 0)

1. Add two photos of the same person: **Photo 1 · full body** and **Photo 2 · close-up**.
2. Type a unique **name** in **Character maker**. Reusing a saved name can replace that file.
3. Turn on **Save new characters**.
4. Click **Character result**, then press ▶ (*Execute to selected output nodes*) in the bar above it.
5. Turn **Save new characters** off again.
6. In **1 · Characters**, refresh the RefMod list and pick your new name.

For a voice, add a clean clip to **Voice clip** (one speaker, no music, 10–30 s), name it in **Voice maker (experimental)**, then do steps 3–6 with **Voice result**. Pick the voice in its own RefMod slot next to the character. Voice RefMods are experimental: check every take by ear.

Both loaders and the voice clip start empty. Until you add files, a normal Run skips the two makers (ComfyUI outlines the empty loaders) and still generates your shot.

### Faster runs: the lightx2v preset

In **4 · Model & speed settings**, open the preset list on **H3 Generation Engine Settings** and pick `lightx2v`. It sets 8 steps, sampler `res_multistep` and scheduler `simple`, and loads the turbo LoRA. Leave the steps at 8: the LoRA is trained for 8 steps. The default preset stays `vanilla` (20 steps, no LoRA).

The preset needs [`minimax_h3_ref2v_turbo_8step_v1.0_768p_comfyui_bf16.safetensors`](https://huggingface.co/lightx2v/Minimax-h3-Turbo/blob/main/minimax_h3_ref2v_turbo_8step_v1.0_768p_comfyui_bf16.safetensors) from lightx2v. Put it directly in `models/loras`, not in a subfolder. If your copy has another name, select it in the preset's `turbo_lora` field.

### Dependencies

Install missing nodes through ComfyUI Manager and consult the original projects for model requirements:

- [comfyui-obvpm](https://github.com/chanon/comfyui-obvpm), **0.2.16+**.
- [comfyui-obvpm-timeline](https://github.com/chanon/comfyui-obvpm-timeline), **0.1.4+**.
- [ComfyUI-MiniMaxH3Mod](https://github.com/Luisacaotica/ComfyUI-MiniMaxH3Mod), with the character and voice creators (**0.2.7+**, tested on 0.2.7).
- [ComfyUI-KJNodes](https://github.com/kijai/ComfyUI-KJNodes), **1.5.0+**.
- [rgthree-comfy](https://github.com/rgthree/rgthree-comfy), **1.0.0+**.
- [ComfyUI-MiniMax-H3-Turbo](https://github.com/Larryvrh/ComfyUI-MiniMax-H3-Turbo), **1.2.2+**.
- [ComfyUI-Spectrum-MiniMax-H3](https://github.com/xmarre/ComfyUI-Spectrum-MiniMax-H3), **0.2.9+**.
- [Comfyui_Minimax_h3_latent_Upscaler](https://github.com/LBH-123-AI/Comfyui_Minimax_h3_latent_Upscaler), with `enable_temporal_chunking` support.

Use a ComfyUI version that supports MiniMax H3 and nested subgraphs. Some dependencies belong to optional optimization branches but their node definitions must still be available to open the complete graph. Turbo LoRA and Spectrum are off in the default engine preset. If a saved model selection is unavailable, select the corresponding installed file; optional turbo presets require their own compatible LoRAs.

### Main model selections

| Purpose | Selected filename |
|---|---|
| Diffusion model | `minimax_h3_ref2va_pruned_int8_convrot.safetensors` |
| Text/vision encoder | `qwen3vl_32b_minimax_h3_nvfp4_awq.safetensors` |
| Generation video VAE | `minimax_h3_video_vae_int8_convrot.safetensors` |
| Upscale video VAE | `minimax_h3_video_vae_fp16.safetensors` |
| Audio VAE | `minimax_h3_audio_vae_fp32.safetensors` |
| Live preview | `taeh3.safetensors` |
| Latent upscaler | `minimax_h3_latent_upscaler_3d_conv_v1_fp16.safetensors` |
| Turbo LoRA (`lightx2v` preset only) | `minimax_h3_ref2v_turbo_8step_v1.0_768p_comfyui_bf16.safetensors` |

No sample images, character RefMod files, videos, model weights or personal project data are distributed here. See [PRIVACY.md](PRIVACY.md) for release checks. The exported graph was checked structurally; it has not been run as a fresh generation after sanitization.

## Credits and related tools

- RefMod extraction: [Luisacaotica / ComfyUI-MiniMaxH3Mod](https://github.com/Luisacaotica/ComfyUI-MiniMaxH3Mod).
- Original OBVPM timeline: [ChanonDevs' OBVPM 007 video](https://youtu.be/k5GF5cu72ps) and [chanon / comfyui-obvpm-timeline](https://github.com/chanon/comfyui-obvpm-timeline).
- Model files: [Comfy-Org / MiniMax-H3](https://huggingface.co/Comfy-Org/MiniMax-H3).
- 8-step turbo LoRA: [lightx2v / Minimax-h3-Turbo](https://huggingface.co/lightx2v/Minimax-h3-Turbo).

Workflow 2 is distributed under the upstream GPL-3.0 license; see [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) and the [included license](licenses/OBVPM-GPL-3.0.txt). This repository distributes workflow configurations, not model weights or custom-node implementations. Those projects' licenses and requirements apply separately.
