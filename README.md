# 🚀 Nuclei - Fast Vulnerability Scanner

> Community-powered vulnerability scanner built on YAML-based templates for detecting security vulnerabilities across applications, APIs, networks, DNS, and cloud configurations.

## 📖 Tool Overview

Nuclei is a fast, customizable vulnerability scanner powered by the global security community and built on a simple YAML-based DSL. It enables collaboration to tackle trending vulnerabilities on the internet and helps security professionals find vulnerabilities in applications, APIs, networks, DNS, and cloud configurations.

**Key Features:**
- ⚡ Fast and efficient scanning engine
- 🔧 YAML-based template system
- 🌐 Community-driven template library (10,000+ templates)
- 🎯 Multi-target support (web apps, APIs, networks, DNS, cloud)
- 📊 Multiple output formats (JSON, SARIF, etc.)
- 🔄 CI/CD integration ready

## 📋 Prerequisites

### System Requirements
- **Operating System**: Linux, macOS, Windows
- **Memory**: 512MB RAM minimum (2GB+ recommended for large scans)
- **Storage**: 100MB for binary, additional space for templates
- **Network**: Internet connection for template updates

### Dependencies
- **Go**: 1.19+ (for building from source)
- **Git**: For template repository management
- **curl/wget**: For downloading releases

## 🔧 Installation Instructions

### Ubuntu/Debian Linux
```bash
# Method 1: Download latest release
wget https://github.com/projectdiscovery/nuclei/releases/latest/download/nuclei_3.2.4_linux_amd64.zip
unzip nuclei_3.2.4_linux_amd64.zip
sudo mv nuclei /usr/local/bin/
nuclei -version

# Method 2: Using Go
go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest

# Method 3: Using snap
sudo snap install nuclei
```

### CentOS/RHEL/Fedora
```bash
# Method 1: Download latest release
curl -LO https://github.com/projectdiscovery/nuclei/releases/latest/download/nuclei_3.2.4_linux_amd64.zip
unzip nuclei_3.2.4_linux_amd64.zip
sudo mv nuclei /usr/local/bin/
nuclei -version

# Method 2: Using Go
go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest

# Method 3: Using RPM (if available)
# Check releases page for RPM packages
```

### Arch Linux
```bash
# Method 1: Using AUR
yay -S nuclei-bin

# Method 2: Using Go
go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest

# Method 3: Manual installation
wget https://github.com/projectdiscovery/nuclei/releases/latest/download/nuclei_3.2.4_linux_amd64.zip
unzip nuclei_3.2.4_linux_amd64.zip
sudo mv nuclei /usr/local/bin/
```

### macOS
```bash
# Method 1: Using Homebrew
brew install nuclei

# Method 2: Download latest release
curl -LO https://github.com/projectdiscovery/nuclei/releases/latest/download/nuclei_3.2.4_macOS_amd64.zip
unzip nuclei_3.2.4_macOS_amd64.zip
sudo mv nuclei /usr/local/bin/
nuclei -version

# Method 3: Using Go
go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest
```

### Windows
```powershell
# Method 1: Download latest release
# Download nuclei_3.2.4_windows_amd64.zip from releases page
# Extract and add to PATH

# Method 2: Using Chocolatey
choco install nuclei

# Method 3: Using Scoop
scoop install nuclei

# Method 4: Using Go
go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest
```

### Build from Source
```bash
git clone https://github.com/projectdiscovery/nuclei.git
cd nuclei/cmd/nuclei
go build -o nuclei .
sudo mv nuclei /usr/local/bin/
nuclei -version
```

## 🐳 Docker Installation

### Basic Docker Setup
```bash
# Pull latest image
docker pull projectdiscovery/nuclei:latest

# Run basic scan
docker run --rm projectdiscovery/nuclei:latest -u https://example.com
```

### Docker Compose Configuration
```yaml
name: nuclei

services:
  nuclei:
    image: projectdiscovery/nuclei:latest
    volumes:
      - ./root/config/nuclei:/root/.config/nuclei
      - ./volumes/data/nuclei:/data
    ports:
      - "172.17.0.1:58001:8080"
    networks:
      - nuclei
    restart: unless-stopped
    command: ["nuclei", "-h"]

networks:
  nuclei:
    external: false
```

