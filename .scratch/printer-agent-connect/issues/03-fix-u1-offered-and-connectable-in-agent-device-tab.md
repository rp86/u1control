# 03: The U1 shows up in the Device tab and connects with the u1control agent

**What to build:** With the u1control printer agent set in a copy of the U1 printer preset and the host filled in, OrcaSlicer's Device tab lists the U1 and connects to it on a fresh start, with no earlier connect needed, and then shows its status as before. Root cause per ticket 01. If the diagnosis shows more than one cause, split this ticket.

**Blocked by:** 01

**Status:** done on fix/agent-device-discovery (not pushed)

- [x] On a fresh agent with the configured host, discovery announces the U1
- [x] Connecting from that entry reaches the connected state and pushes status
- [x] Regression test fails before the fix and passes after
- [x] Existing agent tests (including multi-U1 job routing) still pass

