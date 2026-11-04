# AI Coding Workspace for Android

An open, full-featured AI coding environment for Android: Antigravity and Claude Code agent protocols, integrated Linux terminal (Termux), code editor, and agent-controllable web browser.

---

## 🔒 100% Private & Clean (Zero Fishy Elements)

This codebase has been cleaned and de-branded from the upstream repository:
- **Zero Telemetry / Analytics**: The `TelemetryDeck` SDK, providers, and analytics hooks have been completely removed. No tracking IDs, no install hashes, and no network pinging on app start.
- **No Signature Checks / Build Locks**: Removed artificial signature verification checks (`isOfficialRelease` / `RELEASE_CERT_SHA256`) that previously warned users with "Unofficial build" toasts.
- **No Hardcoded Third-Party Author Links**: Removed external personal repository endpoints, social media, and WhatsApp community links.
- **Secure Official Rootfs Resolution**: Terminal rootfs setup resolves verified packages directly from official repositories (`termux/termux-packages` / `termux/proot-distro`), with full support for custom or offline zip archives.
- **Configurable / Safe Updates**: Background auto-download of third-party release APKs has been disabled so upstream changes can never overwrite your custom application.

---

## 🚀 Key Features

### 1. Dual Agent Support
- **Antigravity (`agy`)**: Direct gRPC connection to the `agy` language server and daemon.
- **Claude Code**: Stream-JSON protocol relay running the official `claude` CLI inside the local Linux environment.
- Real-time streaming tokens, collapsible thinking blocks, inline diff previews, tool approvals, and multi-choice interactive questions.

### 2. Integrated Termux Linux Subsystem
- Full terminal emulator backed by Termux's open-source terminal view libraries.
- Package manager (`apt` / `pkg`) with Python, Node.js, Git, Go, Rust, and C/C++.
- Built-in `termux-*` native bridge commands for clipboard, notifications, and device hardware.
- ADB over Wireless Debugging with automatic re-pairing.

### 3. Integrated IDE & Browser
- Syntax highlighting across multiple programming languages.
- File explorer, tabbed editor, search and replace, Git commit/push/diff UI.
- In-app Chromium WebView with developer console (Eruda) and DOM automation MCP.

### 4. Built-in MCP Servers
- **Browser MCP**: DOM inspection, screenshot capture, automated interaction.
- **Terminal MCP**: Process spawning, command execution, stream capture.
- **Android MCP**: Device UI automation, accessibility gestures, app launching.
- **Notes MCP**: Persistent note storage and scratchpad.

---

## 🛠️ Building the APK

### Prerequisites
- **JDK 17+** (Installed at system level)
- **Android SDK** (API 35/36 with build-tools)
- **Go 1.22+** (Optional: a pre-compiled ARM64 `agy_ide_bridge` binary is already included in `app/src/main/assets/bin/`)

### Build Commands

```powershell
# Navigate to the project root
cd C:\Users\BIKASH\.gemini\antigravity\scratch\open-antigem

# Build Termux-compatible Debug APK (com.termux package name for native path execution)
.\gradlew.bat assembleTermuxDebug

# Build Standard Debug APK (com.antigem package name)
.\gradlew.bat assembleStandardDebug

# Build Release APK
.\gradlew.bat assembleTermuxRelease
```

Built APKs will be located at:
`app/build/outputs/apk/termux/debug/antiGem-termux-debug.apk`

---

## 📁 Project Architecture

```text
open-antigem/
├── app/src/main/
│   ├── java/com/example/gemini/
│   │   ├── data/          # Agent relays (agy gRPC, claude stream-json), ADB, terminal, automation
│   │   ├── domain/        # Protocols, chat models, parsing
│   │   └── ui/            # Jetpack Compose UI (Chat, IDE editor, Browser, Settings)
│   ├── java/com/termux/   # Termux TerminalView & background execution service
│   └── assets/            # Embedded binaries (agy_ide_bridge) and browser extension runtime
├── agy_ide_bridge/        # Go bridge relaying agent sessions to local terminal processes
├── extensions/            # Bundled agent extensions and skills
├── proto_generator/       # Protobuf schema definitions for Antigravity RPC
└── scripts/               # Backup and restore utilities
```
