# Public release privacy

The release contains two cleaned workflow configurations, documentation and an upstream license. No media is included.

## Removed from the workflow

- Selected image filenames and any image-loader content references.
- The character maker's photos, the voice maker's voice clip and their saved names.
- Character names, descriptions, personal project names and subfolder selections.
- Personal free-text notes. Two generic instruction notes are kept: the megapixel table and the steps for making a character.
- Workflow and session UUIDs, revision and viewport metadata.
- Nonstandard duplicated widget metadata and unrecognized node properties.
- Timeline clip paths, pin/bridge state and the pending upscale operation.
- Cached result previews, live previews and previous result decisions.
- Saved character RefMod selections and personal scene prompts.
- Model download metadata and personal model subfolder prefixes.

Workflow 2 starts with an empty timeline, blank scene prompt, `(none)` character selections and the generic `my_film` project folder. Group 0 starts with empty photo and voice loaders, the names `my_character_v1` and `my_voice_v1`, saving off and no cached results. It is exported from the current saved workflow, which keeps the corrected upscaler connection and graph wiring. Subgraph and port UUIDs are regenerated consistently: these identifiers are necessary for the nested graph and are not retained session identifiers.

Only the functional graphs, generic settings, public model filenames, necessary node configuration, public upstream credits and setup instructions remain. The JSON contains no embedded media, preview images or encoded binary payloads. Reference images, saved RefMod weights and generated results are not included.

## Publication checks

- Parse the workflow and verify node types, all links, socket indices and widget order.
- Verify every image and audio loader is blank and character and voice fields are generic or empty.
- Verify all eight timeline subgraphs and their boundary connections; verify timeline and result state is cleared.
- Scan release files for local paths, private addresses, credential patterns, encoded media and personal identifiers.
- Check the exact Git file list and commit contents before pushing.
- Use the GitHub account's no-reply commit email.
- Keep the repository history limited to reviewed release files; private originals are never staged.

The GitHub account name and normal Git commit timestamps remain public. The `.gitignore` allows only the reviewed release filenames; it does not sanitize later edits to those files. Review any future re-export before publishing it.

The release is structurally checked, including its embedded subgraphs. Fresh extraction and video-generation runs have not been performed after sanitization; users must supply their own inputs and installed models.
