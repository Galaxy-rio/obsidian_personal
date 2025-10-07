---
tags:
  - iSH
  - proxy
title: iSH配置代理
created: 2025-10-05 15:51:26
modified: 2025-10-07 09:39:46
status: Done
类别: "[[../Tutorials|Tutorials]]"
cssclasses:
  - tutorial
---

# iSH配置代理

## 查看代理软件本地代理

在 Shadowrocket 里找到要用的“本地代理”地址/端口。Shadowrocket 会显示一个 Server IP 和 Port 例如 `127.0.0.1:1082`。

## 在 iSH 里设置环境变量

把 `IP:PORT` 换成 Shadowrocket 显示的那个。

```sh
# 临时立即生效（当前 shell）
export http_proxy="http://IP:PORT"
export https_proxy="http://IP:PORT"
export HTTP_PROXY="$http_proxy"
export HTTPS_PROXY="$https_proxy"
# 如果要让内网或 localhost 不走代理
export no_proxy="localhost,127.0.0.1,::1"
export NO_PROXY="$no_proxy"
```

## 针对某些特定工具

###### curl

```sh
curl --proxy http://IP:PORT https://example.com
```

###### git

```sh
git config --global http.proxy http://IP:PORT
git config --global https.proxy http://IP:PORT
```
