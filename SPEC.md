# Nuclei Tool Specification

## Tool Information
- **Tool Name**: Nuclei
- **Version**: 3.2.4 (Latest as of September 2025)
- **Category**: Network Security & Vulnerability Scanning
- **License**: MIT License
- **Original License**: MIT License (ProjectDiscovery, Inc.)
- **Official Repository**: https://github.com/projectdiscovery/nuclei
- **Official Website**: https://projectdiscovery.io/nuclei

## Docker Configuration
- **Image**: projectdiscovery/nuclei:latest
- **Port Assignment**: 58001 (172.17.0.1:58001:8080)
- **Volume Mappings**:
  - `./root/config/nuclei:/root/.config/nuclei` (configuration)
  - `./rootfs/data/nuclei:/data` (scan results and data)
- **Network**: nuclei (isolated network)
- **Database**: Not required

## Installation Methods Tested
- ✅ **Ubuntu/Debian**: wget binary, Go install, snap package
- ✅ **CentOS/RHEL/Fedora**: curl binary, Go install
- ✅ **Arch Linux**: AUR package, Go install, manual install
- ✅ **macOS**: Homebrew, binary download, Go install
- ✅ **Windows**: Chocolatey, Scoop, binary download, Go install
- ✅ **Docker**: Official Docker image with compose configuration
- ✅ **Build from Source**: Go compilation

## Testing Notes
- **Platforms Verified**: Linux (Ubuntu 22.04, Arch), macOS, Windows 11, Docker
- **Dependencies Verified**: Go 1.19+, template repository access
- **Performance**: Fast scanning engine, handles large target lists efficiently
- **Template System**: 10,000+ community templates available
- **CI/CD Ready**: JSON/SARIF output formats supported

## Creation Details
- **Repository Created**: September 13, 2025
- **Created By**: HakMgr Organization Setup
- **Initial Version Documented**: 3.2.4
- **Template Compliance**: ✅ Full HakMgr standard compliance

## Update History
- **2025-09-13**: Initial repository creation with comprehensive documentation
- **Version Tracking**: Nuclei actively maintained with regular releases
- **Template Updates**: Community templates updated frequently
- **Security Coverage**: Covers CVE-2025-* vulnerabilities with active templates

## Special Requirements
- **Internet Connection**: Required for template updates and some scanning functions
- **Memory**: Minimum 512MB RAM, 2GB+ recommended for large scans
- **Network Access**: Outbound connections needed for vulnerability scanning
- **Template Management**: Automatic template updates recommended
- **Rate Limiting**: Built-in rate limiting for responsible scanning

## Integration Notes
- **YAML Templates**: Simple DSL for custom vulnerability detection
- **Output Formats**: JSON, SARIF, plain text supported
- **CI/CD Integration**: Exit codes and structured output for automation
- **Community**: Large active community contributing templates
- **Documentation**: Comprehensive official documentation available

## Compliance Status
- ✅ **Open Source**: MIT License (OSI-approved)
- ✅ **Active Maintenance**: Regular updates as of August 2025
- ✅ **Community Driven**: 24,737 GitHub stars, active development
- ✅ **No Commercial Restrictions**: Free for all use cases
- ✅ **Docker Support**: Official Docker images maintained