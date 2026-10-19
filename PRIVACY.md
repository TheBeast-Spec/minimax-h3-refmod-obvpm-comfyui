# Public release privacy

The release contains one blank workflow and text documentation.

## Removed from the workflow

- Selected image filenames and any image-loader content references.
- Character names, descriptions, personal project names and subfolder selections.
- Original free-text notes.
- Workflow and session UUIDs, revision and viewport metadata.
- Nonstandard duplicated widget metadata and unrecognized node properties.

Only the functional graph, generic settings, public model filename, node identifiers and new setup instructions remain. The JSON contains no embedded media, preview images or encoded binary payloads. Reference images, saved RefMod weights and generated results are not included.

## Publication checks

- Parse the workflow and verify node types, all links, socket indices and widget order.
- Verify both image loaders are blank and character fields are generic or empty.
- Scan release files for local paths, private addresses, credential patterns, encoded media and personal identifiers.
- Check the exact Git file list and commit contents before pushing.
- Use the GitHub account's no-reply commit email.
- Publish from a new repository history containing only the reviewed release.

The GitHub account name and normal Git commit timestamps remain public. The `.gitignore` allows only the reviewed release filenames; it does not sanitize later edits to those files. Review any future re-export before publishing it.

The release is structurally checked. A new image-extraction run is not part of the public package; users must supply their own inputs and installed models.
