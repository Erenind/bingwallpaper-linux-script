# 🌄 Bing 壁纸 Linux 脚本

一个美观强大的命令行工具，用于在 Linux 系统上下载必应每日壁纸。📸✨

---

## 🚀 功能特性

### 🌟 核心功能
- 📅 自动下载今日必应壁纸
- 📆 下载过去7天的壁纸
- 🌍 多地区支持（中国、美国、日本、英国、德国、澳大利亚、新西兰、加拿大）
- 🖼️ 高分辨率支持（4K超高清和1080p全高清）
- 📁 自定义保存目录
- ℹ️ 壁纸信息显示
- 🎨 后端命令集成，自动设置壁纸

### 🛠️ 技术特性
- 🐚 Bash脚本 - 适用于任何Linux发行版
- 🔄 使用jq进行JSON解析
- 🌐 使用curl进行HTTP请求
- ✅ 全面的错误处理
- 📋 参数验证

---

## 📦 安装

### 先决条件
```bash
# 安装必要的依赖
# Ubuntu/Debian:
sudo apt update && sudo apt install curl jq

# CentOS/RHEL:
sudo yum install curl jq

# Arch Linux:
sudo pacman -S curl jq
```

### 下载脚本
```bash
# 克隆仓库
git clone https://github.com/Erenind/bingwallpaper-linux-script.git
cd bingwallpaper-linux-script

# 使脚本可执行
chmod +x bingwallpaper-linux-script
```

### 可选：添加到PATH
```bash
# 添加到本地bin目录
mkdir -p ~/.local/bin
cp bingwallpaper-linux-script ~/.local/bin/
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

---

## 🎯 使用方法

### 基本用法
```bash
# 下载今日壁纸
./bingwallpaper-linux-script

# 显示帮助
./bingwallpaper-linux-script --help

# 显示版本
./bingwallpaper-linux-script --version
```

### 高级用法
```bash
# 下载过去7天的壁纸
./bingwallpaper-linux-script --all

# 下载特定日期壁纸
./bingwallpaper-linux-script --date 2024-01-15

# 设置自定义地区
./bingwallpaper-linux-script --country en-US

# 设置自定义分辨率
./bingwallpaper-linux-script --resolution 1920x1080

# 设置自定义保存路径
./bingwallpaper-linux-script --save ~/Pictures/wallpapers

# 显示壁纸信息
./bingwallpaper-linux-script --info

# 自动设置壁纸（GNOME示例）
./bingwallpaper-linux-script --backend "gsettings set org.gnome.desktop.background picture-uri file://\$wallpaper"
```

---

## ⚙️ 参数说明

| 参数 | 参数说明 |
|-----------|-------------|
| `-h, --help` | 显示帮助信息 |
| `-v, --version` | 显示版本信息 |
| `-a, --all` | 下载过去7天的壁纸 |
| `-c, --country` | 设置地区 (zh-CN, en-US, ja-JP, en-UK, de-DE, en-AU, en-NZ, en-CA) |
| `-d, --date` | 下载特定日期壁纸 (YYYY-MM-DD) |
| `-r, --resolution` | 设置分辨率 (1920x1200, 1920x1080, 1366x768, 1280x768, 1080x1920, 768x1024, 800x600, 640x480, 3840x2160) |
| `-s, --save` | 设置自定义保存路径 |
| `-i, --info` | 显示壁纸信息 |
| `-b, --backend` | 设置壁纸设置命令 |

---

## 🎨 示例

### 示例1：每日壁纸自动化
```bash
# 添加到crontab实现每日壁纸
echo "0 9 * * * cd /path/to/script && ./bingwallpaper-linux-script --backend \"gsettings set org.gnome.desktop.background picture-uri file://\\\$wallpaper\"" | crontab -
```

### 示例2：多地区收藏
```bash
# 创建地区特定的收藏
./bingwallpaper-linux-script --country en-US --save ~/Pictures/bing-us
./bingwallpaper-linux-script --country ja-JP --save ~/Pictures/bing-japan
```

### 示例3：每周归档
```bash
# 每周一下载周归档
./bingwallpaper-linux-script --all --save ~/Pictures/bing-weekly-$(date +%Y-%m-%d)
```

---

## 🔧 后端命令示例

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

### 高级示例：使用 wal 和 swww
```bash
# 下载特定日期壁纸，显示信息，并使用 wal + swww 设置
bingwallpaper-linux-script -d 2025-08-25 -i -b "wal -i \$wallpaper >/dev/null 2>&1 && swww img \$wallpaper --transition-type any --transition-step 90 --transition-duration 2 --transition-fps 60"
```

---

## 📁 文件结构

```
bingwallpaper-linux-script/
├── bingwallpaper-linux-script     # 🐚 主脚本
├── bingwallpaper-linux-script-zh  # 🇨🇳 中文版本
├── LICENSE                        # 📄 许可证文件
├── README.en.md                   # 📖 英文文档
└── README.zh-CN.md                # 📖 中文文档
```

---

## 🐛 故障排除

### 常见问题

**❌ 错误: curl 工具未安装**
```bash
sudo apt install curl  # Ubuntu/Debian
sudo yum install curl  # CentOS/RHEL
```

**❌ 错误: jq 工具未安装**
```bash
sudo apt install jq    # Ubuntu/Debian
sudo yum install jq    # CentOS/RHEL
```

**❌ 壁纸未自动设置**
- 检查桌面环境是否受支持
- 验证后端命令语法

**❌ 网络连接问题**
- 检查网络连接
- 验证防火墙设置

---

## 🤝 贡献指南

欢迎贡献！🎉

### 如何贡献
1. 🍴 Fork 仓库
2. 🌿 创建功能分支 (`git checkout -b feature/amazing-feature`)
3. 💾 提交更改 (`git commit -m '添加出色功能'`)
4. 📤 推送到分支 (`git push origin feature/amazing-feature`)
5. 🔀 打开 Pull Request

### 开发指南
- 📝 遵循现有代码风格
- ✅ 为新功能添加测试
- 📖 更新文档
- 🐛 使用 GitHub Issues 报告错误

---

## 📜 许可证

本项目采用 MIT 许可证 - 查看 [LICENSE](LICENSE) 文件了解详情。📄

---

## 🙏 致谢

- **必应** 提供美丽的每日壁纸 🌄
- **开源社区** 提供出色的工具和支持 🤝
- **贡献者** 帮助改进本项目 👥

---

## ⭐ 星标历史

如果你觉得这个项目有用，请给它一个星标！⭐

[![Star History Chart](https://api.star-history.com/svg?repos=Erenind/bingwallpaper-linux-script&type=Timeline)](https://www.star-history.com/#Erenind/bingwallpaper-linux-script&Date)

---

## 📞 支持

如果你需要帮助或有疑问：🤔

- 📋 创建 [Issue](https://github.com/Erenind/bingwallpaper-linux-script/issues)
- 💬 加入我们的 [讨论](https://github.com/Erenind/bingwallpaper-linux-script/discussions)

---

**愉快的壁纸下载！🎉**
