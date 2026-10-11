<p align="center">
  <img src="docs/images/orke-mark.png" width="88" alt="orke logo">
</p>

<h1 align="center">orke for Mac</h1>

<p align="center">
  A workspace for AI coding agents: terminals, web pages and Git in one window.
</p>

<p align="center">
  <a href="https://orke.bomtobe.com">Homepage</a> ·
  <a href="https://orke.bomtobe.com/support/">Support &amp; FAQ</a> ·
  <a href="https://github.com/bomtobe-hgkim/orke-mac/releases">Mac releases</a> ·
  <a href="https://github.com/bomtobe-hgkim/orke-linux">Linux downloads</a>
</p>

This repository contains **macOS downloads and installation instructions**. The orke interface is in Korean. This repository was renamed from `orke-releases` on October 11, 2026; its macOS releases and Git history are preserved, and Linux releases now live in [orke-linux](https://github.com/bomtobe-hgkim/orke-linux).

## Download

**orke 3.4.1 — macOS 26 or later, Apple Silicon (arm64).** Intel Macs are not supported.

**[Download orke-macOS-arm64.dmg](https://github.com/bomtobe-hgkim/orke-mac/releases/download/v3.4.1/orke-macOS-arm64.dmg)** · [SHA-256 file](https://github.com/bomtobe-hgkim/orke-mac/releases/download/v3.4.1/orke-macOS-arm64.dmg.sha256)

The DMG is signed with an Apple Developer ID and notarized by Apple. The current 3.4.1 DMG was built and verified on October 10, 2026. The repository split does not change the file.

## Install or update

1. Download the DMG above.
2. Optional: download its SHA-256 file into the same folder and check it in Terminal:

   ```bash
   shasum -a 256 -c orke-macOS-arm64.dmg.sha256
   ```

   It should print `orke-macOS-arm64.dmg: OK`.
3. Open the DMG and drag **orke.app** into **Applications**. To update, quit orke first and replace the existing app.
4. Open orke from Applications. Install the coding agents you want and sign in with your own accounts; ordinary terminals need no AI subscription.
5. Start a session from the Dock and choose an agent and working folder.

Quit orke when you want to stop all its sessions. Closing its window keeps the running work available.

## What you can do

- Run coding agents next to ordinary terminals.
- Open web pages in the workspace and let agents work with the same pages.
- Review changes, diffs and Git history, then stage, commit, fetch, pull and push.
- Find and reopen terminal sessions while orke is running.
- Manage agent accounts, usage and supported packages.
- Use your own ngrok address to reach the workspace from another device.

For setup and feature details, see the [homepage](https://orke.bomtobe.com) and [support page](https://orke.bomtobe.com/support/). Install agents from their providers; each provider's terms, limits and charges apply.

## Previous macOS releases

| Version | Original date | Notes |
| --- | --- | --- |
| [3.4.1](https://github.com/bomtobe-hgkim/orke-mac/releases/tag/v3.4.1) | 2026-10-10 | Current signed and notarized DMG, including built-in web windows. See the release notes for the tested build and its checksum. |
| [3.1.3](https://github.com/bomtobe-hgkim/orke-mac/releases/tag/v3.1.3) | 2026-09-19 | Earlier signed and notarized macOS build. The app inside is named BOM.app and predates later features. |
| [2.2.2](https://github.com/bomtobe-hgkim/orke-mac/releases/tag/v2.2.2) | 2026-07-12 | Earlier Legacy app, kept for history. |

## Other platforms and help

- [Linux server downloads and install guide](https://github.com/bomtobe-hgkim/orke-linux)
- [Windows — Microsoft Store](https://apps.microsoft.com/detail/9N7G0NK63QGR)
- [Support & FAQ](https://orke.bomtobe.com/support/) · [Privacy policy](https://orke.bomtobe.com/privacy/) · [Terms](https://orke.bomtobe.com/terms/)
- Contact: [bomtobe.sw@gmail.com](mailto:bomtobe.sw@gmail.com). Include your orke version, macOS version and the agent you were using.
