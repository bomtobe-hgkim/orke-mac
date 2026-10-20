<p align="center">
  <img src="docs/images/orke-mark.png" width="88" alt="orke logo">
</p>

<h1 align="center">orke for Mac</h1>

<p align="center">
  A workspace for AI coding agents.<br>
  Bring terminals, web pages, agents and Git together on your Mac.
</p>

<p align="center">
  <a href="https://orke.bomtobe.com">Homepage</a> ·
  <a href="https://github.com/bomtobe-hgkim/orke-mac/releases">Mac releases</a> ·
  <a href="https://github.com/bomtobe-hgkim/orke-linux">Linux server</a> ·
  <a href="https://orke.bomtobe.com/support/">Support</a>
</p>

This README covers downloading and installing the app, starting your first session, connecting agents, remote access, command-line use, updates and removal. The examples below include Korean interface labels with their English meanings.

## Contents

- [Download](#download)
- [Install and open orke](#install-and-open-orke)
- [Start your first session](#start-your-first-session)
- [Agents and accounts](#agents-and-accounts)
- [Web windows, Git and packages](#web-windows-git-and-packages)
- [Connect from another device](#connect-from-another-device)
- [Use orke from Terminal](#use-orke-from-terminal)
- [Use orke support](#use-orke-support)
- [Update orke](#update-orke)
- [Files, logs and backups](#files-logs-and-backups)
- [Uninstall](#uninstall)
- [Troubleshooting](#troubleshooting)
- [Release and validation](#release-and-validation)

## Download

| Current download | Requirements |
| --- | --- |
| **orke 3.4.13** — [orke-macOS-arm64.dmg](https://github.com/bomtobe-hgkim/orke-mac/releases/download/v3.4.13/orke-macOS-arm64.dmg) | **macOS 26 or later, Apple Silicon** — M-series Macs |
| [Matching SHA-256 file](https://github.com/bomtobe-hgkim/orke-mac/releases/download/v3.4.13/orke-macOS-arm64.dmg.sha256) | Optional download verification |

**Intel Macs are not supported.** If unsure, choose the Apple menu → **About This Mac** and check the chip and macOS version. In Terminal, `uname -m` should report `arm64` when running natively; `sw_vers -productVersion` shows macOS.

The app includes its .NET runtime, Electron desktop component and orke's NVIDIA agent. **You do not need to install .NET, Node.js or Electron to run orke.** Coding agents, Git and optional Docker are installed separately as needed.

The DMG is Developer ID signed and Apple-notarized. Version **3.4.13** was built from the current product source on **October 20, 2026**. Its SHA-256 is:

```text
75e2458d0790058e2e5ee8e5b639f1d414b1222dc0e2f42de35e1a68bb75ee4b
```

### Check the download

Put the DMG and its `.sha256` file in the same folder, then open Terminal. For the normal Downloads folder:

```bash
cd "$HOME/Downloads"
shasum -a 256 -c orke-macOS-arm64.dmg.sha256
```

Expected output: **`orke-macOS-arm64.dmg: OK`**. If either file was renamed by your browser, use the matching original filenames or adjust the checksum file's filename reference. A mismatch means the files do not match; download both again before installing.

## Install and open orke

1. Open `orke-macOS-arm64.dmg` in Finder.
2. Drag **orke.app** into **Applications**.
3. Open **Applications → orke**. Launch the installed copy rather than leaving the app running from the mounted DMG.
4. Approve macOS's normal first-launch confirmation for the downloaded app, if shown.
5. Sign in to orke with Google in your default browser and return to the app. This Mac remembers your account for later starts.
6. After the installed app opens, eject the DMG in Finder.

When macOS needs an app-specific firewall allowance, orke requests administrator approval through the system dialog. Canceling that approval keeps the local app available.

After Google sign-in, an orke desktop window opens. Your work runs locally under your Mac user account. Install and sign in to an agent when you want AI assistance.

If macOS blocks opening the app, check the OS/chip requirements and checksum, then use [Apple's guidance for downloaded apps](https://support.apple.com/en-us/102445) or contact support with the exact message.

### Closing a window and quitting the app

| Action | What happens |
| --- | --- |
| Close the main desktop window | The app minimizes to the Dock and continues running; click its Dock icon to return. |
| Close a terminal tab/window | The terminal session can keep running; reopen it from **세션** — **Sessions**. |
| Close a web window inside the workspace | Its web tabs close, with leave-page confirmation when required. |
| Choose **orke 종료** — **Quit orke**, or press **Cmd+Q** | The app quits; terminal processes and web pages end. |

Live processes are not restored after quitting orke or restarting the Mac. Closing the main window and quitting the app are different actions.

## Start your first session

1. Use **Terminal 창 열기** — **Open Terminal window** — in the Dock to open **새 세션** — **New session**.
2. Leave the runtime at **내 PC** — **This PC** — to run on your Mac.
3. Choose **Terminal** for a normal shell, or choose an installed agent.
4. Under **작업 폴더** — **Working folder**, use **찾아보기…** — **Browse…** — to choose the folder you want to work in.
5. Select **시작** — **Start**.

For a first ordinary Terminal session, try:

```bash
pwd
git --version
```

`pwd` shows the selected working folder. If Git is missing, see [Git setup](#git). A first agent session needs that agent's installation and account sign-in from the next section.

| Korean label | Meaning / use |
| --- | --- |
| `세션` | Sessions; reopen work that is still running |
| `확인 필요` | Needs your check; often waiting for input |
| `작업 중` | Working |
| `탭만 닫기 (세션 유지)` | Close only this tab and keep its terminal session |
| `세션 종료…` | End the selected session and its process |
| `설정` | Settings |
| `정보` / `버전 복사` | About / Copy version; useful when asking for help |

Use **세션 종료…** when you actually want to stop a session. Read its confirmation: ending a session can discard the terminal output available in that live session.

## Agents and accounts

orke runs the agent CLIs installed on your Mac. Each provider's account requirements, terms, usage limits and charges still apply. Install tools as your normal Mac user.

### Claude Code

In macOS Terminal, use [Anthropic's native installer](https://code.claude.com/docs/en/setup):

```bash
curl -fsSL https://claude.ai/install.sh | bash
export PATH="$HOME/.local/bin:$PATH"
claude --version
claude auth login
```

Finish the browser authorization. Then reopen orke if it was already running and choose **Claude** in a new session.

### ChatGPT through Codex

Use OpenAI's [official Codex CLI installer](https://github.com/openai/codex#installing-and-running-codex-cli), then sign in with ChatGPT:

```bash
curl -fsSL https://chatgpt.com/codex/install.sh | sh
export PATH="$HOME/.local/bin:$PATH"
codex --version
codex login
```

Complete the browser sign-in, then choose **ChatGPT** in orke's new-session window. If browser callback login cannot complete, `codex login --device-auth` is the alternative; first enable device-code login in your ChatGPT security settings, as described in [OpenAI's authentication guide](https://developers.openai.com/codex/auth/).

The installers above track provider releases. An older orke package and a newly changed agent CLI are not automatically a tested combination. If orke support rejects a newer Codex feature policy, check for a compatible orke/CLI release; the server verification used Codex 0.160.1.

### OpenCode, Hermes and Antigravity

Install only the tools you want. Run their command once in Terminal to complete each provider's own login/setup:

| Agent | Install command | Start / sign in | Official instructions |
| --- | --- | --- | --- |
| OpenCode | `curl -fsSL https://opencode.ai/install \| bash` | `opencode` | [OpenCode](https://opencode.ai/docs/) |
| Hermes | `curl -fsSL https://hermes-agent.nousresearch.com/install.sh \| bash` | `hermes` | [Hermes](https://hermes-agent.nousresearch.com/docs/getting-started/installation/) |
| Antigravity | `curl -fsSL https://antigravity.google/cli/install.sh \| bash` | `agy` | [Antigravity](https://www.antigravity.google/docs/cli/install/) |

These are provider-supplied install methods, not a claim that every current provider version has been validated with this DMG. OpenCode's linked installer currently supplies its OpenCode 1 CLI and can replace a different OpenCode installation.

### NVIDIA

orke includes its own NVIDIA agent for the Mac's **This PC** runtime:

1. Get your key from [NVIDIA Build](https://build.nvidia.com).
2. Open **설정 → 계정 → NVIDIA API 키** — **Settings → Accounts → NVIDIA API key**.
3. Save the key, then choose **NVIDIA** in a new session.

The NVIDIA choice is unavailable in isolated sessions. Its live API use on Mac was not measured in the current release verification; the bundled Mac agent and its status reporting are separate from that live test.

### Manage more than one Claude/ChatGPT account

Open **설정 → 계정 → 계정 관리…** — **Settings → Accounts → Manage accounts…**. Use **계정 추가** — **Add account** — and follow the login flow. **현재** marks the current account; **다시 로그인** means **Sign in again**.

Switching an account changes this execution environment's actual shared CLI login files. It can affect agents already using that login; it does not pin a separate account to each open tab. OpenCode, Hermes and Antigravity manage their authentication through their own CLIs.

If an installed CLI is missing in orke, confirm it in Terminal using `command -v claude` or `command -v codex`, and see [troubleshooting](#troubleshooting).

## Web windows, Git and packages

### Web windows

Use **웹 창** — **Web windows** — to open a website inside the workspace. You and the agent work with the same page; website sign-in happens on the website and is saved in orke's web profile.

Use the page's element-selection or screenshot action when you want to give an agent context from a page. Closing that web window closes its web tabs. Right-click the Web tile in the Dock to close all web pages, with leave-page confirmation where required. Web pages do not reopen automatically when orke starts again. Reloading/recreating a page can lose unsaved forms and scroll position even though profile cookies remain.

### Git

Git is installed separately. In Terminal:

```bash
git --version
```

If macOS offers to install Command Line Tools, finish that installation. You can explicitly request it with:

```bash
xcode-select --install
```

Then use **git 저장소 열기** — **Open Git repository** — in orke and choose your repository. The Git window shows changed files, diffs and history and provides staging, commit, fetch, pull and push actions. Remote repository access uses your existing Git/SSH authentication.

### Packages and Hermes scheduled jobs

Open **패키지** — **Packages** — to work with repeating tasks and AI employees. Each area has its own named groups; use the area's plus button to create a group and choose a group when creating work. Hermes scheduled jobs belong to Hermes; orke shows their state and invokes Hermes's own commands for changes. Install/sign in to Hermes first if you want those features.

### Optional Docker isolation

**내 PC** is the normal Mac runtime. Docker-compatible isolation is optional and requires a running compatible engine. Install the agents and tools you want inside the isolated environment; its image does not supply agent CLIs.

The published isolation image is Linux amd64, so Apple Silicon runs it through emulation. That Mac Docker workflow was not validated for this release. Isolated sessions share a container and home volume; they do not mount your host folders, but network access to host services is still possible.

Host agent sessions run with your Mac user's permissions, and orke starts supported agents with permission prompts skipped. Choose working folders and instructions accordingly.

## Connect from another device

The Mac must remain on, awake, connected to the internet and running orke. Remote devices connect directly to its **public IPv4 over HTTPS**, normally on **port 48650**.

1. Sign in to orke with Google on the Mac.
2. Open **설정 → 다른 기기에서 접속** — **Settings → Access from another device**.
3. Prepare a trusted HTTPS certificate for the current public IPv4. Choose orke's automatic Let's Encrypt certificate management and accept the displayed CA terms, or import a suitable PFX containing the certificate, chain and private key.
4. Approve orke's app-specific Mac firewall allowance if requested, and allow the HTTPS port through your router. Automatic certificate issuance also needs public TCP 80 to reach the configured HTTP challenge listener. Configure forwarding yourself where necessary; CGNAT or a restricted network can prevent direct access.
5. Enable access and copy the **`https://PUBLIC-IP:48650`** address shown by orke.
6. Open that address on the other device, sign in with the **same Google account**, and complete the browser approval shown by orke.

See the [HTTPS and certificate guide](https://orke.bomtobe.com/en/docs/orke/remote/) for certificate requirements, public ports, renewal and connection troubleshooting. Do not use an expired certificate or bypass browser certificate errors.

Turning access off or signing out revokes remote authorization and connections while keeping live terminal sessions. The remote browser uses the same Mac workspace and its files. Phone browsers and compatible mobile clients use the same HTTPS address; Google and official approval pages open through the system browser in the mobile app.

## Use orke from Terminal

The Mac DMG includes orke's local control CLI. Open **orke.app** before using commands that talk to its running workspace.

### Enable the `orke` command

In **설정 → 터미널** — **Settings → Terminal**:

1. Open **Terminal에서 orke 사용** — **Use orke from Terminal**.
2. Select **연결할 파일 검토** — **Review files to connect**.
3. Review the proposed command wrapper and shell-profile changes.
4. Select **검토한 파일 적용** — **Apply reviewed files**.
5. Open a new macOS Terminal window and run:

   ```bash
   command -v orke
   orke help
   ```

This sets up a wrapper at `~/.local/bin/orke` and the necessary PATH block for supported zsh/bash profiles. Install the app in Applications first: setup refuses a copy running from the mounted DMG. It preserves unfamiliar existing command files rather than overwriting them.

### Run without changing PATH

The complete installed command path also works:

```bash
"/Applications/orke.app/Contents/Resources/runtime/orke" help
"/Applications/orke.app/Contents/Resources/runtime/orke" setup status --json
```

These help/setup-status operations do not need a running daemon. For a running workspace:

```bash
"/Applications/orke.app/Contents/Resources/runtime/orke" status --json
"/Applications/orke.app/Contents/Resources/runtime/orke" session list --json
"/Applications/orke.app/Contents/Resources/runtime/orke" package list --json
```

### Useful command families

| Command | Use |
| --- | --- |
| `orke help` | Show the installed management CLI's commands/options; browser/remote/service have separate syntax |
| `orke setup status --json` | Show offline CLI capabilities without starting the app; this does not verify the PATH wrapper |
| `orke status --json` | Inspect the running local daemon |
| `orke session list --json` | List its sessions |
| `orke session screen --id SESSION_ID --json` | Inspect one session's current terminal screen; use an ID from the list |
| `orke session output --id SESSION_ID --follow --json` | Follow output; Ctrl+C stops the observer, not the session |
| `orke package list --json` | Inspect the first page of packages; use its cursor for more |

The CLI also supports session creation, sending input, waiting and ending sessions, and package operations. Read `orke help` for each exact option. Command-created sessions are registered without opening a new desktop window; CLI submission success does not mean an AI task has finished.

Browser commands such as `orke browser tab.list --json` work inside an **orke This PC terminal/agent session** using that session's binding. From macOS Terminal, an operator can also use the running local browser from the exact folder of one existing orke workspace. See the [browser CLI guide](https://orke.bomtobe.com/en/docs/cli/browser/) for commands and workspace selection.

The Linux `orke service`, `orke update` and `orke uninstall` commands are for Linux server installations. On Mac, use the [DMG update](#update-orke) and [uninstall](#uninstall) procedures below.

## Use orke support

orke support lets a trusted backend ask questions through HTTP using Claude/ChatGPT signed in on this Mac.

1. Open **orke support** from the Dock.
2. Select **첫 AI 만들기** / **새 AI** — **Create first AI / New AI**.
3. Name the AI, choose Claude or ChatGPT and enter its instructions. Start with **기본 도구 쓰기** — **Use built-in tools** — off, and an empty **답 형식** — **Response format**.
4. Select **만들기** — **Create**. Save the access key displayed once in **연결** — **Connection**.
5. Try a question in **시험** — **Test**. The Connection tab then shows the matching request examples for your backend.

The default API is **`http://127.0.0.1:48700/v1`**, separate from the remote HTTPS browser address. The access key selects the AI. Codex must be signed in with ChatGPT; an API-key-only login is not accepted for orke support.

<details>
<summary>Terminal example: create a room and send a question</summary>

Run in macOS Terminal using zsh or bash. Paste the access key at the hidden prompt:

```bash
printf 'orke support access key: '
read -rs ORKE_KEY
printf '\n'
ORKE_SUPPORT='http://127.0.0.1:48700'

curl --fail-with-body -sS -X POST "$ORKE_SUPPORT/v1/rooms" \
  -H "Authorization: Bearer $ORKE_KEY" \
  -H 'Content-Type: application/json' \
  -d '{}'
```

Copy the returned `room_id` into the next assignment:

```bash
ROOM_ID='r_copy_the_returned_room_id'
curl --fail-with-body -sS --max-time 360 \
  -X POST "$ORKE_SUPPORT/v1/rooms/$ROOM_ID/messages" \
  -H "Authorization: Bearer $ORKE_KEY" \
  -H 'Content-Type: application/json' \
  -H 'Idempotency-Key: readme-first-question' \
  -d '{"text":"Reply with Hello."}'
```

A successful default response includes `output.answer`. Reuse the room ID for the same conversation; use a new idempotency key for a new question. If a request connection is lost, inspect results before resubmitting:

```bash
curl --fail-with-body -sS "$ORKE_SUPPORT/v1/rooms/$ROOM_ID/messages" \
  -H "Authorization: Bearer $ORKE_KEY"
```

</details>

For another computer's backend, configure an HTTPS reverse proxy forwarding to the support listener. The app's **orke support 설정** — **orke support settings** — provides nginx/Caddy examples; setting **바깥 주소** — **External URL** — changes example URLs and does not configure that proxy for you. Keep access keys in the backend rather than visitor-facing JavaScript. Built-in shell tools can act with your Mac user's permissions.

## Update orke

Mac updates use a new DMG:

1. Finish or save work. Updating requires quitting orke, which ends its running terminals, agents and web pages.
2. Choose **orke 종료** — **Quit orke**, or press **Cmd+Q**.
3. Download the current DMG and matching checksum from this repository's [releases](https://github.com/bomtobe-hgkim/orke-mac/releases).
4. Verify the checksum if desired, open the DMG and replace **Applications/orke.app**.
5. Open the installed app again and eject the DMG.

Settings and data remain in the configured orke data directory. The CLI wrapper set up by the app refers to the installed Applications path, so replacing the app at the same path keeps that command usable. Agent CLI updates are separate from the DMG update.

If moving from 3.1.3 or the older Legacy app, keep their existing data until you decide what to remove. Older product homes are not automatically migrated into the current `~/.orke` home, and automatic migration from those older releases was not validated.

## Files, logs and backups

| Location | Contents |
| --- | --- |
| `/Applications/orke.app` | Installed application |
| `~/.orke` | Default settings, accounts, remote-access data, web profiles and support records |
| `~/.orke/logs/daemon.log` | Detailed runtime log; rotated logs are alongside it |
| `~/.local/bin/orke` | Optional CLI wrapper created by reviewed PATH setup |
| `~/.zprofile` or `~/.bash_profile` | Shell profile that may contain orke's marked PATH block |

An **absolute `ORKE_HOME`** can override the data directory for a deliberately configured launch. Use the actual configured location when reading logs or backing up; changing a shell variable does not move existing app data.

After quitting orke, a private backup of the default data directory can be made in Terminal:

```bash
umask 077
tar -czf "$HOME/orke-data-$(date +%Y%m%d-%H%M%S).tar.gz" -C "$HOME" .orke
```

It can contain account information, keys and conversations. Keep it private. It does not include project folders, live terminal processes or the providers' separate `~/.claude`/`~/.codex` data.

To identify the installed version, use **설정 → 정보 → 버전 복사** — **Settings → About → Copy version**. You can also read the app version without launching it:

```bash
/usr/libexec/PlistBuddy -c 'Print :CFBundleShortVersionString' \
  /Applications/orke.app/Contents/Info.plist
```

The app's CLI does not implement an `orke --version` command; use About or the plist inspection above.

## Uninstall

### Remove the app and keep saved data

1. If you want orke support's associated Claude/Codex histories cleaned, delete its rooms/AIs while orke is still running and let the cleanup finish.
2. Quit orke with **Cmd+Q**.
3. Move **Applications/orke.app** to the Trash.

This leaves the saved data directory and separately installed agents/Docker in place.

### Optionally remove saved data

After backing up anything you need and completing support room cleanup, delete the actual orke data directory. For the default location:

```bash
rm -rf -- "$HOME/.orke"
```

This erases orke's saved accounts, settings, web profiles, keys and records. Provider files outside that directory are separate; do not delete your complete Claude/Codex home as part of removing orke.

### Optionally remove the CLI setup

If you enabled **Use orke from Terminal**, inspect `~/.local/bin/orke`. Remove it only if it is the wrapper created by orke, identified by `# orke-OWNED cli-wrapper v1`. In the shell profile, remove only its marked `# BEGIN orke CLI PATH v1` … `# END orke CLI PATH v1` block. Keep the rest of the profile and any unrelated command file.

### Optionally remove agent help skills

orke can install its help skills outside `~/.orke`, so removing the app/data may leave them behind. Default locations are:

| Skill | Default files |
| --- | --- |
| orke control guide | `~/.agents/skills/orke/SKILL.md`, `~/.claude/skills/orke/SKILL.md` |
| orke browser guide | `~/.codex/skills/orke-browser/SKILL.md`, `~/.claude/skills/orke-browser/SKILL.md`; eligible Antigravity setups also use `~/.gemini/antigravity-cli/skills/orke-browser/SKILL.md` |

Control guides contain `<!-- orke-OWNED control-guide v1 -->`; browser guides contain `<!-- orke-OWNED browser-guide v1 -->`. Inspect files before optionally removing an owned guide. Preserve user-edited/unowned files and the other skills in those directories. Custom `CLAUDE_CONFIG_DIR` and `CODEX_HOME` settings can change the relevant provider paths.

### Optionally remove Docker isolation data

If you used orke's isolated environment and want to erase its separate shared home, confirm there is no work you need inside it, then remove those named Docker resources:

```bash
docker rm -f orke
docker volume rm orke-home
```

These commands remove the isolated container and its home volume; removing the Mac app by itself does not remove them.

## Troubleshooting

| Symptom | Check and next action |
| --- | --- |
| App will not open | Confirm an Apple Silicon Mac and macOS 26+, verify the current checksum and launch the copy in Applications. Include the exact macOS message when asking for help. |
| App's window disappeared | Click the orke Dock icon; closing the main window leaves the app running. |
| Terminal tab closed | Open **세션** — **Sessions** — and reopen it if the app/session still runs. |
| Agent installed, but orke cannot find it | Run `command -v claude` / `command -v codex` in a new Terminal. Fix the login-shell PATH, then fully quit/reopen orke. Native user tools commonly need `~/.local/bin`; Apple Silicon Homebrew commonly uses `/opt/homebrew/bin`. |
| `orke: command not found` in Terminal | Complete reviewed PATH setup and open a new Terminal, or use the full app command path shown above. |
| PATH setup refuses the application location | Move the app from the mounted DMG into Applications and open that copy. |
| PATH setup refuses an existing wrapper | Inspect the existing command; preserve unrelated tools. Use the complete application path while deciding how to resolve the conflict. |
| CLI cannot connect to the daemon | Open the installed orke app first. Help and setup-status work offline; live session/status/package calls need the daemon. |
| External Terminal browser command reports unavailable | Open orke and use the exact working folder of one existing workspace, or use an orke This PC terminal/agent session. |
| HTTPS address cannot be reached | Check the public IPv4, port 48650, router forwarding, Mac firewall and possible CGNAT; follow the HTTPS guide above. |
| Certificate issuance or renewal fails | Check public TCP 80, forwarding to the configured challenge listener and the current CA agreement in the Mac settings. |
| Remote Google sign-in is refused | Use the same Google account as the Mac and complete approval for this browser. |
| Remote access disappears after sleep or quit | Keep the Mac awake and running orke while using it remotely. |
| New Linux `update`/`uninstall` instructions do not work on Mac | Those commands target the Linux server; update by replacing the DMG and uninstall using the steps above. |

For useful runtime details:

```bash
tail -n 100 "$HOME/.orke/logs/daemon.log"
```

Use your actual data location if customized. Include the version from About, chip, macOS version, agent and exact error in a support request. Remove access keys, tokens and private UI addresses from shared logs.

## Release and validation

| Version | Mac release date | Notes |
| --- | --- | --- |
| [3.4.13](https://github.com/bomtobe-hgkim/orke-mac/releases/tag/v3.4.13) | October 20, 2026 | Current signed and notarized DMG; work groups, CLI management, close-all web pages, browser and terminal fixes |
| [3.4.10](https://github.com/bomtobe-hgkim/orke-mac/releases/tag/v3.4.10) | October 18, 2026 | Previous signed and notarized DMG; Google member sign-in and direct HTTPS remote access |

Earlier 3.4.1, 3.1.3 and Legacy 2.2.2 releases and their tags were removed on October 18, 2026 at the owner's request. Install the current DMG above.

The Release build, JavaScript checks (including 13 slow tests and 10 real-Electron probes), and the signed DMG's hidden launcher, HTTP assets and shutdown were checked on an Apple M4 Mac running macOS 27.0.1. The final ordinary .NET run had 22,429 passes, 416 skips and two failures: an annotation-test timeout and a support-port rebind assertion. Both complete test classes passed on an isolated rerun (160 cases), without changing product timeouts. The full .NET run was not entirely green. The macOS Bash 3.2 firewall path-quoting defect found before packaging was fixed; all 31 firewall tests passed. Actual Google sign-in, public CA issuance, external HTTPS access, administrator firewall approval, paid agent calls, Docker isolation, mobile devices, macOS 26.x and installation on a second Mac were not remeasured for this DMG.

This repository was renamed from `orke-releases` on October 11, 2026. Linux downloads have their own repository.

[Homepage](https://orke.bomtobe.com) · [Support & FAQ](https://orke.bomtobe.com/support/) · [Linux server](https://github.com/bomtobe-hgkim/orke-linux) · [Windows Store](https://apps.microsoft.com/detail/9N7G0NK63QGR) · [Privacy](https://orke.bomtobe.com/privacy/) · [Contact: bomtobe.sw@gmail.com](mailto:bomtobe.sw@gmail.com)