### Advanced Docker Usage
```bash
# Run with custom templates
docker run --rm -v $(pwd):/data projectdiscovery/nuclei:latest -u https://example.com -t /data/custom-templates/

# Run with output to host
docker run --rm -v $(pwd):/results projectdiscovery/nuclei:latest -u https://example.com -o /results/nuclei-output.txt

# Run with config volume
docker run --rm -v nuclei-config:/root/.config/nuclei projectdiscovery/nuclei:latest -update-templates
```

## 📚 Usage

### Basic Usage
```bash
# Simple vulnerability scan
nuclei -u https://example.com

# Scan multiple targets
nuclei -l targets.txt

# Scan with specific severity
nuclei -u https://example.com -s critical,high

# Update templates before scanning
nuclei -update-templates
nuclei -u https://example.com
```

### Advanced Usage
```bash
# Scan with specific templates
nuclei -u https://example.com -t nuclei-templates/cves/
nuclei -u https://example.com -t nuclei-templates/vulnerabilities/

# Custom template usage
nuclei -u https://example.com -t custom-template.yaml

# Scan with rate limiting
nuclei -u https://example.com -rate-limit 100

# Parallel scanning
nuclei -l targets.txt -c 25

# Output formats
nuclei -u https://example.com -json -o results.json
nuclei -u https://example.com -sarif -o results.sarif
```

### Template Management
```bash
# List available templates
nuclei -tl

# Update templates
nuclei -update-templates

# Run specific template tags
nuclei -u https://example.com -tags sqli,xss

# Exclude specific templates
nuclei -u https://example.com -exclude-tags dos
```

### CI/CD Integration
```bash
# Basic CI scan (exit on findings)
nuclei -u https://staging.example.com -s high,critical -exit-on-found

# Generate reports for CI
nuclei -u https://example.com -json -o nuclei-report.json -s medium,high,critical
```

## 🛠️ Troubleshooting

### Common Issues

**Templates not found:**
```bash
# Update templates
nuclei -update-templates

# Check template location
nuclei -tl | head -10
```

**Connection timeouts:**
```bash
# Increase timeout
nuclei -u https://example.com -timeout 30

# Reduce rate limit
nuclei -u https://example.com -rate-limit 10
```

**Permission denied (Linux):**
```bash
# Fix binary permissions
chmod +x nuclei
sudo mv nuclei /usr/local/bin/
```

**Memory issues:**
```bash
# Reduce concurrent threads
nuclei -l targets.txt -c 10

# Use streaming mode for large scans
nuclei -l targets.txt -stream
```

### Performance Optimization
```bash
# Optimize for large target lists
nuclei -l targets.txt -c 50 -rate-limit 150 -timeout 10

# Use bulk processing
nuclei -l targets.txt -bulk-size 25

# Enable HTTP pipeline
nuclei -u https://example.com -http-pipeline
```

### Debug Mode
```bash
# Enable verbose output
nuclei -u https://example.com -verbose

# Debug mode
nuclei -u https://example.com -debug

# Show statistics
nuclei -u https://example.com -stats
```

## 🔗 Additional Resources

- 📖 [Official Documentation](https://docs.projectdiscovery.io/tools/nuclei/overview)
- 🎥 [Video Tutorials](https://www.youtube.com/c/ProjectDiscovery)
- 📚 [Template Writing Guide](https://docs.projectdiscovery.io/templates/introduction)
- 🐛 [Bug Reports](https://github.com/projectdiscovery/nuclei/issues)
- 💬 [Community Discord](https://discord.gg/projectdiscovery)
- 📝 [Blog Posts](https://blog.projectdiscovery.io/)

### Learning Resources
- 🎓 [Nuclei Academy](https://nuclei.projectdiscovery.io/nuclei/get-started/)
- 📖 [Template Examples](https://github.com/projectdiscovery/nuclei-templates)
- 🔧 [Custom Template Development](https://docs.projectdiscovery.io/templates/protocols/http)
- 🚀 [Advanced Usage Patterns](https://blog.projectdiscovery.io/nuclei-unleashed-quickly-write-complex-exploits/)

---

## 📦 Official Links

- 📦 **Source Code**: [https://github.com/projectdiscovery/nuclei](https://github.com/projectdiscovery/nuclei)
- 🌐 **Official Website**: [https://projectdiscovery.io/nuclei](https://projectdiscovery.io/nuclei)
- 📄 **License**: MIT License