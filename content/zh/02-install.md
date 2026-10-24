---
title: 安装与启动
description: Windows / macOS / 源码三种装法，第一次配模型，与 SLATE 同机共存时的端口分配
section: 开始
order: 2
---

## 装

### Windows

下载 `SLATE-Teams-Setup-<版本>.exe`，双击装完从桌面图标启动。默认装到当前用户的
`AppData\Local\Programs\SLATE Teams`，不需要管理员权限。

装完第一次启动会打开一个本地窗口，界面就是 [六个页签](./03-interface.md)。

### macOS

发行版给的是 `SLATE Teams.app` 与 `SLATE-Teams-Setup-<版本>.dmg`；从源码跑用仓库里的
`build_macos.sh` 打包，或者 `python desktop.py` 直接起（见下面「源码」）。
装机版的数据目录不在应用包里，而在 `~/Library/Application Support/SLATE Teams`。

:::note 第一次打开被拦
未签名的包会被 Gatekeeper 拦一下。在「系统设置 → 隐私与安全性」里点「仍要打开」，
只需要做一次。
:::

### 源码

```
git clone <仓库地址>
cd SLATE_Teams
pip install -r requirements.txt
python desktop.py
```

`desktop.py` 会自己起后端、自己开窗口；只想拿接口给别的浏览器用，用
`python backend/main.py` 起后端，然后开 `http://127.0.0.1:<端口>/`。

## 第一次配模型

设置 → 模型/上下文 里填一家厂商的 API Key，选一个默认模型，就能开了。
Key 只写进本机 `data/desktop_state.json`，不会出现在任何一条对外请求里，也不进备份。

:::danger 备份里有你的 Key
导出的备份把整份本机状态一起打进去，**其中包含模型 API Key（明文）**。
所以备份文件等同于一串钥匙：不要上传到网盘、不要贴进 issue、不要发给别人。
要分享问题现场，只截界面图、只贴日志。
:::

## 与 SLATE 同机共存

两个产品可以在同一台机器上并存，互不覆盖：

| | 应用端口 | 数据 |
| --- | --- | --- |
| SLATE | 各自的默认口 | 自己的安装目录 `data/` |
| SLATE Teams | 首选 8130（被占则顺延） | 自己的安装目录 `data/` |

安装器身份、开始菜单项、更新源都是分开的，所以不会出现"装了 Teams 把 SLATE 的自动更新接走"。

## 起不来先看这两处

1. **端口被占**：日志 `data/desktop_backend.log` 里会写它实际拿到的端口。
2. **依赖没装全**：源码跑最常见，报错会直接说缺哪个包。

更多在 [常见问题](./15-faq.md)。
