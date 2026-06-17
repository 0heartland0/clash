# 🌀 OpenClash_Overwrite 覆写模块

> 🧩 适配版本：**OpenClash v0.47.006 及以上**  
> 🧱 建议新装 **OpenClash** 用户使用，请勿修改任何 LuCI 设置  
`yaml` 目录是最终被 OpenClash 加载的 Mihomo 配置文件，`conf` 目录是 OpenClash 覆写模块文件。正常使用时，在 OpenClash 覆写模块里添加 `conf` 文件链接即可，`conf` 会自动下载并指向对应的 `yaml` 配置。

---

## 📖 目录

* [⚙️ 使用方法](#️-使用方法)
  * [1️⃣ 新增覆写模块](#1️⃣-新增覆写模块)
  * [2️⃣ 配置环境变量](#2️⃣-配置环境变量)
* [💡 温馨提示](#-温馨提示)

---




## ⚙️ 使用方法

### 1️⃣ 新增覆写模块

* **文件名**：可自定义  
* **类型**：`http`  
* **订阅链接**：根据使用场景选择  

#### 🔹 主路由用户 - Url-test -无IPv6

```bash
https://raw.githubusercontent.com/0heartland0/clash/main/overwrite/conf/Overwrite-Yacd.conf
```

#### 🔹 主路由用户 - Url-test -无IPv6 -如果机场只提供临时订阅链接，建议使用低频版

```bash
https://raw.githubusercontent.com/0heartland0/clash/main/overwrite/conf/Overwrite-Yacd-SlowUpdate.conf
```

#### 🔹 主路由IPv6用户 - Url-test 

```bash
https://raw.githubusercontent.com/0heartland0/clash/main/overwrite/conf/Overwrite-Yacd-IPv6.conf
```

#### 🔹 主路由IPv6用户 - Url-test -需要 IPv6、低频拉取

```bash
https://raw.githubusercontent.com/0heartland0/clash/main/overwrite/conf/Overwrite-Yacd-SlowUpdate-IPv6.conf
```

#### 🔹 主路由用户 - Url-test -无IPv6 -路由器访问 GitHub raw 不稳定，使用 CDN 版

```bash
https://testingcf.jsdelivr.net/gh/0heartland0/clash@main/overwrite/conf/Overwrite-Yacd-CDN.conf
```

#### 🔹 主路由用户 - Url-test -无IPv6 -需要 低频拉取和 CDN 加速

```bash
https://testingcf.jsdelivr.net/gh/0heartland0/clash@main/overwrite/conf/Overwrite-Yacd-SlowUpdate-CDN.conf
```

#### 🔹 主路由IPv6用户 - Url-test -CDN 加速

```bash
https://testingcf.jsdelivr.net/gh/0heartland0/clash@main/overwrite/conf/Overwrite-Yacd-IPv6-CDN.conf
```

#### 🔹 主路由IPv6用户 - Url-test -IPv6、低频拉取和 CDN 加速

```bash
https://testingcf.jsdelivr.net/gh/0heartland0/clash@main/overwrite/conf/Overwrite-Yacd-SlowUpdate-IPv6-CDN.conf
```

---

### 2️⃣ 配置环境变量

在 OpenClash 中启用覆写模块前，请根据需要设置以下环境变量：

#### ✴️ 必填变量 — 机场订阅链接
* 仅支持单一订阅，多机场用户建议搭配 Sub-Store 聚合后载入配置。

```bash
EN_KEY=你的机场订阅链接
```

配置完成后，**保存 → 应用配置重启即可**。  

---

## 说明

`SlowUpdate` 版本将代理提供者的订阅更新间隔设置为 `315360000` 秒，适合机场只提供临时订阅链接、平时不想频繁拉取节点的场景。需要更新节点时，重新填写新的 `EN_KEY` 后手动更新或重启 OpenClash。

`Yacd` 版本在策略组名称里加入 emoji，主要用于 Yacd 面板显示图标。Metacubexd、Zashboard、Dashboard 也可以使用。

`IPv6` 版本会开启：

```ini
IPV6_ENABLE = 1
IPV6_DNS = 1
IPV6_MODE = 3
ENABLE_V6_UDP_PROXY = 1
CHINA_IP6_ROUTE = 1
```

非 IPv6 版本保持：

```ini
IPV6_ENABLE = 0
IPV6_DNS = 0
```

配置文件默认使用 `fake-ip-mix + gvisor`：

```ini
EN_MODE = fake-ip-mix
STACK_TYPE = gvisor
```


## 💡 温馨提示

1. 仓库文件默认均使用 **GitHub 原始链接**，请确保路由器可正常访问 GitHub。  
2. 默认 OpenClash 不包含 **Geo 数据库**：
   * 建议手动提前更新 Geo 数据库。
   * 26/4/13  虽然当前yaml文件完全不依赖geo数据库运行但是依然建议保持数据库更新
3. 如未提前下载 GeoIP 数据库，初次运行可能提示 **内核错误**，多次重启后或手动下载数据库后即可恢复。  
4. `EN_KEY` 必须填写可直接访问的机场订阅链接。
5. 如果机场订阅链接过期，可能出现 `[Provider] Sub-store pull error: 401 Unauthorized`，需要重新获取临时订阅链接。
6. CDN 版只影响覆写配置文件下载地址，不会改变机场订阅链接。
7. 如果使用 Yacd 面板且希望看到图标，优先选择 `Yacd` 版本。
