# frpc 配置示例

本目录包含几种常见场景的 frpc 配置示例文件，可根据自身需求选择合适的配置模板，并进行必要的修改。

## 配置文件列表

1. **frpc_basic.toml** - 基础配置示例
   * 包含最基本的服务器连接设置和简单的 TCP 代理
   * 适合初次使用或简单场景

2. **frpc_ssh.toml** - SSH 穿透配置
   * 专注于 SSH 服务的穿透配置
   * 包含安全传输和压缩设置
   * 适合远程管理服务器场景

3. **frpc_web.toml** - Web 服务配置
   * 针对 HTTP 服务的穿透配置
   * 包含域名、路由和认证设置
   * 适合网站和 Web 应用穿透

4. **frpc_advanced.toml** - 高级组合配置
   * 多种服务类型的组合配置
   * 包含 SSH、HTTP、HTTPS、RDP 和 UDP 服务
   * 展示高级功能如 STCP、管理接口等
   * 适合复杂网络环境和多服务场景

## 使用方法

1. 根据需求选择一个配置模板
2. 复制并修改以下必要参数：
   * `serverAddr` - 改为您的 FRP 服务器地址
   * `serverPort` - 改为您的 FRP 服务器端口
   * `auth.token` - 改为您的认证令牌
   * 服务特定参数（端口、域名等）
3. 使用以下命令安装 frpc 并应用配置：

```bash
./frpc.sh install --token your_token_value --config-file ./configs/选择的配置文件
```

## 配置参数说明

所有配置文件遵循 TOML 格式，主要参数说明如下：

* **服务器连接**
  * `serverAddr` - FRP 服务器地址
  * `serverPort` - FRP 服务器端口
  * `auth.token` - 认证令牌

* **代理服务 (`[[proxies]]` 部分)**
  * `name` - 服务名称，必须唯一
  * `type` - 服务类型 (tcp, udp, http, https, stcp 等)
  * `localIP` - 本地服务 IP
  * `localPort` - 本地服务端口
  * `remotePort` - 远程服务端口 (TCP/UDP 类型使用)
  * `customDomains` - 自定义域名 (HTTP/HTTPS 类型使用)

* **日志配置**
  * `log.level` - 日志级别
  * `log.maxDays` - 日志文件保留天数
  * `log.file` - 日志文件路径

更多详细配置说明，请参考 [FRP 官方文档](https://github.com/fatedier/frp/blob/dev/README.md)。
