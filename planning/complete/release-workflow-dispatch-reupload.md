# Release workflow dispatch and asset replacement

## Goal

Allow the release workflow to run manually with a version input and ensure rerunning against an existing release replaces release assets instead of accumulating duplicates.

## Checklist

- [x] Inspect current release workflow behavior.
- [x] Add `workflow_dispatch` support with a required version input.
- [x] Normalize manual version input to the release tag/version used by the workflow.
- [x] Ensure upload replaces existing assets for already-created releases.
- [x] Validate the updated workflow syntax and shell logic where practical.
