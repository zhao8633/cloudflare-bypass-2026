<p align="center">
  <img src="https://img.shields.io/badge/Python-3.9+-blue.svg" alt="Python">
  <img src="https://img.shields.io/badge/Platform-Mac%20%7C%20Windows%20%7C%20Linux-green.svg" alt="Platform">
  <img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="License">
  <img src="https://img.shields.io/badge/Cloudflare-Turnstile-orange.svg" alt="Cloudflare">
</p>

<h1 align="center">🛡️ Cloudflare Bypass Tool 2026</h1>

<p align="center">
  <b>基于 SeleniumBase UC Mode 的 Cloudflare Turnstile 验证绕过工具</b>
  <br>
  <i>A Cloudflare Turnstile bypass tool based on SeleniumBase UC Mode</i>
</p>

<p align="center">
  <a href="#-快速开始">快速开始</a> •
  <a href="#-功能特点">功能特点</a> •
  <a href="#-安装部署">安装部署</a> •
  <a href="#-使用方法">使用方法</a> •
  <a href="#-english">English</a>
</p>

---

## ⚠️ 免责声明

> 本工具仅供学习研究使用，请遵守相关法律法规和目标网站的服务条款。使用本工具所产生的一切后果由使用者自行承担。

---

## 📊 测试结果

| 方法 | 状态 | cf_clearance | 耗时 |
|:---:|:---:|:---:|:---:|
| **SeleniumBase UC Mode** | ✅ 成功 | ✅ 获取 | ~35秒 |
| **直连模式** | ✅ 推荐 | ✅ 稳定 | ~35秒 |
| **并行模式** | ✅ 可用 | 取决于代理 | ~60秒 |

---

## ✨ 功能特点

- 🚀 **SeleniumBase UC Mode** - 操作系统级鼠标模拟，最稳定
- 🔄 **代理轮换模式** - 支持从文件批量加载代理
- ⚡ **并行模式** - 同时启动多个浏览器，提高效率
- 🔍 **代理检测** - HTTPS隧道验证，确保代理可用
- 🐧 **跨平台** - 支持 Mac / Windows / Linux
- 💾 **Cookie保存** - JSON和Netscape格式，方便使用

---

## 🚀 快速开始

```bash
# 安装
pip install seleniumbase

# 运行
python simple_bypass.py https://your-target-site.com
```

---

## � 安装部署

### Mac

```bash
git clone https://github.com/1837620622/cloudflare-bypass-2026.git
cd cloudflare-bypass-2026
pip install -r requirements.txt
python simple_bypass.py https://example.com
```

### Windows

```powershell
git clone https://github.com/1837620622/cloudflare-bypass-2026.git
cd cloudflare-bypass-2026
pip install -r requirements.txt
python simple_bypass.py https://example.com
```

### Linux (Ubuntu/Debian)

```bash
# 方式1: 一键安装（推荐）
git clone https://github.com/1837620622/cloudflare-bypass-2026.git
cd cloudflare-bypass-2026
sudo bash install_linux.sh
python simple_bypass.py https://example.com

# 方式2: 手动安装
sudo apt-get update
sudo apt-get install -y xvfb libglib2.0-0 libnss3 libatk1.0-0 libatk-bridge2.0-0 libcups2 libdrm2 libxkbcommon0 libgbm1 libasound2

# 安装Chrome
wget -q https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i google-chrome-stable_current_amd64.deb
sudo apt-get install -f -y

# 安装Python依赖
pip install seleniumbase pyvirtualdisplay
```

---

## 📖 使用方法

### 命令行

```bash
# 直连模式（推荐）
python simple_bypass.py https://example.com

# 指定代理
python simple_bypass.py https://example.com -p http://127.0.0.1:7890

# 代理轮换模式
python simple_bypass.py https://example.com -r -f proxy.txt

# 并行模式（3个浏览器同时）
python simple_bypass.py https://example.com -P -b 3 -t 60

# 完整参数
python simple_bypass.py https://example.com -P -c -b 3 -t 60 -n 5
```

