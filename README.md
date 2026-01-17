# YouTube Music Downloader NG - Web Edition

🎵 **Containerized YouTube Music Downloader with Modern Web UI**

A beautiful, self-hosted web application for downloading music from YouTube Music with audiophile-grade quality profiles. Built with Rust (Axum) backend and modern web technologies.

## ✨ Features

- **🎨 Modern Web UI**: Beautiful gradient design with real-time updates
- **🐳 Fully Containerized**: Run anywhere with Docker
- **⚡ Rust-Powered**: Lightning-fast web backend built with Axum
- **🔄 Real-time Updates**: WebSocket-based live progress tracking
- **🎯 11 Quality Profiles**: From audiobook to audiophile-max
- **📦 Self-Contained**: Everything in one container
- **🔒 Secure**: Runs as non-root user
- **💾 Persistent Storage**: Volume mounts for downloads and configs

## 🚀 Quick Start

### Using Docker Compose (Recommended)

```bash
# Clone the repository
git clone <your-repo-url>
cd ytdl-web

# Start the application
docker-compose up -d

# Access the web UI
open http://localhost:8080
```

### Using Docker CLI

```bash
# Build the image
docker build -t ytdl-web .

# Run the container
docker run -d \
  -p 8080:8080 \
  -p 4416:4416 \
  -v $(pwd)/downloads:/data/downloads \
  -v $(pwd)/config:/data/config \
  --name ytdl-web \
  ytdl-web

# View logs
docker logs -f ytdl-web
```

## 📖 Usage

### Web Interface

1. Open your browser to `http://localhost:8080`
2. Enter a YouTube Music URL
3. Select a quality profile
4. Click "Start Download"
5. Monitor progress in real-time!

### API Endpoints

#### Health Check
```bash
curl http://localhost:8080/health
```

#### List Profiles
```bash
curl http://localhost:8080/api/profiles
```

#### Start Download
```bash
curl -X POST http://localhost:8080/api/download \
  -H "Content-Type: application/json" \
  -d '{"url": "https://music.youtube.com/playlist?list=...","profile": "profiles/audiophile-max"}'
```

#### List Jobs
```bash
curl http://localhost:8080/api/jobs
```

#### Get Job Status
```bash
curl http://localhost:8080/api/jobs/{job-id}
```

#### Server Status
```bash
curl http://localhost:8080/api/server/status
```

### WebSocket
Connect to `ws://localhost:8080/ws` for real-time job updates.

## 🎵 Quality Profiles

| Profile | Format | Bitrate | Cover Size | Best For |
|---------|--------|---------|------------|----------|
| **gytmdl** | AAC | 128 kbps | 1200px PNG | General use |
| **profiles/audiobook** | AAC | 128 kbps | 1200px PNG | Audiobooks/Podcasts |
| **profiles/music-hq** | Opus | 135 kbps | 1200px PNG | Standard music |
| **profiles/audiophile-max** | Opus | 135 kbps | 1400px PNG | Maximum quality |
| **profiles/critical-listening** | Opus | 135 kbps | 1200px PNG | Pure audio focus |
| **profiles/archive-lossless** | Opus | 135 kbps | 1400px PNG | Long-term preservation |
| **profiles/vinyl-collection** | Opus | 135 kbps | 1400px PNG | Album collectors |
| **profiles/classical** | Opus | 135 kbps | 1200px PNG | Classical music |
| **profiles/live-recordings** | Opus | 135 kbps | 1200px PNG | Concert recordings |
| **profiles/mobile-optimized** | AAC | 128 kbps | 800px JPG | Portable devices |
| **profiles/reference-testing** | Opus | 135 kbps | 1400px PNG | A/B testing |

## 🏗️ Architecture

```
┌─────────────────────────────────────────────┐
│          Web UI (Embedded HTML)             │
│  Beautiful gradient design with real-time   │
│         WebSocket updates                   │
└─────────────────┬───────────────────────────┘
                  │
┌─────────────────▼───────────────────────────┐
│       Rust Web Backend (Axum)               │
│  • REST API endpoints                       │
│  • WebSocket server                         │
│  • Job management                           │
│  • Process orchestration                    │
└─────────────────┬───────────────────────────┘
                  │
        ┌─────────┴──────────┐
        │                    │
┌───────▼────────┐  ┌────────▼──────────┐
│  Python Script │  │  Node.js Server   │
│    (ytdl.py)   │  │  (PO Token)       │
│  • Downloads   │  │  • Token gen      │
│  • Profiles    │  │  • Port 4416      │
└────────────────┘  └───────────────────┘
```

## 🔧 Configuration

### Environment Variables

- `YTDL_PORT`: Web UI port (default: 8080)
- `YTDL_DATA_DIR`: Data directory path (default: /data)
- `RUST_LOG`: Logging level (default: info)

### Volume Mounts

- `/data/downloads`: Downloaded files
- `/data/config`: Configuration files and cookies
- `/data/cache`: yt-dlp cache
- `/data/logs`: Application logs

## 🐛 Troubleshooting

### Container won't start
```bash
# Check logs
docker logs ytdl-web

# Verify ports are available
lsof -i :8080
lsof -i :4416
```

### Downloads fail
1. Check cookies file: `config/cookies.txt`
2. Export fresh cookies from browser
3. Restart container: `docker-compose restart`

### PO Token Server issues
```bash
# Check server status via API
curl http://localhost:8080/api/server/status

# Start server manually
curl -X POST http://localhost:8080/api/server/start
```

## 🔄 Updates

```bash
# Pull latest changes
git pull

# Rebuild and restart
docker-compose down
docker-compose build --no-cache
docker-compose up -d
```

## 📊 Performance

- **Container Size**: ~500MB (optimized multi-stage build)
- **Memory Usage**: ~200-300MB idle, ~500MB-1GB during downloads
- **CPU Usage**: Minimal when idle, variable during downloads
- **Download Speed**: Limited by aria2c/gytmdl, typically 2-5MB/s

## 🛠️ Development

### Local Development

```bash
# Install Rust
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

# Build backend
cd web-backend
cargo build

# Run backend
cargo run

# Access UI at http://localhost:8080
```

### Testing

```bash
# Test Python script
python ytdl.py check

# Test API
curl http://localhost:8080/health
```

## 📝 License

See LICENSE file for details.

## 🙏 Credits

- **gytmdl**: Core download functionality
- **yt-dlp**: Video/audio extraction
- **Axum**: Rust web framework
- **bgutil-ytdlp-pot-provider**: PO token generation

## 🚀 Future Enhancements

- [ ] Multi-user support with authentication
- [ ] Download queue management
- [ ] Scheduled downloads
- [ ] Download history and statistics
- [ ] Custom profile editor
- [ ] Batch URL import from clipboard
- [ ] Mobile app
- [ ] Dark/light theme toggle
- [ ] Download notifications
- [ ] Integration with Plex/Jellyfin

## 📧 Support

For issues, questions, or contributions, please open an issue on GitHub.

---

**Made with ❤️ and Rust** 🦀
