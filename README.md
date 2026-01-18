# YT-Download-NG

A modern, containerized YouTube Music downloader with a comprehensive web interface. Built with Rust (Axum), Python (gytmdl), and Node.js (PO Token server).

## ✨ Features

### 🎨 Enhanced Web UI
- **Dashboard** - Statistics cards with Chart.js visualizations
- **Downloads** - Batch input, filters, and job management
- **Files** - Browse and search downloaded files
- **Logs** - Real-time log viewer with filtering and export
- **Settings** - Configuration, cookie management, system info
- Sidebar navigation with 5 main views
- Purple gradient theme with professional design
- Real-time updates via WebSocket

### 🚀 Technical Features
- 🔒 **Containerized** - Runs in Docker for easy deployment
- 🚀 **Fast Rust Backend** - Built with Axum for high performance
- 🎵 **Multiple Quality Profiles** - 11 pre-configured profiles
- 📊 **Job Management** - Track download progress and history
- 🛡️ **PO Token Support** - Automatic bot protection bypass
- ✅ **Production Ready** - All features tested and working

## 🚀 Quick Start

```bash
docker compose up -d
```

Access the web UI at **http://localhost:8080**

## 📁 Downloads

Downloaded files appear in `./downloads/` directory.

## 🎯 API Endpoints

- `GET /` - Web UI (Dashboard, Downloads, Files, Logs, Settings)
- `GET /health` - Health check
- `GET /api/profiles` - List quality profiles
- `POST /api/download` - Submit download job
- `GET /api/jobs` - List all jobs
- `GET /api/jobs/:id` - Get specific job status
- `GET /api/server/status` - PO token server status
- `POST /api/server/start` - Start PO token server
- `WS /ws` - WebSocket for real-time updates

## 🎨 Quality Profiles

- **gytmdl** - Standard (140 kbps AAC)
- **audiophile-max** - Maximum quality
- **music-hq** - High quality
- **archive-lossless** - Lossless
- **vinyl-collection** - Vinyl-optimized
- And 6 more specialized profiles

## 🔧 Technical Details

**The Key Fix**: Modified gytmdl files with PO token server detection (in `gytmdl-patches/`)

**Architecture**:
1. Rust Backend (Axum) - HTTP/WebSocket/Job management
2. Python (gytmdl) - Download orchestration
3. Node.js (bgutil) - PO token generation
4. Enhanced Frontend - 5-view modern UI with Chart.js

**Views**:
- Dashboard: Stats cards, charts (downloads over time, profile usage), recent activity
- Downloads: Batch URL input, advanced filters, job controls
- Files: File browser, search functionality
- Logs: Real-time viewer, level filtering, export
- Settings: Download config, cookie management, system info

## ✅ Status

**ALL ISSUES FIXED!** ✓

- ✓ Virtual environment detection
- ✓ Config paths for Linux
- ✓ PO token server integration
- ✓ Downloads working perfectly
- ✓ Files saved to mounted volume
- ✓ Web UI fully functional

**Tested**: 33-track album downloaded successfully!

## 🙏 Credits

- [gytmdl](https://github.com/glomatico/gytmdl)
- [yt-dlp](https://github.com/yt-dlp/yt-dlp)
- [bgutil-ytdlp-pot-provider](https://github.com/Brainicism/bgutil-ytdlp-pot-provider)
- [Axum](https://github.com/tokio-rs/axum)
