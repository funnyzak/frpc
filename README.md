# frpc (Fast Reverse Proxy)

`frpc.sh` is a comprehensive installation and management script for FRP Client (frpc), which helps establish secure connections between local and remote networks through NAT or firewalls.

## Features
- **Complete Installation**: Automated installation and configuration of frpc.
- **Multiple Configuration Methods**: Support for URL-based, local file, or interactive configuration.
- **Customizable Paths**: Flexible installation and configuration paths.
- **Service Management**: Automatic systemd service setup and management.
- **Uninstallation Support**: Clean removal of frpc installation when needed.

## Requirements
- Linux-based operating system with systemd
- Root or sudo privileges
- curl or wget for downloading packages

## Usage

### Installation
```bash
# Basic installation with token
./install_frpc.sh install --token my-token-value

# Installation with URL configuration
./install_frpc.sh install --token my-token-value --config-url http://example.com/frpc.toml

# Installation with local configuration file
./install_frpc.sh install --token my-token-value --config-file ./my-frpc.toml

# Interactive configuration
./install_frpc.sh install --token my-token-value --interactive

# Installation with custom paths
./install_frpc.sh install --token my-token-value --install-path /usr/local/frpc --config-path /etc/frpc.toml
```

### Management
```bash
# Show current configuration
./install_frpc.sh config

# Show usage tips
./install_frpc.sh tips

# Uninstall frpc
./install_frpc.sh uninstall
```

### Remote Execution
```bash
# Remote installation example
curl -sSL https://gitee.com/funnyzak/frpc/raw/main/utilities/shell/frp/install_frpc.sh | bash -s install --token your_token --config-url http://example.com/frpc.toml
```

## Options for Install Command
- `--token <value>`: Set the FRP server token (required)
- `--config-url <url>`: Download configuration from URL
- `--config-file <path>`: Use local configuration file
- `--interactive`: Enter interactive configuration mode
- `--frp-download-url <url>`: Custom download URL for frpc package
- `--install-path <path>`: Custom installation path
- `--config-path <path>`: Custom config file path
- `--version <version>`: Specific version to install

## Environment Variables
- `FRPC_INSTALL_PATH`: Custom installation path (default: /opt/frpc)
- `FRPC_CONFIG_PATH`: Custom config path (default: /etc/frp/frpc.toml)
- `FRPC_DOWNLOAD_URL`: Custom download URL for frpc package
- `FRPC_VERSION`: Specific version to install (default: 0.61.2)
- `FRPC_TOKEN`: FRP server token

## Notes
- For security, the script validates all inputs and configurations.
- The script creates a systemd service for automatic startup and management.
- Configuration files are backed up before any changes.
- Logs are available in the system journal (`journalctl -u frpc`).
