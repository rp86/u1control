# 02: Make agent discovery and connect failures visible in the log

**What to build:** When the agent skips announcing the U1, or the first status read after connecting fails (wrong host or key, timeout, missing network permission), the reason is logged once, instead of silence until the printer has connected at least once. Someone reading OrcaSlicer's log can tell why the U1 is missing or not connecting.

**Blocked by:** None (can start immediately).

**Status:** ready-for-agent

- [ ] Skipped discovery logs why (no host known)
- [ ] A failure on the first status read logs its cause once, not every 2 s poll
- [ ] Existing connected-then-dropped logging is unchanged
- [ ] Tests cover both log paths

