# Release Notes

## v1.4.0 (2025-12-12)

### 🚀 New Features

#### xZenith Launcher

- **Unified Game Library** - Add, manage, and launch games from a single interface
- **Auto-Detection** - Automatically detect installed games from Steam, Epic, Xbox, GOG, and more
- **Per-Game Tweaks** - Apply performance profiles automatically when launching games
- **IGDB Integration** - Fetch game metadata (genres, description, developer, publisher, cover art) from IGDB
- **Favorites System** - Star your favorite games for quick access with filtering
- **Genre Filtering** - Filter games by genre with auto-populated dropdown
- **Fullscreen Mode** - Immersive fullscreen game browser with keyboard navigation
- **Game Size Tracking** - Calculate and display game folder sizes
- **Play Time Tracking** - Track total play time and session history per game

#### Comprehensive Keyboard Navigation

xZenith now features extensive keyboard shortcuts for power users:

**Global Shortcuts**
| Shortcut | Action |
|----------|--------|
| `Ctrl+K` | Open Global Search Command |
| `Ctrl+[` | Toggle sidebar collapse |
| `Alt+1-9` | Navigate directly to sidebar items |
| `Alt+↑/↓` | Navigate sidebar with focus |
| `Alt+Enter` | Go to focused sidebar item |
| `Alt+Home` | Go to Home page |

**xZenith Launcher (Fullscreen)**
| Shortcut | Action |
|----------|--------|
| `F11` / `Ctrl+F` | Toggle fullscreen mode |
| `←↑↓→` | Navigate game grid |
| `Enter` | Launch selected game |
| `E` | Edit game settings |
| `F` | Toggle favorite |
| `Esc` | Exit fullscreen |

**Game Settings Drawer**
| Shortcut | Action |
|----------|--------|
| `1-3` | Switch tabs |
| `Ctrl+←/→` | Navigate tabs |
| `↑/↓` | Navigate form fields |
| `Ctrl+S` | Save changes |
| `Esc` | Close drawer |
| `Alt+B` | Browse executable |
| `Alt+F` | Fetch from IGDB |
| `Alt+C` | Calculate size |

#### Tools Page Redesign

- **Compact Featured Cards** - New `FeaturedToolCard` component with 3-column grid layout
- **Smaller Quick Access** - More compact utility buttons with 4-column grid
- **Streamlined Tools Grid** - 5-column clickable cards with inline navigation
- **Reduced Page Height** - ~30% less vertical scrolling required

#### Global Search Improvements

- **Added xZenith Launcher** - Now searchable via Ctrl+K
- **Improved Trigger Reliability** - Uses capture phase to ensure Ctrl+K always works
- **Case-Insensitive** - Works with both uppercase and lowercase K

### 🐛 Bug Fixes

- Fixed keyboard event conflicts between components
- Fixed Global Search not triggering in some contexts

---

## v1.3.5 (2025-12-12)

### 🚀 New Features

#### Comprehensive Logging System

- **Application-Wide Logging** - New logging infrastructure with configurable log levels and file output
- **Structured Logging** - Replaced console.log statements with structured logging using Rust's log crate
- **Logging Settings UI** - New settings panel with:
  - Enable/disable logging toggle
  - Open log folder button
  - Clear logs functionality

#### Build & Installer Improvements

- **Optimized Release Build** - LTO (Link-Time Optimization), single codegen unit, and binary stripping for smaller, faster binaries
- **Enhanced NSIS Installer** - Silent install support (`/S` flag) and improved driver handling
- **Windows Defender Exclusion** - Automatic exclusion added during installation to prevent false positives
- **Resource Restructuring** - Organized resources into `tools/` and `installers/` subdirectories

#### Additional Improvements

- Improved error handling and debug output across all components
- Enhanced driver installation handling in installer

---

## v1.3.4 (2025-12-11)

### 🚀 New Features

#### Backend Driver Update