### 参数说明

| 参数 | 说明 | 默认值 |
|:---|:---|:---:|
| `url` | 目标网站URL | 必填 |
| `-p, --proxy` | 指定代理地址 | 无 |
| `-f, --proxy-file` | 代理文件路径 | proxy.txt |
| `-r, --rotate` | 顺序代理轮换模式 | 否 |
| `-P, --parallel` | 并行模式 | 否 |
| `-b, --batch` | 并行浏览器数量 | 3 |
| `-t, --timeout` | 超时时间（秒） | 60 |
| `-n, --retries` | 最大重试次数 | 3 |
| `-c, --check-proxy` | 预检测代理存活 | 否 |

### Python API

```python
from simple_bypass import bypass_cloudflare

# 基础用法
result = bypass_cloudflare("https://example.com")

if result["success"]:
    print(f"cf_clearance: {result['cf_clearance']}")
    print(f"Cookies: {result['cookies']}")
    print(f"User-Agent: {result['user_agent']}")
else:
    print(f"失败: {result['error']}")
```

---

## 📁 项目结构

```
cloudflare-bypass-2026/
├── simple_bypass.py      # 主程序（推荐使用）
├── bypass_seleniumbase.py # 完整版（更多功能）
├── install_linux.sh      # Linux安装脚本
├── requirements.txt      # Python依赖
├── proxy.txt             # 代理列表
├── .gitignore
├── LICENSE
└── README.md
```

---

## 📝 输出文件

运行成功后，Cookie 将保存到 `output/cookies/` 目录：

- `cookies_*.json` - JSON格式，包含完整Cookie信息
- `cookies_*.txt` - Netscape格式，可用于 `curl -b`

---

## ❓ 常见问题

<details>
<summary><b>Q: 为什么不使用无头模式？</b></summary>
Cloudflare 可检测无头浏览器特征，建议保持可视化模式以获得最高成功率。
</details>

<details>
<summary><b>Q: cf_clearance 有效期？</b></summary>
通常 30 分钟到数小时，建议过期前重新获取。
</details>

<details>
<summary><b>Q: 代理不工作？</b></summary>
公共代理大多不支持 HTTPS 隧道。建议使用直连模式或购买高质量住宅代理。
</details>

<details>
<summary><b>Q: Linux 报错 "X11 display failed"？</b></summary>
运行 <code>sudo bash install_linux.sh</code> 安装必要依赖。
</details>

---

## � 技术参考

- [Cloudflare Turnstile 文档](https://developers.cloudflare.com/turnstile/)
- [SeleniumBase UC Mode](https://seleniumbase.com/)
- [研究报告](./绕过Cloudflare%20Turnstile最新研究.pdf)

---

<a name="-english"></a>
## 🌍 English

### Quick Start

```bash
pip install seleniumbase
python simple_bypass.py https://your-target-site.com
```

### Features

- 🚀 **SeleniumBase UC Mode** - OS-level mouse simulation
- 🔄 **Proxy Rotation** - Batch proxy support
- ⚡ **Parallel Mode** - Multiple browsers simultaneously
- 🐧 **Cross-platform** - Mac / Windows / Linux

### Usage

```bash
# Direct mode (recommended)
python simple_bypass.py https://example.com

# With proxy
python simple_bypass.py https://example.com -p http://127.0.0.1:7890

# Parallel mode
python simple_bypass.py https://example.com -P -b 3 -t 60
```

### Python API

```python
from simple_bypass import bypass_cloudflare

result = bypass_cloudflare("https://example.com")
if result["success"]:
    print(f"cf_clearance: {result['cf_clearance']}")
```

---

## 📄 License

MIT License © 2026

---

<p align="center">
  <b>如果这个项目对你有帮助，请给个 ⭐ Star！</b>
  <br>
  <i>If this project helps you, please give it a ⭐ Star!</i>
</p>
