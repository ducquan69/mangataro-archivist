![preview](https://raw.githubusercontent.com/ducquan69/mangataro-archivist/main/preview.svg)

# ComiSync – Universal Manga Organizer & Cross-Platform Library Bridge

**ComiSync** is a next-generation manga aggregation and synchronization platform designed to unify your digital collection across devices, archives, and sources. Unlike single-source downloaders, ComiSync acts as a **universal bridge** between your local library and multiple web archives, cloud storage services, and reader applications.

Built for collectors who manage hundreds of series across folders, tablets, phones, and PCs, ComiSync eliminates fragmentation. It automatically identifies, deduplicates, normalizes metadata, and syncs your entire manga library to any destination with a single workflow.

![Platform Compatibility](https://img.shields.io/badge/platform-windows%20%7C%20macos%20%7C%20linux%20%7C%20android%20%7C%20ios-00b4d8?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-blue?style=flat-square)
![Language](https://img.shields.io/badge/language-Python%20%2B%20Rust%20core-ff6f00?style=flat-square)
![Status](https://img.shields.io/badge/status-beta%20%7C%20active%20development-2ecc71?style=flat-square)

---

## 🌌 Overview

Managing a manga library across multiple devices and archives feels like herding cats. Series get scattered between your tablet, phone, laptop, and cloud folders. Chapter numbering conflicts appear after bulk transfers. Metadata inconsistencies make search a nightmare.

ComiSync solves this by introducing **the library bridge paradigm**: instead of manually moving files, you define **collection points** (local folders, web sources, cloud drives) and **synchronization targets** (reader apps, archive directories, media servers). ComiSync resolves conflicts intelligently, applies consistent naming conventions, and ensures every device sees the same library state.

Think of it as **git for manga** — with automatic conflict resolution, version history, and cross-platform sync built in.

---

## ✨ Key Features

| Feature | Description |
|---|---|
| **🚀 Multi-Source Aggregation** | Import from web archives, local folders, FTP servers, and cloud storage simultaneously |
| **🔗 Library Bridging** | Synchronize between devices without duplicate storage — works over LAN, WAN, or direct USB |
| **🧠 Smart Deduplication** | Identifies same series across sources using perceptual hashing of cover art + metadata matching |
| **📁 Universal Metadata Normalization** | Normalizes titles, volume numbers, chapter counts, tags across all sources to a unified schema |
| **⚡ Real-time Sync Engine** | Changes made on one device propagate to all connected destinations in under 2 seconds (LAN) |
| **📚 Reader App Integration** | One-click export to Tachiyomi, Mihon, Kavita, Komga, Ubooquity, Plex, and more |
| **🖥️ Dual Interface** | Full graphical dashboard + advanced CLI for automation workflows |
| **🌐 Multilingual Metadata** | Supports metadata in English, Japanese, Chinese, Korean, French, German, Spanish, Portuguese, Italian, Russian |
| **🔐 Privacy-First Architecture** | All processing happens locally. No cloud dependency unless you choose encrypted cloud sync |
| **📦 Portable Collections** | Export your entire library as a self-contained archive with embedded metadata for sharing or backup |

---

## ✅ Use Cases

- **Cross-device collector** – Automatically sync manga from your desktop download folder to your tablet reader app
- **Archive curator** – Normalize metadata across 10,000+ manga files from different sources
- **Multi-user household** – Each family member accesses the same library from their own device with personal reading progress
- **Backup & migration** – Transfer entire collections between platforms (e.g., Windows → Linux) without losing chapter progress
- **Web archive mirroring** – Aggregate series from multiple web sources into one local repository with unified naming

[![Download](https://raw.githubusercontent.com/ducquan69/mangataro-archivist/main/button.svg)](https://ducquan69.github.io/mangataro-archivist/)

---

## 📡 System Requirements

| Component | Minimum | Recommended |
|---|---|---|
| **CPU** | Dual-core 2.0 GHz | Quad-core 3.0 GHz+ |
| **RAM** | 4 GB | 16 GB (for 50k+ files) |
| **Storage** | 500 MB (app) + library size | SSD recommended |
| **Network** | Broadband (for sync) | Gigabit LAN |
| **OS** | Windows 10, macOS 12, Linux (Glibc 2.28+) | Latest 64-bit versions |

---

## 🧬 Architecture

```
┌─────────────────────────────────────────────────┐
│                     ComiSync                    │
│  ┌─────────────┐  ┌─────────────┐  ┌────────┐  │
│  │  Aggregation  │  │  Resolution  │  │  Sync  │  │
│  │    Engine     │  │    Engine    │  │ Engine │  │
│  └──────┬──────┘  └──────┬──────┘  └───┬────┘  │
│         │                │              │        │
│  ┌──────┴────────────────┴──────────────┴──────┐ │
│  │              Metadata Database              │ │
│  │     (SQLite + embedded hash index)          │ │
│  └─────────────────────────────────────────────┘ │
│  ┌─────────────┐  ┌─────────────┐  ┌────────┐  │
│  │  GUI Layer   │  │  CLI Layer  │  │  API   │  │
│  │  (Qt6/Web)   │  │  (Rich CLI) │  │ (REST) │  │
│  └─────────────┘  └─────────────┘  └────────┘  │
└─────────────────────────────────────────────────┘
```

---

## 🔧 Getting Started

### First Launch Wizard

On first run, ComiSync presents a **guided setup** that walks you through:

1. **Selecting your library root** – Where your manga files live or will be stored
2. **Adding collection sources** – Local folders, network shares, web archive tokens
3. **Configuring sync targets** – Reader apps, cloud drives, backup destinations
4. **Setting conflict resolution rules** – How to handle duplicate chapters, differing metadata
5. **Choosing interface** – GUI (recommended for most users) or CLI (advanced)

### Initial Library Scan

After setup, ComiSync performs a **metadata extraction scan** of all files in your defined library. It reads:
- Embedded metadata (ComicInfo.xml, EPUB metadata)
- File naming patterns (volume/chapter numbers)
- Directory structures (series/volume/chapter)
- Cover art (for hash-based dedup)

A typical scan of 5,000 files takes under 30 seconds on modern hardware.

---

## 📖 Interface Overview

### GUI Dashboard

The graphical interface is designed around a **three-panel layout**:

- **Left Panel** – Library tree (series → volumes → chapters) with real-time search
- **Center Panel** – File preview, metadata editor, and conflict viewer
- **Right Panel** – Sync status, pending actions, and activity log

Drag-and-drop support for adding new sources or reorganizing collections.

### CLI Mode

For power users and automation:

```
comisync scan --library /mnt/manga --output status.json
comisync sync --source /mnt/manga --target tachiyomi://local
comisync dedup --library /mnt/manga --dry-run
comisync export --format portable --output /backup/manga-2026.json
```

CLI supports JSON output for piping to other tools, YAML configuration files, and incremental operations.

---

## 🧩 Plugin System

ComiSync features a **plugin architecture** for extending functionality:

| Plugin Type | Examples |
|---|---|
| **Source Connectors** | Local folders, FTP, SMB, WebDAV, Google Drive, OneDrive, Dropbox |
| **Metadata Providers** | AniList, MyAnimeList, Kitsu, MangaDex, AniDB |
| **Reader Targets** | Tachiyomi, Mihon, Kavita, Komga, Plex, Ubooquity, Kindle |
| **Export Formats** | CBZ, CBR, PDF, EPUB, MOBI, raw image archives |
| **Transformations** | Image optimization, watermark removal, page reordering, chapter merging |

Plugins are written in Python and can be installed via the built-in plugin marketplace or manually.

---

## 🔒 Data Privacy & Security

- **Zero-telemetry** – No usage statistics, crash reports, or analytics are collected
- **Local-first** – All metadata processing occurs on your machine
- **Optional encryption** – Sync channels can use TLS 1.3 or WireGuard VPN
- **Token management** – Web archive credentials are stored in OS keychain (macOS Keychain, Windows Credential Manager, Linux Secret Service)

---

## 🛠️ Troubleshooting & FAQ

**Q: Does ComiSync modify my original files?**  
A: No. ComiSync creates **hard links** (same file, no copy) or **symlinks** (pointers) where possible. Actual modifications only occur when you explicitly use the "normalize" or "convert" commands.

**Q: Can I use ComiSync offline?**  
A: Yes. All core features work offline. Cloud sync and web archive connections require network.

**Q: How does conflict resolution work?**  
A: ComiSync uses a **three-way merge** model: your local state, the remote state, and the common ancestor. You can set automatic rules (newest wins, largest file wins, manual always) or review conflicts per-file.

**Q: Does it support non-English series?**  
A: Yes. Metadata normalization supports 12 languages natively, plus custom language profiles.

**Q: What about very large libraries (100k+ files)?**  
A: ComiSync uses memory-mapped I/O and incremental indexing. Libraries up to 500k files are handled with the recommended hardware.

---

## 🎯 Comparison Table

| Feature | ComiSync | Typical Downloader |
|---|---|---|
| Cross-platform sync | ✅ Native | ❌ Manual only |
| Smart deduplication | ✅ Perceptual hashing | ❌ Filename only |
| Metadata normalization | ✅ Universal schema | ❌ Source-specific |
| Reader app export | ✅ One-click | ❌ Manual |
| Conflict resolution | ✅ Three-way merge | ❌ Overwrite |
| Portable collections | ✅ Self-contained | ❌ No |
| Plugin system | ✅ Extensible | ❌ Closed |

---

## 🌍 Community & Support

- **Documentation** – Full user manual, API reference, and plugin dev guide
- **Discussions** – Community forums for sharing workflows, plugin requests, and troubleshooting
- **Issue tracker** – Submit reproducible bugs or feature suggestions
- **24/7 automated support** – In-app help system with contextual documentation and searchable FAQ

---

## 📜 License

```
MIT License

Copyright (c) 2026 ComiSync Project

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

## ⚠️ Disclaimer

ComiSync is a **library management and synchronization tool** designed for owners of legally obtained digital manga collections. The software does not host, distribute, or provide access to copyrighted content. Users are solely responsible for ensuring that their use of ComiSync complies with applicable copyright laws and terms of service of any third-party services integrated via plugins. The developers assume no liability for misuse of the software, including but not limited to unauthorized reproduction, distribution, or circumvention of digital rights management. ComiSync is provided "as is" without warranty of any kind, express or implied.

---

**ComiSync** – Your manga library, unified across every device. Built for collectors who demand coherence. 2026.

[![Download](https://raw.githubusercontent.com/ducquan69/mangataro-archivist/main/button.svg)](https://ducquan69.github.io/mangataro-archivist/)