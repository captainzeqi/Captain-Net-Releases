<div align="center">
  <img src="Assets/CaptainNet.png" width="128" alt="Captain Net icon">
  <h1>Captain Net</h1>
  <p>Desktop network diagnostics and LAN collaboration workspace</p>
  <p><a href="README.md">中文</a> · <strong>English</strong></p>
</div>

<br>

Captain Net is a desktop network diagnostics and local network collaboration tool for Windows users. It brings IP, DNS, WebRTC, proxy, network protection, multi-device collaboration, and printer sharing into one workspace.

## Who is it for?

- Users of V2rayN, Clash, mihomo, sing-box, and other proxy clients
- Users troubleshooting DNS leaks, WebRTC leaks, IPv6 bypasses, or routing issues
- Developers, remote workers, and users who need connectivity checks across regions
- Families, studios, and small offices using multiple computers
- Users who want to share clipboard content, files, layouts, or printers locally

## Features

### Network diagnostics

- **Speed test**: measures download throughput for the domestic and overseas routes separately, each showing the exit IP that route actually uses
- **IP check**: public IP, ASN, ISP, location, and offline map marker
- **IP score**: cleanliness, risk, proxy signals, ports, and multi-source geolocation
- **Connectivity**: latency matrix for China, Japan, the US, and global sites
- **Global Ping**: latency, packet loss, jitter, and traceroute
- **DNS leak test**: system DNS, recursive resolver egress, and quick/deep checks
- **WebRTC / STUN**: public mappings, local interfaces, and leak exposure
- **Service status**: cloud, developer, and AI service availability
- **AI risk checks**: Claude and ChatGPT egress and endpoint availability
- **Full report**: run all checks and export a report

### Network protection

- Inspect adapter DNS settings and Chromium WebRTC policy
- Back up the original configuration before changes
- Apply recommended protection settings with one click
- Restore the exact previous configuration
- Hide IP addresses in screenshots and recordings

### Proxy diagnostics

- Detect V2rayN, Clash, mihomo, sing-box, and related processes
- Inspect system proxy settings, ports, TUN adapters, and runtime signals
- Search common configuration directories and portable installations
- Perform an administrator deep scan of process paths and command-line parameters
- Read-only diagnostics; proxy configuration is never changed automatically

### Borderless keyboard and mouse

- One keyboard and mouse drive every paired device; any device can be the controller, with no "primary device" to configure
- Move the pointer to a screen edge to switch devices; the keyboard follows the active device
- Multi-monitor devices are detected automatically, and each monitor is its own node in the layout
- Grid-based device layout syncs to every device on drag, and never overlaps no matter how many devices join
- Only the active device shows a cursor; the others hide theirs automatically
- Held modifiers are released on the remote when control leaves, so Ctrl never sticks down
- Cursor visibility is guarded by its own watchdog: outside an active cross-device session the cursor is restored within one second, a crashed run is repaired on next startup, and "Restore mouse cursor" is available in both the settings page and the tray menu

### LAN printer

- Enable sharing on the machine physically connected to the printer; other devices pick it up automatically
- Upload a file and submit a print job from any device
- Print history stays in sync across devices

### LAN transfer

- Share files or folders by drag-and-drop or file picker
- Every paired device sees the same combined catalog
- Any device can download to a directory it picks; folder structure is recreated on the receiver
- Sharing publishes only a manifest — bytes move on demand, and files stay on the device that published them

### Clipboard sync

- Text clipboard content syncs automatically between paired devices
- Screenshots and copied images sync too, transferred losslessly as PNG and offered as both bitmap and PNG so Paint, Office and browsers can all paste them
- Copy files on one device and press Ctrl+V on another; oversized transfers ask first
- Syncing is driven by the system clipboard sequence number, and both reads and writes retry, so a brief lock by an IME or another app no longer drops a sync

### Application behaviour

- Closing the window keeps the app running in the system tray; restore from the tray icon, quit from its menu
- Checks for new versions on startup and raises a bottom-left prompt; "Restart and update now" downloads, replaces and relaunches the app in one click
- Updates jump straight to the newest release, download next to the running executable, and remove the previous one once the swap succeeds

LAN discovery uses UDP `45678`; collaboration transfers use TCP `45679`, while low-latency mouse/keyboard input uses UDP `45679`. If Windows Firewall blocks discovery, allow Captain Net to access the local network.

## Getting started

1. Download the package for your operating system from Releases and extract it.
2. Launch Captain Net and run **IP Lookup** or **Full Network Check**.
3. Open **Network Protection** to review backups before applying a recommendation.
4. Open **Proxy Diagnostics** and use **Administrator Deep Scan** when needed.
5. For multi-device work, open **Borderless KB/Mouse**, pair the other devices, arrange the layout to match how the screens physically sit, then enable sharing.
6. On the computer connected to a printer, enable sharing under **LAN Printer**; other devices can then submit print jobs.
7. To move files, open **LAN Transfer**, drop in files or folders, and download them from any device to a path you choose.

## Downloads

- [Latest release](https://github.com/captainzeqi/Captain-Net-Releases/releases/latest)
- [All Releases](https://github.com/captainzeqi/Captain-Net-Releases/releases)

Only a self-contained Windows x64 portable build is published: download the versioned `.exe` and run it, with no installation and no .NET runtime required.

After the first install you do not need to come back here — the app checks for new versions and shows a bottom-left prompt; "Restart and update now" downloads, replaces and relaunches it. The settings page can also check manually.

All devices must run the same version to share keyboard, mouse, clipboard and files.

## Privacy and security

- Results are stored locally under `%AppData%\\CaptainNet` on Windows.
- Captain Net does not upload reports and does not depend on the original reference website.
- Administrator privileges are requested only for explicit actions such as deep proxy scans, network protection changes, and printer sharing.
- LAN features are available only to **paired** devices, and pairing requires confirmation.
- Relative paths in received shares are sanitised, so a peer cannot write outside the directory you chose.
- Use LAN collaboration only on trusted networks. Production deployment should add TLS pairing, input-control permissions, and code signing.

## Development

### Windows

Requires the .NET 8 SDK:

```powershell
dotnet build -c Debug
dotnet publish NetCoffee.csproj -c Release -r win-x64 --self-contained true /p:PublishSingleFile=true
```

Pushing a `v*` tag triggers `.github/workflows/release.yml`, which builds the portable Windows asset and publishes it both here and to the public release repository [`Captain-Net-Releases`](https://github.com/captainzeqi/Captain-Net-Releases). The in-app updater reads only the public release repository, so this source repository can be private.

Publishing to the public repository requires a `RELEASE_REPO_TOKEN` secret with Contents write access to it; the step is skipped when the secret is absent.
