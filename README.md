# 🌄 Bing Wallpaper Linux Script

A beautiful and powerful command-line tool to download Bing's daily wallpapers on Linux systems. 📸✨


https://github.com/user-attachments/assets/afd7c05f-1212-4ef7-a54d-b521fb9d8216


---

## 🚀 Features

### 🌟 Core Features
- 📅 Download today's Bing wallpaper automatically
- 📆 Download wallpapers from the past 7 days
- 🌍 Multiple region support (China, US, Japan, UK, Germany, Australia, NZ, Canada)
- 🖼️ High resolution support (4K UHD & 1080p Full HD)
- 📁 Custom save directory
- ℹ️ Wallpaper information display
- 🎨 Backend command integration for automatic wallpaper setting

### 🛠️ Technical Features
- 🐚 Bash script - works on any Linux distribution
- 🔄 JSON parsing with jq
- 🌐 HTTP requests with curl
- ✅ Comprehensive error handling
- 📋 Parameter validation

---

## 📦 Installation

### Prerequisites
```bash
# Install required dependencies
# Ubuntu/Debian:
sudo apt update && sudo apt install curl jq

# CentOS/RHEL:
sudo yum install curl jq

# Arch Linux:
sudo pacman -S curl jq
```

### Download Script
```bash
# Clone the repository
git clone https://github.com/Erenind/bingwallpaper-linux-script.git
cd bingwallpaper-linux-script

# Make the script executable
chmod +x bingwallpaper-linux-script
```

### Optional: Add to PATH
```bash
# Add to your local bin directory
mkdir -p ~/.local/bin
cp bingwallpaper-linux-script ~/.local/bin/
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

---

## 🎯 Usage

### Basic Usage
```bash
# Download today's wallpaper
./bingwallpaper-linux-script

# Show help
./bingwallpaper-linux-script --help

# Show version
./bingwallpaper-linux-script --version
```

### Advanced Usage
```bash
# Download wallpapers from last 7 days
./bingwallpaper-linux-script --all

# Download specific date wallpaper
./bingwallpaper-linux-script --date 2024-01-15

# Set custom region
./bingwallpaper-linux-script --country en-US

# Set custom resolution
./bingwallpaper-linux-script --resolution 1920x1080

# Set custom save path
./bingwallpaper-linux-script --save ~/Pictures/wallpapers

# Show wallpaper information
./bingwallpaper-linux-script --info