- **PawnIO Integration** - Replaced WinRing0 kernel driver with PawnIO for improved hardware access
  - Better compatibility with Windows security features
  - Enhanced stability and reliability
  - Improved support for modern hardware
  - Reduced antivirus false positives

#### Enhanced Monitoring Architecture

- **Component-Based Design** - Refactored monitoring page from 3,586 lines to modular components for better maintainability
- **RAM Monitoring** - New dedicated section with physical/virtual memory stats and DIMM module details
- **Battery Monitoring** - Comprehensive battery section with charge level, voltage, power rates, and capacity in Wh
- **Storage Monitoring** - Added Temperature 2 sensor support for NVMe drives with dual sensors
- **DIMM SPD Timing Data** - View RAM timing information (tAA, tRCD, tRP, tRAS) for each memory module

#### Enhanced Storage Monitoring

- **Comprehensive SMART Data** - Health metrics including remaining life, available spare, percentage used
- **Lifetime Statistics** - Total data read/written (with TB tooltip), power-on hours, power cycles
- **Activity & Throughput** - Real-time read/write activity percentages and transfer rates
- **Unsupported Hardware Indicators** - Warning tooltips for zero-value sensors (Temperature, Temperature 2, Health)

#### Improved Hardware Support

- **AMD Ryzen CCD Temps** - Support for CCD1-8 temperature sensors, CCDs Max/Average
- **AMD Effective Clocks** - Average and effective clock speed monitoring
- **Intel Core Temps** - Core max and average temperature sensors
- **Intel Arc GPUs** - Power total and throughput sensors for discrete Intel GPUs
- **New Sensor Types** - Added Timing, Conductivity, and Humidity sensor support

#### UI/UX Improvements

- **Unsupported Hardware Tooltips** - Warning indicators for zero-value sensors in Motherboard and Storage monitoring
- **GPU Core Load Fix** - Limited to 0.00% minimum to prevent negative display values
- **Data Tooltips** - Hover Data Read/Written (GB) to see TB equivalent

#### Drivers Lookup Enhancement

- **Actual Hardware IDs** - Now displays real Hardware IDs instead of device instance paths
- **Full Hardware ID Tooltip** - Hover over Hardware ID to see all associated hardware IDs
- **Improved Driver Search** - Online search now uses actual hardware IDs for more accurate results

---

## v1.3.3 (2025-12-08)

### 🐛 Bug Fixes

#### OSD Power Mode Fix

- **Fixed Power Mode OSD** - Power mode OSD now triggers correctly without requiring touchpad events
  - Power mode changes (Silent/Balanced/Performance) now show OSD independently
  - Removed incorrect dependency on touchpad state for power mode OSD display
  - Added power mode change detection to prevent duplicate OSD notifications
  - Improved event handling to filter out zero-value events

---

## v1.3.2 (2025-12-07)

### 🚀 New Features

#### Auto-Start on Login

- **Windows Startup Integration** - New setting to automatically launch xZenith when you log in to Windows
- **Toggle Control** - Enable/disable auto-start from Settings > Settings Management
- **Persistent Configuration** - Auto-start preference saved and applied on each app launch

#### Enhanced Update System

- **Download Progress Tracking** - Real-time progress bar showing download percentage during updates
- **Reusable Update Dialog** - Centralized `UpdateDialog` component shared between loading screen and settings
- **Better UX Feedback** - Clear visual indicators for:
  - Download in progress with percentage
  - Installation phase after download completes
  - Disabled controls during update process
- **Improved Error Handling** - Better error messages and state cleanup on update failures

### 🐛 Bug Fixes

#### Auto-Start Configuration

- **Fixed Hardcoded Behavior** - Auto-start now properly respects user settings instead of always enabling
- **Settings Synchronization** - Auto-start state correctly loads from settings store on app launch
- **Clean Imports** - Removed unused `MacosLauncher` imports (Windows-only app)

#### Update System Improvements

