# ClaudePlayer Development Guide

## Project Structure

```
ClaudePlayer/
├── CMakeLists.txt              # CMake build configuration
├── build.ps1                   # Windows build script
├── README.md                   # Project overview
├── INSTALL.md                  # Installation guide
├── DEVELOP.md                  # Development guide (this file)
│
├── src/
│   ├── main.cpp               # Application entry point
│   ├── MainWindow.h           # Main window header
│   ├── MainWindow.cpp         # Main window implementation
│
├── resources/
│   ├── icon.rc                # Windows icon resource
│   └── icon.ico               # Application icon (create manually)
│
└── build/                      # Generated during build
    └── ClaudePlayer.exe
```

## Setting Up Development Environment

### 1. Install Required Tools

```powershell
# Using Windows Package Manager (winget)
winget install Microsoft.VisualStudio.2022.Community
winget install Kitware.CMake
winget install Qt.Qt
winget install Git.Git
```

### 2. Install Qt 6 Manually

1. Download Qt Online Installer from [qt.io](https://www.qt.io/download)
2. Run the installer
3. Create a Qt account (free)
4. Select **Qt 6.x** (latest version)
5. Install these components:
   - **MSVC 2019 64-bit** or **MSVC 2022 64-bit**
   - Check **Qt Multimedia**
   - Check **Qt 5 Compatibility Module** (optional)
6. Complete installation (takes ~15-30 minutes)

### 3. Clone Repository

```powershell
git clone https://github.com/061025koki-debug/ClaudePlayer.git
cd ClaudePlayer
```

### 4. Configure Qt Path

```powershell
# Set environment variable for your Qt installation
$env:CMAKE_PREFIX_PATH = "C:\Qt\6.7.0\msvc2022_64"  # Adjust version as needed
```

## Building

### Development Build

```powershell
# Debug build with full debugging symbols
.\build.ps1 -Config Debug
```

### Release Build

```powershell
# Optimized release build
.\build.ps1 -Config Release
```

### With Installer

```powershell
# Release build with Windows installer
.\build.ps1 -Config Release -BuildInstaller
```

## Opening in Visual Studio

```powershell
# Generate Visual Studio solution
cmake -S . -B build -G "Visual Studio 17 2022" -A x64 -DCMAKE_PREFIX_PATH="C:\Qt\6.7.0\msvc2022_64"

# Open the solution
Start-Process "build\ClaudePlayer.sln"
```

## Code Structure

### MainWindow Class

The main application window handles:

- **Media Playback**: Using `QMediaPlayer`
- **Video Display**: Using `QVideoWidget`
- **Audio Control**: Using `QAudioOutput`
- **Playlist Management**: Using `QListWidget`
- **UI Controls**: Buttons, sliders, labels

### Key Methods

```cpp
// File operations
void openFile();      // Browse and open single file
void openFolder();    // Browse and open folder

// Playback control
void play();          // Start playback
void pause();         // Pause playback
void stop();          // Stop playback
void previous();      // Previous track
void next();          // Next track

// Media information
void updateMediaInfo();        // Update media info display
void onPositionChanged(qint64);  // Handle position updates
void onDurationChanged(qint64);  // Handle duration updates
```

## Adding Features

### Adding a New Menu

1. Edit `MainWindow.h`:
```cpp
private:
    void createMenuBar();
```

2. Edit `MainWindow.cpp`:
```cpp
void MainWindow::createMenuBar()
{
    QMenuBar *menuBar = new QMenuBar(this);
    setMenuBar(menuBar);
    
    QMenu *fileMenu = menuBar->addMenu("&File");
    // Add actions...
}
```

3. Call in `createUI()`:
```cpp
void MainWindow::createUI()
{
    createMenuBar();
    // ... rest of UI
}
```

### Adding a New Control

1. Declare in `MainWindow.h`:
```cpp
private:
    QPushButton *newButton;
```

2. Create and connect in `MainWindow.cpp`:
```cpp
newButton = new QPushButton("New Button", this);
controlLayout->addWidget(newButton);
connect(newButton, &QPushButton::clicked, this, &MainWindow::onNewButtonClicked);
```

3. Implement the slot:
```cpp
void MainWindow::onNewButtonClicked()
{
    // Implementation
}
```

## Debugging

### Debug Output

```cpp
#include <QDebug>

qDebug() << "Message:" << variable;
qWarning() << "Warning:" << variable;
qCritical() << "Error:" << variable;
```

### Visual Studio Debugging

1. Build Debug configuration:
```powershell
.\build.ps1 -Config Debug
```

2. Open in Visual Studio:
```powershell
Start-Process "build\ClaudePlayer.sln"
```

3. Set breakpoints and press F5 to debug

## Common Tasks

### Update Application Version

1. Edit `CMakeLists.txt`:
```cmake
project(ClaudePlayer VERSION 1.1.0.0 LANGUAGES CXX RC)
```

2. Update `CMakeLists.txt` CPack section:
```cmake
set(CPACK_PACKAGE_VERSION "1.1.0.0")
```

### Add New Source File

1. Create file in `src/` directory
2. Edit `CMakeLists.txt`:
```cmake
qt_add_executable(ClaudePlayer WIN32
    src/main.cpp
    src/MainWindow.h
    src/MainWindow.cpp
    src/NewFile.h          # Add new files
    src/NewFile.cpp        # Add new files
)
```

### Add External Library

1. Edit `CMakeLists.txt`:
```cmake
find_package(ExternalLib REQUIRED)
target_link_libraries(ClaudePlayer PRIVATE ExternalLib::Library)
```

2. Install library with:
```powershell
vcpkg install externallibrary:x64-windows
```

## Testing

### Manual Testing Checklist

- [ ] Application starts without errors
- [ ] Open file dialog works
- [ ] Media file plays
- [ ] Play/Pause/Stop buttons work
- [ ] Seek slider works
- [ ] Volume slider works
- [ ] Previous/Next buttons work
- [ ] Playlist items load
- [ ] Double-click plays item

### Build Verification

```powershell
# Clean and rebuild
Remove-Item build -Recurse -Force
.\build.ps1 -Config Release
```

## Performance Optimization

### Build Optimization

```powershell
# Parallel build with all cores
cmake --build build --config Release --parallel
```

### Runtime Optimization

- Use Release builds for distribution
- Minimize UI updates during playback
- Use efficient data structures for playlists

## Troubleshooting Build Issues

### CMake Cannot Find Qt

```powershell
# Manually specify Qt path
$env:CMAKE_PREFIX_PATH = "C:\Qt\6.7.0\msvc2022_64"
Remove-Item build -Recurse -Force
.\build.ps1
```

### Linker Errors

```powershell
# Clean and rebuild
Remove-Item build -Recurse -Force
Remove-Item install -Recurse -Force
.\build.ps1 -Config Release
```

### Missing Dependencies

```powershell
# Verify all required Qt modules are installed
# Qt Widgets, Qt Multimedia, Qt Multimedia Widgets
```

## Publishing Updates

1. Update version in `CMakeLists.txt`
2. Update `CPACK_WIX_UPGRADE_GUID` (for major updates)
3. Build release:
```powershell
.\build.ps1 -Config Release -BuildInstaller
```
4. Create GitHub Release with `.msi` file

## Additional Resources

- [Qt Documentation](https://doc.qt.io/)
- [CMake Documentation](https://cmake.org/documentation/)
- [Visual Studio Docs](https://docs.microsoft.com/en-us/visualstudio/)
- [WiX Toolset Documentation](https://wixtoolset.org/documentation/)

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make changes and test thoroughly
4. Submit a pull request
5. Ensure all builds pass

## License

See LICENSE file in repository
