# ClaudePlayer Installation Guide

## Quick Start (Windows Installer)

1. Download `ClaudePlayer-1.0.0.0-win64.msi` from the releases page
2. Double-click the installer
3. Follow the installation wizard
4. Click "Finish" to complete installation
5. Launch ClaudePlayer from:
   - **Start Menu** → "ClaudePlayer" → "Prism Media Player"
   - **Desktop** shortcut (if selected during installation)
   - **Programs** folder in Windows

## System Requirements

- **OS**: Windows 10 or later (64-bit)
- **RAM**: 2 GB minimum (4 GB recommended)
- **Disk Space**: 500 MB for installation
- **Display**: 1280×720 resolution or higher

## Installation Options

### Option 1: Standard Installation
- Installs to: `C:\Program Files\ClaudePlayer`
- Creates Start Menu shortcuts
- Creates Desktop shortcut

### Option 2: Custom Installation
During the installer wizard, you can:
- Choose installation directory
- Select which shortcuts to create
- Choose installation folder

## Supported Media Formats

### Audio
- MP3, WAV, FLAC, AAC, OGG, M4A

### Video
- MP4, MKV, AVI, MOV, WMV, FLV

### Subtitles
- SRT, ASS, SSA, VTT

## First Run

1. Open ClaudePlayer
2. Click **"Open File"** to browse for media
3. Select a media file and click **Open**
4. Use the playback controls to play/pause/stop

## Troubleshooting

### "Application won't start"
1. Uninstall ClaudePlayer
2. Restart your computer
3. Reinstall from scratch

### "Missing audio/video codecs"
- Windows 10 includes most common codecs
- For additional formats, install K-Lite Codec Pack

### "Slow playback"
- Close other applications
- Verify your graphics drivers are updated
- Try a different media file

### "Uninstall Issues"
1. Press `Win + R`
2. Type `appwiz.cpl` and press Enter
3. Find "ClaudePlayer" in the list
4. Click and select **Uninstall**
5. Follow the uninstall wizard

## Updating to New Versions

1. Download the new installer
2. Run the installer - it will automatically upgrade
3. All settings are preserved during upgrade

## Building from Source

See [README.md](README.md) for complete build instructions.

## Support

For help, visit: https://github.com/061025koki-debug/ClaudePlayer/issues

## License

See LICENSE file in the installation directory.
