# lidarr-youtube-downloader

Look for missing tracks in your lidarr library and download them from youtube.

# Docker Usage

### build and run locally
```
docker build -t yls .
# you need to be careful that the path matches the path that lidarr knows (use the same external:internal references)
docker run \
   -v /path/to/music:/path/to/music \
   -v /path/to/db/file:/path/to/db/file \   
   -e LIDARR_URL="http://YOUR-HOST-IP:8686" \
   -e LIDARR_API_KEY="YOUR-LIDARR-API-KEY" \
   -e LIDARR_DB="/path/to/lidarr/lidarr.db" \
   -e LIDARR_MUSIC_PATH="/music" \
   --name yls yls
```

### via docker-compose (only for arm64 for now)
```
version: "3"
services:
lidarr-youtube:
    image: chalomadek/yls
    container_name: lidarr-youtube
    environment:
      - LIDARR_URL=http://YOUR-HOST-IP:8686
      - LIDARR_API_KEY=YOUR-LIDARR-API-KEY
      - LIDARR_DB=/path/to/lidarr/lidarr.db
      - LIDARR_MUSIC_PATH=/music
    volumes:
      - /path/to/music:/path/to/music
      - /path/to/db/file:/path/to/db/file
    restart: unless-stopped
```

# Local Usage

### Requirements
```
dnf/apt install ffmpeg
sudo curl https://youtube-dl.org/downloads/latest/youtube-dl -o /usr/bin/youtube-dl
chmod +x /usr/bin/youtube-dl
pip3 install eyed3 youtube-search-python
```

### Config
```
export LIDARR_URL="http://127.0.0.1:8686"
export LIDARR_API_KEY="771de60596e946f6b3e5e6f5fb6fd729" # your key
export LIDARR_DB="/path/to/lidarr/lidarr.db"
export LIDARR_MUSIC_PATH="/music"
```

### Usage
```
python3 lidarr-youtube-downloader.py
```

