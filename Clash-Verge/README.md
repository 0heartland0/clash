# Clash Verge 配置说明

本目录提供适用于 Clash Verge 客户端的完整 YAML 配置，内核面向 Mihomo（Clash.Meta）：

```text
Clash-Verge.yaml
```

配置默认启用虚拟网卡模式（TUN）、IPv6、Fake-IP、流量嗅探和分流规则。策略组与规则基于本仓库维护的 Clash 规则体系。

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
5. 启用配置后，进入 `设置 -> 虚拟网卡模式`，开启虚拟网卡模式（TUN）。

### Remote 导入

Remote 模式只能让 Clash Verge 在线下载本仓库的 YAML 模板，不能自动替换模板里的机场订阅占位。

如果配置文件上传到 GitHub，可将 Raw 地址填入 Clash Verge 的 `订阅链接`：

```text
https://raw.githubusercontent.com/0heartland0/clash/main/Clash-Verge/Clash-Verge.yaml
```

公开仓库中的配置会保留：

```yaml
proxy-providers:
  Sub-store:
    url: "订阅链接请复制通用订阅"
```

因此，直接用上面的 Raw 地址创建 `Remote` 配置时，Clash Verge 只能下载到配置模板，不能拉取到代理节点。

如需实际使用，请选择以下方式之一：

- 推荐：下载 `Clash-Verge.yaml`，在本地替换订阅占位后，通过 `Local` 导入。
- 私用：Fork 本仓库到私有仓库，在私有仓库中替换订阅链接，再使用自己的 Raw 地址导入。
- 高级：自行搭建配置生成器，在服务端将订阅占位替换为真实订阅后返回 YAML。

不要把真实机场订阅链接提交到公开 GitHub。订阅链接通常等同账号凭证，泄露后可能被他人使用。

## 虚拟网卡模式（TUN）与 DNS 防泄露

配置文件已包含虚拟网卡模式（TUN）基础配置：

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

Clash Verge 中“虚拟网卡模式”就是 TUN 模式。该设置可能由客户端 UI 独立管理，导入配置后建议手动检查：

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
- 虚拟网卡模式（TUN）通常需要按 Clash Verge 的提示启用服务模式，或以管理员权限运行。
