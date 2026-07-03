# Godot License File

Godot asset store now requires the zip to include a license file.
So, we need to update the workflow to copy LICENSE.txt from the root, into the dist dir that will endup being the Godot addon zip.

## Checklist

- [x] Locate the Godot add-on packaging workflow.
- [x] Update the workflow to include root `LICENSE.txt` in the Godot add-on zip.
- [x] Verify the generated zip contains `LICENSE.txt`.
