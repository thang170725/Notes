# Install & run .deb
```bash
1. sudo apt update
2. sudo apt install ./google.deb
```

# Cài GIMP (remove background img)
```bash
sudo apt install gimp     # Ubuntu / Debian
sudo pacman -S gimp       # Arch
sudo dnf install gimp     # Fedora
```
# Tải video
**Step**
```bash
1. sudo apt update
2. sudo apt install yt-dlp -y
3.
yt-dlp "https://www.youtube.com/watch?v=ABC123"
yt-dlp -f best "https://www.youtube.com/watch?v=ABC123"
yt-dlp -f bestaudio "https://www.youtube.com/watch?v=ABC123" -o "%(title)s.%(ext)s"
yt-dlp -x --audio-format mp3 "https://www.youtube.com/watch?v=ABC123"
yt-dlp -f best "https://www.youtube.com/playlist?list=PLxxxx"
yt-dlp -o "%(title)s.%(ext)s" "https://www.youtube.com/watch?v=ABC123"
python -m yt_dlp "https://www.youtube.com/watch?v=4ar4bwuJwLo"
echo 'alias ytd="python -m yt_dlp --merge-output-format mp4"' >> ~/.bashrc
source ~/.bashrc
4. ytd https://www.youtube.com/shorts/4ar4bwuJwLo
```
**Fix lỗi av1**
```bash
ffmpeg -i dance_korea.mp4 -c:v libx264 -c:a aac output.mp4 # thường xuất hiện trên ubuntu
```