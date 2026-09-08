# ClaudePlayer Quick Reference

## Build Commands

```powershell
# Basic build (Release)
.\build.ps1

# Debug build
.\build.ps1 -Config Debug

# With installer
.\build.ps1 -Config Release -BuildInstaller

# Manual CMake
cmake -S . -B build -G "Visual Studio 17 2022" -A x64
cmake --build build --config Release
cmake --install build --config Release
```

## File Locations After Build

- **Executable**: `install/bin/ClaudePlayer.exe`
- **Installer**: `build/ClaudePlayer-1.0.0.0-win64.msi`
- **Build artifacts**: `build/` directory

## Qt Installation Paths

- **Community Edition**: `C:\Qt\6.x.x\msvc2022_64`
- **Custom Installation**: Check your Qt installer settings

## Important Files

| File | Purpose |
|------|---------|
| `CMakeLists.txt` | Build configuration |
| `build.ps1` | Windows build script |
| `src/main.cpp` | Application entry point |
| `src/MainWindow.h` | UI definitions |
| `src/MainWindow.cpp` | UI implementation |
| `README.md` | Project overview |
| `DEVELOP.md` | Development guide |
| `INSTALL.md` | Installation guide |

## Environment Setup

```powershell
# Set Qt path (run before building)
$env:CMAKE_PREFIX_PATH = "C:\Qt\6.7.0\msvc2022_64"

# Verify CMake
cmake --version

# Verify Git
git --version
```

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Qt not found | Set `CMAKE_PREFIX_PATH` |
| Visual Studio not found | Install VS 2022 Community |
| CMake not found | Install from cmake.org or use VS CMake |
| Build fails | Clean build: `Remove-Item build -Recurse -Force` |

## Key Features

- ✅ Local media playback (audio & video)
- ✅ Playlist management
- ✅ Playback controls
- ✅ Volume & seek control
- ✅ Media info display
- ✅ Windows installer
- 🔄 Upcoming: Recording, advanced tools

## Supported Formats

**Audio**: MP3, WAV, FLAC, AAC, OGG, M4A
**Video**: MP4, MKV, AVI, MOV, WMV, FLV
**Subtitles**: SRT, ASS, SSA, VTT

## Development Tips

1. **Use Visual Studio IDE**:
   ```powershell
   cmake -S . -B build -G "Visual Studio 17 2022" -A x64
   Start-Process "build\ClaudePlayer.sln"
   ```

2. **Debug with output**:
   ```cpp
   #include <QDebug>
   qDebug() << "Variable:" << value;
   ```

3. **Clean rebuild when stuck**:
   ```powershell
   Remove-Item build, install -Recurse -Force
   .\build.ps1
   ```

## Release Process

1. Update version in `CMakeLists.txt`
2. Update `CHANGELOG.md`
3. Build: `.\build.ps1 -Config Release -BuildInstaller`
4. Test installer thoroughly
5. Create GitHub Release with `.msi` file
6. Tag commit: `git tag v1.x.x`

## Resources

- 📖 [README](README.md)
- 🔧 [DEVELOP.md](DEVELOP.md)
- 📦 [INSTALL.md](INSTALL.md)
- 🤝 [CONTRIBUTING.md](CONTRIBUTING.md)
- 📝 [CHANGELOG.md](CHANGELOG.md)
- 🔗 [Qt Docs](https://doc.qt.io/)
- 🔗 [CMake Docs](https://cmake.org/documentation/)

## License

MIT License - See [LICENSE](LICENSE) file
