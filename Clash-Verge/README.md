# Clash Verge 配置说明

本目录提供适用于 Clash Verge 客户端的完整 YAML 配置，内核面向 Mihomo（Clash.Meta）：

```text
Clash-Verge.yaml
```

配置默认启用 TUN、IPv6、Fake-IP、流量嗅探和分流规则。策略组与规则基于本仓库维护的 Clash 规则体系。

## 使用方法

### 本地导入

1. 下载或复制 `Clash-Verge.yaml`。
2. 打开文件，找到：

```yaml
proxy-providers:
  Sub-store:
    url: "订阅链接请复制通用订阅"
```

3. 将占位内容替换为自己的机场通用订阅链接。
4. 在 Clash Verge 中选择 `订阅 -> 新建 -> Local` 导入该文件。
5. 启用配置后，进入 `设置 -> 虚拟网卡模式`，开启 TUN。

### Remote 导入

如果配置文件上传到 GitHub，可使用 Raw 地址作为 Remote 订阅链接，例如：

```text
https://raw.githubusercontent.com/0heartland0/clash/main/Clash-Verge/Clash-Verge.yaml
```

公开仓库中的配置请保留订阅占位，不要提交真实机场订阅链接。真实订阅链接通常等同账号凭证，泄露后可能被他人使用。

## TUN 与 DNS 防泄露

配置文件已包含 TUN 基础配置：

```yaml
tun:
  enable: true
  stack: mixed
  device: mihomo
  dns-hijack:
    - any:53
    - tcp://any:53
  auto-route: true
  auto-detect-interface: true
  auto-redirect: true
  endpoint-independent-nat: true
```

Clash Verge 的虚拟网卡设置可能由客户端 UI 独立管理。导入配置后，建议手动检查：

```text
设置 -> 虚拟网卡模式 -> 严格路由
```

如果 DNS 检测出现 China IP，请开启 `严格路由`，保存后重启内核，并清理系统 DNS 缓存：

```powershell
ipconfig /flushdns
```

浏览器中的 `安全 DNS` / `Secure DNS` 建议关闭，或设置为使用系统 DNS，否则浏览器可能绕过 Mihomo 自行发起 DoH 查询。

## 注意事项

- `url: "订阅链接请复制通用订阅"` 是公开模板占位，不是可用订阅。
- `Remote` 模式只能拉取在线 YAML，不会自动替换配置中的订阅占位。
- 如果要公开发布到 GitHub，不要在配置文件中写入真实订阅链接。
- 如果只在本机使用，可以复制一份本地私有配置，填入真实订阅后用 `Local` 导入。
- TUN 模式通常需要 Clash Verge 开启 Service Mode 或管理员权限。
