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

### Remote Execution
```bash
# Basic remote installation with token
curl -sSL https://gitee.com/funnyzak/frpc/raw/main/frpc.sh | bash -s install --token your_token

# Remote installation with URL configuration
curl -sSL https://gitee.com/funnyzak/frpc/raw/main/frpc.sh | bash -s install --token your_token --config-url http://example.com/frpc.toml

# Remote installation of specific version
curl -sSL https://gitee.com/funnyzak/frpc/raw/main/frpc.sh | bash -s install --token your_token --version 0.60.0

# Remote interactive installation
curl -sSL https://gitee.com/funnyzak/frpc/raw/main/frpc.sh | bash -s install --token your_token --interactive

# Remote installation with custom paths
curl -sSL https://gitee.com/funnyzak/frpc/raw/main/frpc.sh | bash -s install --token your_token --install-path /usr/local/frpc --config-path /etc/frpc/frpc.toml

# Custom installation package download URL
curl -sSL https://gitee.com/funnyzak/frpc/raw/main/frpc.sh | bash -s install --token your_token --frp-download-url http://example.com/frp.tar.gz

# Remote view of current configuration
curl -sSL https://gitee.com/funnyzak/frpc/raw/main/frpc.sh | bash -s config

# Remote view of usage tips
curl -sSL https://gitee.com/funnyzak/frpc/raw/main/frpc.sh | bash -s tips

# Remote uninstallation
curl -sSL https://gitee.com/funnyzak/frpc/raw/main/frpc.sh | bash -s uninstall
```

### Installation
```bash
# Basic installation with token
./frpc.sh install --token my-token-value

# Installation with URL configuration
./frpc.sh install --token my-token-value --config-url http://example.com/frpc.toml

# Installation with local configuration file
./frpc.sh install --token my-token-value --config-file ./configs/frpc_basic.toml

# Interactive configuration
./frpc.sh install --token my-token-value --interactive

# Installation with custom paths
./frpc.sh install --token my-token-value --install-path /usr/local/frpc --config-path /etc/frpc/frpc.toml
```

### Management
```bash
# Show current configuration
./frpc.sh config

# Show usage tips
./frpc.sh tips

# Uninstall frpc
./frpc.sh uninstall
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
- `PROXY_URL`: Github download proxy, default uses `https://ghfast.top/`, mainly for downloads in China.
- `TMP_PATH`: Temporary file storage path, default is inside `/tmp`.
- `SERVER_INSTALL_NAME`: Service name, default is `frpc.service`, can be customized.

## Configuration Example

Basic configuration example (`configs/frpc_basic.toml`):

```toml
serverAddr = "frps.example.com"
serverPort = 7000
auth.token = "your_token_here"

# SSH tunnel configuration
[[proxies]]
name = "ssh"
type = "tcp"
localIP = "127.0.0.1"
localPort = 22
remotePort = 6000
```

Check the `configs` directory for more configuration examples.

## Troubleshooting

- Service logs can be viewed with `journalctl -u frpc`
- The script validates all inputs and configurations during execution

## Notes
- For security, the script validates all inputs and configurations.
- The script creates a systemd service for automatic startup and management.
- Logs are available in the system journal (`journalctl -u frpc`).
