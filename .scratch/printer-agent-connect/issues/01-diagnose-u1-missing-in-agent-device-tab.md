# 01: Reproduce and diagnose why the U1 never appears in the OrcaSlicer Device tab with the u1control agent

**What to build:** A failing test or log trace that pins down why, with the u1control printer agent selected, the U1 is not offered as a printer to connect to in OrcaSlicer's Device tab (the stock agent connects fine). Confirm or refute the leading hypothesis: the agent's discovery step announces the U1 only once a host is already known, but the host is only learned during connect, so on a fresh session nothing is ever announced. Also check where the printer agent's host from the printer preset is supposed to reach the agent, and whether that path is used at all. Use the `diagnosing-bugs` skill.

**Blocked by:** None (can start immediately).

**Status:** done (see Findings)

- [x] Symptom reproduced against current upstream main in a test with a fake host callback (no OrcaSlicer needed)
- [x] Root cause stated in one paragraph, with evidence
- [x] Findings written up in this ticket for ticket 03 to build on


## Findings

Root cause: OrcaSlicer lists printers in the Device tab from the printer agent's discovery messages, and asks for discovery before it connects. `U1Agent.start_discovery` announced the U1 only when `self.host` was set, and `self.host` was only set by `connect_printer`. On a fresh session nothing was announced, so the U1 was never offered and could never be connected. The stock agent announces the preset's configured host. The existing test connected first, which hid the bug.

The preset's `print_host` was not reaching the agent at all before connect. Fix: announce the connected host, else U1 Control's `host` setting, else the selected U1 preset's `print_host` (read on the UI thread).

Branch `fix/agent-device-discovery` (commits a80ed37 and the follow-up). The new tests fail on upstream `16fe5ed` and pass on the branch.
