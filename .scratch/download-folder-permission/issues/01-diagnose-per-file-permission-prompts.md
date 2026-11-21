# 01: Pin down which permission prompts repeat per file

**What to build:** A written finding that says which OrcaSlicer permission category repeats per file (network URL or filesystem path), with evidence from OrcaSlicer's permission rules and from what the plugin declares, and a test that shows the declaration that is wrong.

**Blocked by:** None (can start immediately).

**Status:** ready-for-agent

- [x] The plugin's declared grants are listed, with how OrcaSlicer matches each kind
- [x] The declaration that does not cover files inside the download folder is identified
- [x] A failing test shows it

## Findings

Network grants are host-wide as declared (`scheme://host`). The download folder is declared as a bare directory, which OrcaSlicer reads as one exact path, so each file saved into it prompts separately and is remembered per file. Not confirmed against the reporter's actual prompt text. Correction: thumbnails and `/screen/touch` are network requests, not files, so they are not explained by the download folder grant.
