<div align="center">
  <img src="Assets/CaptainNet.png" width="128" alt="Captain Net icon">
  <h1>Captain Net</h1>
  <p>Local network diagnostics · LAN collaboration · Portable Windows workspace</p>
  <p><a href="README.md">中文</a> · <strong>English</strong></p>
</div>

<br>

Captain Net is a local Windows network diagnostics and LAN collaboration workspace. It brings IP, DNS, WebRTC, proxy diagnostics, network protection, cross-device keyboard and mouse, file transfer, screen broadcasting, and private LAN chat into one desktop app.

Diagnostics, chat history, device aliases, and transfer history stay on the local device by default. Nothing is uploaded. LAN features are available only to devices the user has explicitly paired.

## Who is it for?

- Users of V2rayN, Clash, mihomo, sing-box, and other proxy clients
- Anyone troubleshooting DNS leaks, WebRTC leaks, IPv6 bypasses, split routing, or real-world link speed
- Developers, remote workers, families, studios, and small offices using multiple Windows PCs
- Anyone who wants to share a keyboard, mouse, clipboard, files, screens, or printers locally

## Features

### Network diagnostics

- **Speed test**: measures real domestic and overseas download throughput separately and shows each route's actual exit IP
- **IP check**: public IPv4/IPv6, ASN, ISP, geolocation, and map marker
- **IP score**: cleanliness, VPN/proxy/Tor/hosting risk, ports, and multi-source geolocation
- **Connectivity**: handshake latency matrix for China, Japan, the US, and global sites
- **Global Ping**: latency, packet loss, jitter, and route tracing
- **DNS leak test**: system DNS, recursive resolver egress, and poisoning signals
- **WebRTC / STUN**: public mappings, local interfaces, and leak exposure
- **Service status**: cloud, developer, and AI service availability
- **AI risk checks**: Claude and ChatGPT egress and endpoint checks
- **Full report**: run every check and export a report
- **Network protection**: back up DNS/WebRTC settings, apply recommendations, and restore
- **Proxy diagnostics**: read-only inspection of processes, system proxy, ports, TUN adapters, and configuration clues
- **Hide IP**: one switch consistently masks or reveals IPs across every page

### LAN collaboration

Each collaboration area has its own entry in the left navigation. Start by discovering and pairing devices under **Borderless KB/Mouse**.

#### Borderless keyboard and mouse

- Move the pointer to a screen edge to switch to a neighboring device; any device can be the controller
- Detect multi-monitor devices automatically; every monitor is an independent layout node
- Drag the Canvas layout to sync the physical arrangement across paired devices
- Sync text, screenshots, images, and copyable file lists between paired devices
- A cursor watchdog restores the system cursor after unexpected exits or stale control sessions

#### LAN transfer

- Share files or folders by drag-and-drop or file picker
- All paired devices see the same catalog and can choose their own download directory
- Folder structure is recreated on the receiver
- Multi-file jobs expose per-file and overall progress and keep transfer history
- Interrupted transfers support resume
- Partial data lives in a hidden `.captain-partial` tree; after byte-count verification, the original path, filename, and extension are restored, including `.exe`, archives, media, and documents

#### Screen broadcast

- A dedicated **Screen Broadcast** page with per-device selection and Select All
- Broadcast invitations appear as a topmost desktop prompt on the receiving device
- The receiver must explicitly choose **Accept viewing** or **Reject**
- The broadcaster sees pending, accepted, viewing, rejected, and ended states per device
- The broadcaster can end all viewers at any time
- The receiver sees who is viewing at the top of the app and can cancel viewing with one click

#### LAN chat

- A dedicated **LAN Chat** page for two-way text conversations between paired devices
- Send files and folders of any format from the conversation
- Device aliases are local-only and do not rename the other device
- Clear one conversation at a time; clearing affects only the local device
- Chat history is stored under `%AppData%\\CaptainNet\\chat` and never uploaded

#### LAN printer

- Enable sharing on the computer connected to the printer; paired devices discover it automatically
- Submit print jobs from any paired device
- Print history stays synchronized

## Getting started

1. Download the Windows x64 portable build from [Releases](https://github.com/captainzeqi/Captain-Net-Releases/releases/latest).
2. Run the EXE directly; no installer or .NET runtime is required.
3. Start with **IP Check** or **Full Network Check**.
4. For collaboration, open **Borderless KB/Mouse**, discover devices, and complete pairing on both sides.
5. To move files, open **LAN Transfer** and share a file or folder.
6. To broadcast a screen, open **Screen Broadcast**, select devices, and wait for explicit acceptance.
7. To chat, open **LAN Chat**, select a device, and send text, files, or folders.

## Downloads and updates

- [Latest release](https://github.com/captainzeqi/Captain-Net-Releases/releases/latest)
- [All releases](https://github.com/captainzeqi/Captain-Net-Releases/releases)

Only a self-contained Windows x64 portable build is published. Captain Net checks for updates and shows a bottom-left **Restart and update now** prompt; it downloads, replaces, and relaunches the app automatically. Manual checking is also available in Settings.

For keyboard/mouse, clipboard, file transfer, screen broadcast, and chat interoperability, keep paired devices on the same version.

## Privacy and security boundaries

- Diagnostics, chat history, device aliases, and transfer history are stored under `%AppData%\\CaptainNet` on the local device.
- Captain Net does not upload reports. Internet access is used only for network checks and update checks.
- LAN features are available only to explicitly paired devices, and pairing requires confirmation.
- Received paths reject drive prefixes, `..`, and invalid filename characters so peers cannot write outside the selected directory.
- Files are written to a hidden partial tree and only promoted to the original filename after a complete-length check.
- LAN collaboration is intended for trusted networks. For production use, add TLS pairing, granular permissions, and code signing.

## Network ports

- UDP `45678`: device discovery and heartbeat
- TCP `45679`: collaboration control, files, and chat messages
- UDP `45679`: low-latency mouse and keyboard input
- TCP `45680`: screen viewing and broadcast stream

If Windows Firewall blocks discovery, allow Captain Net on private networks.

## Development

Requires the .NET 8 SDK:

```powershell
dotnet build -c Debug
dotnet publish NetCoffee.csproj -c Release -r win-x64 --self-contained true /p:PublishSingleFile=true
```

Pushing a `v*` tag triggers `.github/workflows/release.yml`, which builds the portable Windows asset and publishes it to this source repository and the public [Captain-Net-Releases](https://github.com/captainzeqi/Captain-Net-Releases) repository. The in-app updater reads only the public release repository, so the source repository can remain private.