- **Type Safety** - Fixed TypeScript errors with Tauri's `DownloadEvent` types
- **Accurate Progress** - Download progress now tracks cumulative bytes instead of individual chunks
- **Event Handling** - Proper handling of Started, Progress, and Finished download events

---

## v1.3.1 (2025-12-07)

### 🐛 Bug Fixes

#### xZenithCast Improvements

- **Removed Recording Feature** - Removed unstable recording-to-file functionality that was producing blank files
- **Simplified Audio Options** - Removed recording UI controls and validation logic
- **Removed Experimental Features** - Cleaned up unstable advanced options:
  - Removed H.265 and AV1 video codecs (kept stable H.264)
  - Removed camera video source option
  - Removed FLAC and Raw audio codecs
  - Removed entire Camera Options section
  - Removed OTG Mode option
  - Removed AOA modes from keyboard/mouse/gamepad controls
- **Improved Stability** - Focus on core mirroring functionality with proven stable features

#### First-Run Tour Fixes

- **Fixed Sidebar Highlighting** - Corrected sidebar navigation item IDs to use dashes instead of spaces
- **Added New Tour Steps** - Enhanced tour coverage:
  - Drivers Lookup page with search functionality
  - Process Manager page with process search
- **Improved Navigation Flow** - Tools page now shows xZenithCast and xZenithBoost highlights in context
- **Better Timing** - Added extra wait times to ensure elements are ready before highlighting

---

## v1.3.0 (2025-12-07)

### 🚀 New Features & Improvements

This update introduces auto-update functionality, enhanced user experience with toast notifications, centralized app configuration, and improved Discord Rich Presence integration.

---

### ✨ What's New

#### Auto-Update System

- **Automatic Update Checking** - App checks for updates automatically on startup (silent mode)
- **Manual Update Check** - Check for updates anytime from Settings > Application Status
- **Auto-Update Toggle** - Enable/disable automatic updates from Settings
- **Toast Notifications** - Clean toast notifications for update status:
  - Success toast when you're already on the latest version
  - Error toast if update check fails
  - Native dialog for available updates with release notes
- **Signed Updates** - Secure update distribution with cryptographic signing
- **Custom NSIS Installer** - Windows installer with xZenith branding:
  - System compatibility check (Windows 10 1809+)
  - Automatic dependency installation (VC++ Redistributable)
  - WebView2 availability detection
  - Graceful handling of running instances
  - Registry and user data cleanup on uninstall
  - Custom install/uninstall dialogs

#### Discord Rich Presence Enhancements

- **Enhanced Discord Rich Presence** - Now shows actual hardware in your Discord status:
  - System model (e.g., "ASUS ROG Strix")
  - CPU model (e.g., "Intel Core i9-14900K")
  - GPU model (e.g., "NVIDIA RTX 4090")
  - Smart truncation for long hardware names

#### Enhanced Hardware Monitoring

- **Always-On Monitoring** - Automatic monitoring starts when opening the page
- **Continuous CSV Logging** - New "Start/Stop Logging" toggle button for real-time data recording
- **Comprehensive Data Export** - CSV logs now include 75+ hardware metrics:
  - CPU: Temperature (main, package, avg, max), Power (package, avg, max, Intel breakdown), Voltage (core, SoC), Load, Frequency, Bus Speed
  - GPU: Temperature (core, hotspot, memory, junction), Power (current, max, PPT, SoC, core), Voltage (core, SoC, memory), Load, Clock, Memory usage, Fan metrics
  - Motherboard: Temperatures (system, VRM, CPU, PCH), Voltages (Vcore, +3.3V, +5V, +12V)
  - Network: Speed, Utilization, Total transferred data
  - Storage: Temperature (primary, sensor 2), Activity, Throughput (read/write rates), Health (remaining life, spare, percentage used, errors, shutdowns), Lifetime data (GB read/written, power-on hours), Capacity used
