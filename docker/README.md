# 🐳 Docker Installer for Ubuntu

[![Ubuntu](https://img.shields.io/badge/Ubuntu-22.04%20|%2024.04-E95420?style=flat-square&logo=ubuntu&logoColor=white)](https://ubuntu.com/)
[![Docker](https://img.shields.io/badge/Docker-Latest-2496ED?style=flat-square&logo=docker&logoColor=white)](https://www.docker.com/)
[![License](https://img.shields.io/badge/License-MIT-green.svg?style=flat-square)](LICENSE)
[![Shell Script](https://img.shields.io/badge/Shell-Bash-4EAA25?style=flat-square&logo=gnu-bash&logoColor=white)](https://www.gnu.org/software/bash/)

A comprehensive, automated Docker installation script for Ubuntu 22.04/24.04 LTS with elegant progress visualization and 2025 best practices.

## ✨ Features

### 🎨 **Elegant User Experience**
- **Beautiful Progress Display**: Colored output with Unicode symbols (✓, ✗, ℹ, →, 🐳, ⚙)
- **Real-time Feedback**: Step-by-step progress indicators with detailed substeps
- **Professional Output**: Clean headers, summaries, and formatted information sections

### 🔒 **Security & Best Practices**
- **Non-root Execution**: Prevents running as root for enhanced security
- **Clean Installation**: Removes conflicting old Docker versions
- **Official Sources**: Uses Docker's official GPG keys and repositories
- **Secure Configuration**: Implements 2025 security best practices
- **Proper Permissions**: Configures user access safely

### 🛠 **System Compatibility**
- **Ubuntu LTS Support**: Compatible with Ubuntu 22.04 (Jammy) and 24.04 (Noble)
- **Architecture Support**: Works with amd64, arm64, and armhf architectures
- **System Validation**: Checks disk space, memory, and system requirements
- **Version Detection**: Automatic OS version detection and validation

### 📊 **Advanced Configuration**
- **Modern Daemon Config**: Optimized `daemon.json` with 2025 best practices
- **BuildKit Enabled**: Latest Docker build features enabled by default
- **Log Management**: Automatic log rotation and size limits
- **Storage Optimization**: Uses overlay2 storage driver
- **Live Restore**: Keeps containers running during daemon updates

### 🔍 **Comprehensive Verification**
- **Installation Testing**: Automated verification of all components
- **Hello World Test**: Runs Docker's hello-world container
- **Service Status**: Checks Docker daemon status
- **Version Reporting**: Displays installed versions and system info

## 🚀 Quick Start

### Prerequisites

- Ubuntu 22.04 LTS or Ubuntu 24.04 LTS
- Internet connection
- Sudo privileges
- At least 1GB RAM and 2GB free disk space

### Installation

```bash
# Download the script
wget https://raw.githubusercontent.com/alialnaghmoush/docker-installer/main/install-docker.sh

# Make it executable
chmod +x install-docker.sh

# Run the installer
./install-docker.sh
```

### One-liner Installation

```bash
curl -fsSL https://raw.githubusercontent.com/alialnaghmoush/docker-installer/main/install-docker.sh | bash
```

## 📋 What Gets Installed

The script installs the latest versions of:

- **Docker Engine** - The core Docker runtime
- **Docker CLI** - Command-line interface
- **containerd** - Container runtime
- **Docker Buildx** - Extended build capabilities
- **Docker Compose** - Multi-container application management

## 🔧 Configuration Details

### Docker Daemon Configuration

The script creates an optimized `/etc/docker/daemon.json`:

```json
{
    "log-driver": "json-file",
    "log-opts": {
        "max-size": "10m",
        "max-file": "3"
    },
    "storage-driver": "overlay2",
    "features": {
        "buildkit": true
    },
    "default-address-pools": [
        {
            "base": "172.20.0.0/16",
            "size": 24
        }
    ],
    "userland-proxy": false,
    "experimental": false,
    "live-restore": true
}
```

### Security Features

- **User Group Management**: Adds current user to docker group
- **Socket Permissions**: Properly configures Docker socket
- **Non-root Operation**: Ensures Docker runs without root privileges
- **Clean Package Management**: Removes conflicting packages safely

## 📸 Screenshots

### Installation Progress
```
═══════════════════════════════════════════════════════════════
🐳 Docker Installer v1.0 🐳
═══════════════════════════════════════════════════════════════

→ Checking Ubuntu version compatibility
✓ Ubuntu 24.04 LTS (Noble) detected - Supported

→ Checking system requirements
✓ Architecture amd64 is supported
✓ Sufficient disk space available
✓ Sufficient memory available (4096 MB)

→ Updating system packages
  ⚙ Updating package index
  ⚙ Installing prerequisite packages
✓ System packages updated successfully
```

### Installation Summary
```
📋 Installation Summary:
   • Docker Engine: 25.0.3
   • Docker Compose: v2.24.6
   • Architecture: amd64
   • Ubuntu Version: 24.04 (noble)
   • Installation Log: /tmp/docker_install_20250530_143022.log

⚠️  Important Notes:
   • You may need to log out and back in for group changes to take effect
   • Test your installation: docker run hello-world
   • Check Docker status: sudo systemctl status docker

🚀 Quick Start Commands:
   • Start a container: docker run -it ubuntu:latest bash
   • List containers: docker ps -a
   • List images: docker images
   • Docker Compose: docker compose up -d
```

## 🧪 Testing Your Installation

After installation, verify everything works:

```bash
# Test Docker
docker run hello-world

# Check Docker version
docker --version

# Check Docker Compose
docker compose version

# View running containers
docker ps

# Check Docker service status
sudo systemctl status docker
```

## 🔧 Troubleshooting

### Common Issues

**Permission Denied Error**
```bash
# If you get permission errors, try:
sudo usermod -aG docker $USER
newgrp docker
# Or log out and back in
```

**Service Not Starting**
```bash
# Check Docker service status
sudo systemctl status docker

# Restart Docker service
sudo systemctl restart docker

# Check logs
sudo journalctl -u docker
```

**Old Docker Conflicts**
```bash
# The script automatically removes old versions, but if issues persist:
sudo apt-get purge docker docker-engine docker.io containerd runc
sudo apt-get autoremove
# Then run the installer again
```

### Log Files

Installation logs are saved to `/tmp/docker_install_YYYYMMDD_HHMMSS.log` for debugging.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

### Development

```bash
# Clone the repository
git clone https://github.com/alialnaghmoush/docker-installer.git
cd docker-installer

# Make changes and test
chmod +x install-docker.sh
./install-docker.sh
```

### Reporting Issues

Please include the following information when reporting issues:
- Ubuntu version (`lsb_release -a`)
- Architecture (`dpkg --print-architecture`)
- Error messages
- Installation log file contents

## 📚 Additional Resources

- [Docker Documentation](https://docs.docker.com/)
- [Docker Compose Documentation](https://docs.docker.com/compose/)
- [Docker Best Practices](https://docs.docker.com/develop/best-practices/)
- [Ubuntu Docker Installation Guide](https://docs.docker.com/engine/install/ubuntu/)

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Docker team for excellent documentation
- Ubuntu community for LTS support
- Contributors and testers

## 📊 Compatibility Matrix

| Ubuntu Version | Status | Docker CE | Docker Compose | Notes |
|---------------|--------|-----------|----------------|-------|
| 22.04 LTS (Jammy) | ✅ Supported | Latest | Plugin | Fully tested |
| 24.04 LTS (Noble) | ✅ Supported | Latest | Plugin | Fully tested |
| 20.04 LTS (Focal) | ❌ Not supported | - | - | Use older version |
| Other versions | ❌ Not supported | - | - | Not tested |

## 🔄 Version History

### v1.0 (Current)
- ✨ Added Ubuntu 24.04 support
- 🔧 Updated to latest Docker best practices
- 🎨 Enhanced UI with better progress indicators
- 🔒 Improved security configuration
- 📊 Added comprehensive system checks

### Previous Versions
See [CHANGELOG.md](CHANGELOG.md) for detailed version history.

---

**Made with ❤️ for the Docker community**

If this script helped you, please ⭐ star the repository!