# Set wallpaper automatically (example for GNOME)
./bingwallpaper-linux-script --backend "gsettings set org.gnome.desktop.background picture-uri file://\$wallpaper"
```

---

## ⚙️ Parameters

| Parameter | Description |
|-----------|-------------|
| `-h, --help` | Show help message |
| `-v, --version` | Show version information |
| `-a, --all` | Download last 7 days wallpapers |
| `-c, --country` | Set region (zh-CN, en-US, ja-JP, en-UK, de-DE, en-AU, en-NZ, en-CA) |
| `-d, --date` | Download specific date wallpaper (YYYY-MM-DD) |
| `-r, --resolution` | Set resolution (1920x1200, 1920x1080, 1366x768, 1280x768, 1080x1920, 768x1024, 800x600, 640x480, 3840x2160) |
| `-s, --save` | Set custom save path |
| `-i, --info` | Display wallpaper information |
| `-b, --backend` | Set wallpaper setting command |

---

## 🎨 Examples

### Example 1: Daily Wallpaper Automation
```bash
# Add to crontab for daily wallpaper
echo "0 9 * * * cd /path/to/script && ./bingwallpaper-linux-script --backend \"gsettings set org.gnome.desktop.background picture-uri file://\\\$wallpaper\"" | crontab -
```

### Example 2: Multi-region Collection
```bash
# Create region-specific collections
./bingwallpaper-linux-script --country en-US --save ~/Pictures/bing-us
./bingwallpaper-linux-script --country ja-JP --save ~/Pictures/bing-japan
```

### Example 3: Weekly Archive
```bash
# Download weekly archive every Monday
./bingwallpaper-linux-script --all --save ~/Pictures/bing-weekly-$(date +%Y-%m-%d)
```

---

## 🔧 Backend Commands

### GNOME / Unity
```bash
./bingwallpaper-linux-script --backend "gsettings set org.gnome.desktop.background picture-uri file://\$wallpaper"
```

### KDE Plasma
```bash
./bingwallpaper-linux-script --backend "dbus-send --session --dest=org.kde.plasmashell --type=method_call /PlasmaShell org.kde.PlasmaShell.evaluateScript 'string: var allDesktops = desktops(); for (i=0;i<allDesktops.length;i++) { d = allDesktops[i]; d.wallpaperPlugin = \"org.kde.image\"; d.currentConfigGroup = Array(\"Wallpaper\", \"org.kde.image\", \"General\"); d.writeConfig(\"Image\", \"file://\$wallpaper\") }'"
```

### XFCE
```bash
./bingwallpaper-linux-script --backend "xfconf-query -c xfce4-desktop -p /backdrop/screen0/monitor0/workspace0/last-image -s \$wallpaper"
```

### MATE
```bash
./bingwallpaper-linux-script --backend "gsettings set org.mate.background picture-filename \$wallpaper"
```

### Advanced Example with wal and swww
```bash
# Download specific date wallpaper, show info, and set with wal + swww
bingwallpaper-linux-script -d 2025-08-25 -i -b "wal -i \$wallpaper >/dev/null 2>&1 && swww img \$wallpaper --transition-type any --transition-step 90 --transition-duration 2 --transition-fps 60"
```

---

## 📁 File Structure

```
bingwallpaper-linux-script/
├── bingwallpaper-linux-script     # 🐚 Main script
├── bingwallpaper-linux-script-zh  # 🇨🇳 Chinese version
├── LICENSE                        # 📄 License file
├── README.en.md                   # 📖 English documentation
└── README.zh-CN.md                # 📖 Chinese documentation
```

---

## 🐛 Troubleshooting

### Common Issues

**❌ Error: curl tool is not installed**
```bash
sudo apt install curl  # Ubuntu/Debian
sudo yum install curl  # CentOS/RHEL
```

**❌ Error: jq tool is not installed**
```bash
sudo apt install jq    # Ubuntu/Debian
sudo yum install jq    # CentOS/RHEL
```

**❌ Wallpaper not setting automatically**
- Check if your desktop environment is supported
- Verify the backend command syntax

**❌ Network connection issues**
- Check your internet connection
- Verify firewall settings

---

## 🤝 Contributing

We welcome contributions! 🎉

### How to Contribute
1. 🍴 Fork the repository
2. 🌿 Create a feature branch (`git checkout -b feature/amazing-feature`)
3. 💾 Commit your changes (`git commit -m 'Add amazing feature'`)
4. 📤 Push to the branch (`git push origin feature/amazing-feature`)
5. 🔀 Open a Pull Request

### Development Guidelines
- 📝 Follow existing code style
- ✅ Add tests for new features
- 📖 Update documentation
- 🐛 Report bugs using GitHub Issues

---

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details. 📄

---

## 🙏 Acknowledgments

- **Bing** for providing beautiful daily wallpapers 🌄
- **Open source community** for amazing tools and support 🤝
- **Contributors** who help improve this project 👥

---

## ⭐ Star History

If you find this project useful, please give it a star! ⭐
## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=Erenind/bingwallpaper-linux-script&type=Timeline)](https://www.star-history.com/#Erenind/bingwallpaper-linux-script&Date)

---

## 📞 Support

If you need help or have questions: 🤔

- 📋 Create an [Issue](https://github.com/Erenind/bingwallpaper-linux-script/issues)
- 💬 Join our [Discussions](https://github.com/Erenind/bingwallpaper-linux-script/discussions)

---

**Happy wallpaper downloading! 🎉**