- **Streamlined Chart Exports** - Chart dropdowns now only show PNG export (CSV export moved to logging feature)
- **Enhanced CPU Data** - Intel power breakdown (cores, graphics, memory, platform), voltage tracking, bus speed
- **Enhanced GPU Data** - Memory temperature, memory junction temperature, AMD power breakdown (PPT, SoC, Core), expanded voltage and memory metrics
- **Storage Monitoring** - Comprehensive NVMe/SATA drive monitoring with:
  - Real-time temperature tracking with dual sensors
  - Activity monitoring and throughput metrics (read/write rates)
  - Health status monitoring (remaining life, spare blocks, percentage used)
  - Lifetime statistics (total data read/written, power-on hours)
  - Per-drive selection with device metadata (model, interface, media type)
  - Detailed storage information dialog
  - CSV logging integration
  - Automatic capacity formatting (GB/GiB for <1TB drives, TB/TiB for ≥1TB drives)
- **Drivers Lookup** - New page to view all installed device drivers with:
  - Hardware IDs and driver version information
  - Filter by device category (Network, Display, Audio, USB, etc.)
  - Show/hide Microsoft drivers toggle
  - Problem device detection with error codes and descriptions
  - Search by device name, manufacturer, or hardware ID
  - Copy device information to clipboard
  - Search online for driver updates
  - Responsive design with desktop table and mobile card views

#### Dashboard & Monitoring

- Real-time system dashboard with CPU, GPU, RAM, Battery, and Storage overview
- Live hardware monitoring with performance charts for CPU, GPU, and Storage
- Temperature and power tracking for Intel, AMD, and NVIDIA hardware
- Storage device selection with health status indicators
- Customizable update intervals (0.5s - 5s)
- Min/Max/Current value tracking with history

#### System Tools

- **File System Cleaner** - Remove temporary files and free disk space
- **Driver Backup & Restore** - Backup and restore system drivers
- **DNS Changer** - Quick DNS configuration with preset providers
- **App Installer** - Install apps via Windows Package Manager (winget)
- **System Utilities** - SFC, DISM, network reset, flush DNS
- **System Diagnostics** - Sleep study, battery reports, memory diagnostics
- **xZenith Cast** - Mirror Android devices to PC
- **xZenith Boost** - Performance optimization profiles for gaming and productivity
- **Process Manager** - Monitor and control running processes with app grouping

#### System Tweaks

- Performance optimizations (HAGS, Ultimate Performance Plan)
- Privacy enhancements (Telemetry, Core Isolation settings)
- Network optimizations
- Apply/Unapply with history tracking

#### Additional Features

- Global Search Command (Ctrl+K) for quick navigation
- Discord Rich Presence integration
- On-Screen Display (OSD) for system events
- 8 color themes: xZenith, Midnight, Ocean, Forest, Sunset, Aurora, Rose, Cyber
- Dynamic backgrounds: Gradients, Shooting Stars, DarkVeil
- System Restore Points management
- First-run guided tour

---

### 💻 System Requirements

- **OS:** Windows 10 (1809+) or Windows 11
- **RAM:** 4 GB minimum, 8 GB recommended
- **Disk:** 200 MB free space
- **Prerequisites:** Edge WebView2, VC++ Redistributable, .NET Framework 4.7.2+

---

### ⚠️ Known Limitations

- Some laptop sensors may show limited data due to manufacturer restrictions
- OSD may not display on certain multi-monitor setups
- First launch may take longer while initializing hardware detection

---

### 📝 Notes

- Run as **Administrator** for full functionality
- Some features require system restart to take effect
- Please report any bugs on our Discord

---

### 🙏 Feedback

Your feedback is valuable! Please join our [Discord Server](https://discord.gg/HKG9GNTesb) to:

- Report bugs
- Suggest features
- Get support
- Connect with the community

---

**Full Changelog:** [v1.4.0](https://github.com/xFlawlessDev/xzenith/releases/tag/v1.4.0)

---

<div align="center">
  
  Made with ❤️ by xFlawlessDev
  
</div>
