# 01: Reproduce and diagnose why the U1 never appears in the OrcaSlicer Device tab with the u1control agent

**What to build:** A failing test or log trace that pins down why, with the u1control printer agent selected, the U1 is not offered as a printer to connect to in OrcaSlicer's Device tab (the stock agent connects fine). Confirm or refute the leading hypothesis: the agent's discovery step announces the U1 only once a host is already known, but the host is only learned during connect, so on a fresh session nothing is ever announced. Also check where the printer agent's host from the printer preset is supposed to reach the agent, and whether that path is used at all. Use the `diagnosing-bugs` skill.

**Blocked by:** None (can start immediately).

**Status:** ready-for-agent

- [ ] Symptom reproduced against current upstream main in a test with a fake host callback (no OrcaSlicer needed)
- [ ] Root cause stated in one paragraph, with evidence
- [ ] Findings written up in this ticket for ticket 03 to build on

