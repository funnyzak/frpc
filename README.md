# frpc (Fast Reverse Proxy Client)

`frpc.sh` 是一个全面的 FRP 客户端 (frpc) 安装和管理脚本，用于帮助在 NAT 或防火墙后建立本地与远程网络之间的安全连接。

## 特点

- **一键安装**：自动化安装和配置 frpc
- **多种配置方式**：支持基于 URL、本地文件或交互式配置
- **路径自定义**：灵活的安装路径和配置路径
- **服务管理**：自动设置和管理 systemd 服务
- **完整卸载**：需要时可以彻底删除 frpc 安装

## 系统要求

- 基于 Linux 的操作系统，且支持 systemd
- root 或 sudo 权限
- curl 或 wget 用于下载软件包

## 如何使用


```bash
# 基本远程安装示例（使用令牌）
curl -sSL https://raw.githubusercontent.com/funnyzak/frpc/refs/heads/main/frpc.sh | bash -s install --token your_token

# 使用远程配置文件URL安装
curl -sSL https://raw.githubusercontent.com/funnyzak/frpc/refs/heads/main/frpc.sh | bash -s install --token your_token --config-url http://example.com/frpc.toml

# 远程安装特定版本
curl -sSL https://raw.githubusercontent.com/funnyzak/frpc/refs/heads/main/frpc.sh | bash -s install --token your_token --version 0.60.0

# 远程交互式安装
curl -sSL https://raw.githubusercontent.com/funnyzak/frpc/refs/heads/main/frpc.sh | bash -s install --token your_token --interactive

# 远程安装到自定义路径
curl -sSL https://raw.githubusercontent.com/funnyzak/frpc/refs/heads/main/frpc.sh | bash -s install --token your_token --install-path /usr/local/frpc --config-path /etc/frpc/frpc.toml

# 自定义安装包下载地址
curl -sSL https://raw.githubusercontent.com/funnyzak/frpc/refs/heads/main/frpc.sh | bash -s install --token your_token --frp-download-url http://example.com/frp.tar.gz

# 远程查看当前配置
curl -sSL https://raw.githubusercontent.com/funnyzak/frpc/refs/heads/main/frpc.sh | bash -s config

# 远程查看使用提示
curl -sSL https://raw.githubusercontent.com/funnyzak/frpc/refs/heads/main/frpc.sh | bash -s tips

# 远程卸载
curl -sSL https://raw.githubusercontent.com/funnyzak/frpc/refs/heads/main/frpc.sh | bash -s uninstall
```
> 如果你在中国大陆地区，无法访问 Github, 请使用 `Gitee` 镜像地址：
> `https://gitee.com/funnyzak/frpc/raw/main/frpc.sh`，或者使用 `ghfast` 代理地址：`https://ghfast.top/https://raw.githubusercontent.com/funnyzak/frpc/refs/heads/main/frpc.sh`。

> 如果使用模板配置文件，则配置文件中的 `token` 值，使用占位符号 `your_token_here`，在安装时会自动替换为传入的 `--token` 值。

### 基本安装

```bash
# 基本安装（使用 token）
./frpc.sh install --token my-token-value

# 使用 URL 配置安装
./frpc.sh install --token my-token-value --config-url http://example.com/frpc.toml

# 使用本地配置文件安装
./frpc.sh install --token my-token-value --config-file ./configs/frpc_basic.toml

# 交互式配置安装
./frpc.sh install --token my-token-value --interactive

# 自定义路径安装
./frpc.sh install --token my-token-value --install-path /usr/local/frpc --config-path /etc/frpc/frpc.toml
```

### 管理命令

```bash
# 查看当前配置
./frpc.sh config

# 查看使用提示
./frpc.sh tips

# 卸载 frpc
./frpc.sh uninstall
```

## 命令选项

- `--token <value>`：设置 FRP 服务器令牌（必需）
- `--config-url <url>`：从 URL 下载客户端配置文件
- `--config-file <path>`：使用本地配置文件
- `--interactive`：进入交互式配置模式
- `--frp-download-url <url>`：自定义 frpc 包的下载 URL，如果不指定，则使用默认的 GitHub URL 和 最新版本
- `--install-path <path>`：自定义安装路径，不需要指定，默认安装在 `/opt/frpc`
- `--config-path <path>`：自定义配置文件路径，不需要指定，默认安装在 `/etc/frp/frpc.toml`
- `--version <version>`：指定要安装的版本，如果不指定，则使用最新版本

## 环境变量

