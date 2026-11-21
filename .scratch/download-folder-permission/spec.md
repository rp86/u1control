# Upstream issue #73: permission prompts generated per file, not per directory

Source: https://github.com/bloodf/u1control/issues/73 ("Gcode thumbnail permissions generating endlessly", u1control 0.15.1, OrcaSlicer 2.5.1, macOS, Extended Firmware). Reporter's text: permissions for `server/files/gcode/.thumbs/*` are generated per file, not for the directory; a comment adds the same for `server/files/timelapse/*` and `/screen/touch/*`.

## Reading of the problem (from OrcaSlicer's own permission docs and source)

- Network: a canonical `scheme://host` entry is host-wide (every path, port, query). The plugin already declares one per printer and Spoolman at load (#48), so a printer already known at load does not prompt per URL.
- Filesystem: `fs_read` / `fs_readwrite` targets are exact paths or `<dir>/*` trees. The plugin declares `fs_readwrite` as the bare folder `~/Downloads/u1control`, which is an exact path. Every new file saved into it (time-lapse videos, pictures, thumbnails, camera pictures) is a new runtime prompt, and OrcaSlicer saves the approval for that one file.
- The reporter's prompt text is not in the issue (empty log), so which of the two prompts they saw is not confirmed.

## Correction after review

- Thumbnails (`.thumbs/*`) and time-lapse covers are returned to the page in memory; nothing is written to disk for them. `/screen/touch` is a POST to the printer. Those three paths in the report are network URLs, so the download-folder grant does not touch them. It does fix real per-file prompts for files saved to the download folder (time-lapse videos, pictures).
- Per-URL network prompts happen only when the printer's origin was not granted at load: the origins come from the settings `host` and the printers used before (`network_origins`), and a printer first used in a session is left to runtime prompts until the next load. That is ticket 04.

## Root cause (confirmed 2026-11-21)

OrcaSlicer 2.5.1 answers `plugin.storage()` only for a registered plugin with a current-plugin context, never inside `register_capabilities`. The settings could not be opened at load, so the load-time network request carried no printer address and every URL prompted for itself (the per-URL entries in the Permissions tab). Fix: the printer's `scheme://host` is kept in `<OrcaSlicer data dir>/u1control/hosts.json` (data dir from the plugin's install path, as in the Profile Library plugin) and read at load. Verified by the reporter: the per-URL prompts stopped. After an Opus review the work was split into two minimal branches built on upstream's `peers.py` helpers (hosts file beside presence.json): `fix/load-time-network-grant` (the real #73 fix) and `fix/download-folder-grant` (one-line tree grant). Not pushed.
