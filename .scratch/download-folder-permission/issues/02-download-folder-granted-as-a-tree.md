# 02: Saved printer files go to the download folder without a prompt per file

**What to build:** Saving a time-lapse, a picture, a thumbnail or any other printer file to the download folder asks for permission once for the folder, not once per file. The folder grant covers the files inside it.

**Blocked by:** 01

**Status:** done on fix/download-folder-grant (not pushed)

- [x] The plugin declares the download folder as a tree (`<folder>/*`), the same form as the sliced-job grant
- [x] One place names the folder, so the grant and the downloads can't drift apart
- [x] Declaring the grant at load creates nothing on disk
- [x] A test fails without the change and passes with it

