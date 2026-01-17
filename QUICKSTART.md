# 🚀 Quick Start Guide

Get up and running with YouTube Music Downloader NG - Web Edition in 5 minutes!

## Prerequisites

- **Docker**: [Install Docker](https://docs.docker.com/get-docker/)
- **Docker Compose**: Usually included with Docker Desktop
- **YouTube Cookies**: Export from your browser (see below)

## Step 1: Get Cookies

1. Install browser extension: "Get cookies.txt LOCALLY" ([Chrome](https://chrome.google.com/webstore/detail/get-cookiestxt/bgaddhkoddajcdgocldbbfleckgcbcid) / [Firefox](https://addons.mozilla.org/en-US/firefox/addon/cookies-txt/))
2. Go to [music.youtube.com](https://music.youtube.com)
3. Click the extension icon
4. Click "Export" → Save as `cookies.txt`
5. Move `cookies.txt` to `config/cookies.txt` in this project

## Step 2: Start the Container

```bash
# Clone this repository (if you haven't)
cd C:\Users\TiHa\.git\ytdl-web

# Start with Docker Compose
docker-compose up -d

# Or build and run manually
docker build -t ytdl-web .
docker run -d -p 8080:8080 -p 4416:4416 --name ytdl-web ytdl-web
```

## Step 3: Access the Web UI

Open your browser to: **http://localhost:8080**

You should see a beautiful purple gradient interface! 🎨

## Step 4: Download Your First Album

1. Go to [YouTube Music](https://music.youtube.com)
2. Find an album or playlist
3. Copy the URL (should look like: `https://music.youtube.com/playlist?list=...`)
4. Paste into the Web UI
5. Select a quality profile (try "profiles/audiophile-max" for best quality)
6. Click "Start Download"
7. Watch the magic happen! ✨

## 🎵 Example URLs to Try

```
# Albums
https://music.youtube.com/playlist?list=OLAK5uy_lV2bH0OHkf8eX_J03qt_z2axGlP1INVlw

# Playlists
https://music.youtube.com/playlist?list=PLrEnWoR732-BHrPp_Pm8_VleD68f9s14-
```

## 📦 Where Are My Downloads?

Downloads are saved to: `./downloads/` in your project directory

They're organized by profile:
- `downloads/` - Default profile
- `downloads/Music/Audiophile/` - Audiophile-max profile
- `downloads/Audiobooks/` - Audiobook profile
- etc.

## 🔧 Common Commands

```bash
# View logs
docker logs -f ytdl-web

# Stop container
docker-compose down

# Restart container
docker-compose restart

# Rebuild after changes
docker-compose down
docker-compose build --no-cache
docker-compose up -d
```

## ⚡ Quick Tips

1. **Best Quality**: Use `profiles/audiophile-max` (Opus 135kbps, 1400px PNG covers)
2. **Fast Downloads**: The container uses the optimized downloader (no aria2c issues!)
3. **Real-time Updates**: The WebSocket connection shows live progress
4. **Multiple Downloads**: You can queue multiple downloads at once
5. **Cookies Expire**: If downloads fail, update your `cookies.txt`

## 🐛 Troubleshooting

### "Cannot connect to localhost:8080"
```bash
# Check if container is running
docker ps

# Check logs
docker logs ytdl-web

# Try restarting
docker-compose restart
```

### "Downloads fail immediately"
- Update your `cookies.txt` (they expire!)
- Make sure you're logged into YouTube Music
- Check the logs: `docker logs ytdl-web`

### "Port 8080 already in use"
Edit `docker-compose.yml` and change `"8080:8080"` to `"9090:8080"` (or any free port)

## 🎨 What Makes This Special?

- **Beautiful UI**: Modern gradient design, not a boring terminal
- **Real-time**: See progress updates live via WebSocket
- **Container-based**: No messy installs, just `docker-compose up`
- **Rust-powered**: Lightning-fast web backend
- **Auto-fixes**: Automatically handles aria2c and config issues
- **Production-ready**: Health checks, logging, proper error handling

## 🚀 Next Steps

1. ✅ Download your first album
2. 📊 Try different quality profiles
3. 🔄 Use the API (see README.md)
4. 🎯 Set up automatic downloads
5. 📱 Access from your phone (use your computer's IP instead of localhost)

## 💡 Pro Tips

**Batch Download Multiple Albums:**
1. Create a file `urls.txt` with one URL per line
2. Copy it into the container: `docker cp urls.txt ytdl-web:/app/`
3. Run: `docker exec ytdl-web python ytdl.py batch /app/urls.txt -p profiles/audiophile-max`

**Access from Another Device:**
Replace `localhost` with your computer's IP address:
- Windows: Run `ipconfig` and look for "IPv4 Address"
- Example: `http://192.168.1.100:8080`

**Monitor System Resources:**
```bash
docker stats ytdl-web
```

---

## 🎉 You're Ready!

Enjoy your new containerized music downloader with a beautiful web UI!

Need help? Check the full [README.md](README.md) or open an issue.

**Happy Downloading!** 🎵
