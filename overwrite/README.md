# 🌀 OpenClash_Overwrite 覆写模块

> 🧩 适配版本：**OpenClash v0.47.006 及以上**  
> 🧱 建议新装 **OpenClash** 用户使用，请勿修改任何 LuCI 设置  

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

#### 🔹 主路由用户 - Url-test【ipv6 写】

```bash
https://raw.githubusercontent.com/0heartland0/clash/main/overwrite/conf/Overwrite-ipv6.conf
```

#### 🔹 主路由无需 IPv6 用户 - Url-test

```bash
https://raw.githubusercontent.com/0heartland0/clash/main/overwrite/conf/Overwrite-Yacd.conf
```

---

### 2️⃣ 配置环境变量

在 OpenClash 中启用覆写模块前，请根据需要设置以下环境变量：

#### ✴️ 必填变量 — 机场订阅链接
* 仅支持单一订阅，多机场用户建议搭配Sub-store聚合后载入配置。

```bash
EN_KEY=你的机场订阅链接
```

配置完成后，**保存 → 应用配置重启即可**。  

---

## 💡 温馨提示

1. 仓库文件默认均使用 **GitHub 原始链接**，请确保路由器可正常访问 GitHub。  
2. 默认 OpenClash 不包含 **Geo 数据库**：
   * 建议手动提前更新 Geo 数据库。
   * 26/4/13  虽然当前yaml文件完全不依赖geo数据库运行但是依然建议保持数据库更新
3. 如未提前下载 GeoIP 数据库，初次运行可能提示 **内核错误**，多次重启后或手动下载数据库后即可恢复。  

---
