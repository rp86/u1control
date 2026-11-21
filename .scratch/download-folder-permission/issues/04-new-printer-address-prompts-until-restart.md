# 04: A printer address first used after load may still prompt per URL until restart

**What to build:** Find out whether a printer or Spoolman address that was not known at load (first run, or a changed address) prompts per URL until OrcaSlicer restarts, and what it would take to avoid that.

**Blocked by:** None

**Status:** done on fix/download-folder-grant (3aae43b); confirmed by the reporter

- [ ] The reporter says whether their prompts were for web addresses (http://...) or for files on disk
- [ ] Decide whether a fix is possible: grants are only declared at load


## Questions for the reporter

- Does the prompt show a web address (`http://<printer>/server/files/gcode/.thumbs/...`) or a file path on the Mac?
- Does it still appear after OrcaSlicer is restarted, with the printer address already set in U1 Control's settings or used once before?
- Is there a log line `network permission: settings not readable at load` in `python_*.log`?

## Outcome

This was the real cause of #73 (see spec.md, Root cause). Tickets 02 and 03 were a smaller, separate fix for the download folder.
