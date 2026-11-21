# Upstream issue #73: permission prompts generated per file, not per directory

Source: https://github.com/bloodf/u1control/issues/73 ("Gcode thumbnail permissions generating endlessly", u1control 0.15.1, OrcaSlicer 2.5.1, macOS, Extended Firmware). Reporter's text: permissions for `server/files/gcode/.thumbs/*` are generated per file, not for the directory; a comment adds the same for `server/files/timelapse/*` and `/screen/touch/*`.

## Reading of the problem (from OrcaSlicer's own permission docs and source)

- Network: a canonical `scheme://host` entry is host-wide (every path, port, query). The plugin already declares one per printer and Spoolman at load (#48), so a printer already known at load does not prompt per URL.
- Filesystem: `fs_read` / `fs_readwrite` targets are exact paths or `<dir>/*` trees. The plugin declares `fs_readwrite` as the bare folder `~/Downloads/u1control`, which is an exact path. Every new file saved into it (time-lapse videos, pictures, thumbnails, camera pictures) is a new runtime prompt, and OrcaSlicer saves the approval for that one file.
- The reporter's prompt text is not in the issue (empty log), so which of the two prompts they saw is not confirmed.