- `FRPC_INSTALL_PATH`：自定义安装路径（默认：/opt/frpc）
- `FRPC_CONFIG_PATH`：自定义配置路径（默认：/etc/frp/frpc.toml）
- `FRPC_DOWNLOAD_URL`：自定义 frpc 包的下载 URL
- `FRPC_VERSION`：指定安装的版本（默认：0.61.2）
- `FRPC_TOKEN`：FRP 服务器令牌
- `PROXY_URL`： 如果在中国大陆地区，则使用 Github 下载代理，默认使用 `https://ghfast.top/` 以提高下载速度。可以通过设置环境变量 `PROXY_URL` 来修改代理地址。
- `TMP_PATH`：临时文件存放路径，默认 `/tmp` 内。
- `SERVER_INSTALL_NAME`：服务名称，默认 `frpc.service`，可自定义。

## 配置示例

基础配置示例（`configs/frpc_basic.toml`）：

```toml
serverAddr = "frps.example.com"
serverPort = 7000
auth.token = "your_token_here"

# SSH 穿透配置
[[proxies]]
name = "ssh"
type = "tcp"
localIP = "127.0.0.1"
localPort = 22
remotePort = 6000
```

查看 `configs` 目录获取更多配置示例。

## 安装示例

如下为一个通过远程配置文件安装的示例：

```plain
> # curl -sSL https://gitee.com/funnyzak/frpc/raw/main/frpc.sh | bash -s install --token myfrpstoken --config-url https://myfrpcstore.yycc.dev/示例配置.toml
[INFO] Configuration method: URL (https://myfrpcstore.yycc.dev/示例配置.toml)

===== Installing FRPC =====

===== Pre-installation Checks =====
[INFO] Checking required dependencies...
[SUCCESS] All dependencies are installed.
[SUCCESS] systemd is available.
[INFO] Created temporary directory: /tmp/frpc_install_1744079006
[INFO] Downloading FRPC configuration to /tmp/frpc_install_1744079006/frpc_conf_1744079006.toml
[INFO] Source: https://myfrpcstore.yycc.dev/示例配置.toml
######################################################################## 100.0%
[SUCCESS] FRPC configuration downloaded successfully.
[SUCCESS] Configuration successfully downloaded from URL.
[SUCCESS] FRPC configuration applied successfully to /etc/frp/frpc.toml
[INFO] Downloading FRPC package to /tmp/frpc_install_1744079006/frp.tar.gz
[INFO] Source: https://ghfast.top/https://github.com/fatedier/frp/releases/download/v0.61.2/frp_0.61.2_linux_amd64.tar.gz
######################################################################## 100.0%
[SUCCESS] FRPC package downloaded successfully.
[INFO] Extracting FRPC package...
[SUCCESS] FRPC binary installed to /opt/frpc/frpc
[INFO] Configuring systemd service...
Created symlink /etc/systemd/system/multi-user.target.wants/frpc.service → /etc/systemd/system/frpc.service.
[INFO] Checking FRPC service status...
● frpc.service - FRP Client Service
     Loaded: loaded (/etc/systemd/system/frpc.service; enabled; vendor preset: enabled)
     Active: active (running) since Tue 2025-04-08 10:23:35 CST; 2s ago
   Main PID: 23709 (frpc)
      Tasks: 6 (limit: 48097)
     Memory: 4.9M
        CPU: 11ms
     CGroup: /system.slice/frpc.service
             └─23709 /opt/frpc/frpc -c /etc/frp/frpc.toml

4月 08 10:23:35 PVE systemd[1]: Started FRP Client Service.
4月 08 10:23:35 PVE frpc[23709]: 2025-04-08 10:23:35.561 [I] [sub/root.go:142] start frpc service for config file [/etc/frp/frpc.toml]
4月 08 10:23:35 PVE frpc[23709]: 2025-04-08 10:23:35.562 [I] [client/service.go:295] try to connect to server...
4月 08 10:23:35 PVE frpc[23709]: 2025-04-08 10:23:35.603 [I] [client/service.go:287] [b150d9480cc74323] login to server success, get run id [b150d9480cc74323]
4月 08 10:23:35 PVE frpc[23709]: 2025-04-08 10:23:35.603 [I] [proxy/proxy_manager.go:173] [b150d9480cc74323] proxy added: [示例配置.RPC 示例配置.HTTP]
4月 08 10:23:35 PVE frpc[23709]: 2025-04-08 10:23:35.615 [I] [client/control.go:168] [b150d9480cc74323] [示例配置.RPC] start proxy success
4月 08 10:23:35 PVE frpc[23709]: 2025-04-08 10:23:35.615 [I] [client/control.go:168] [b150d9480cc74323] [示例配置.HTTP] start proxy success
Hint: Some lines were ellipsized, use -l to show in full.
[SUCCESS] FRPC service is running.
```

## 故障排除

- 服务日志可通过 `journalctl -u frpc` 查看
- 脚本在执行过程中会对所有输入和配置进行验证

## 注意事项

- 为安全起见，脚本会验证所有输入和配置
- 脚本会创建 systemd 服务，用于自动启动和管理
- 日志可在系统日志中查看（`journalctl -u frpc`）