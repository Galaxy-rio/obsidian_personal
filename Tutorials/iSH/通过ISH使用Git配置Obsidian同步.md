---
tags:
  - iSH
  - Git
  - Tutorial
---

# 通过 iSH 使用 Git 配置 Obsidian 同步

## 前置操作

- 在 PC 上完成配置并同步至 Git 服务器。
- 在 iOS 设备上新建空的 Obsidian 仓库。

## 安装 Git

安装 Git 并配置 Git 用户信息。

```sh
apk update
apk add git

git config --global user.name "username"
git config --global user.email "email@example.com"
```

## 配置 Git 服务端

授权 HTTPS 并生成 Personal Access Token。

### GitHub

- 打开 GitHub/`Settings`/`Developer settings`/`Personal access tokens`/`Tokens (classic)`/`Generate new token`
- 权限勾选 `repo`
- 保存 token
### Gitee

- 登录 Gitee/`设置`/`安全设置`/`私人令牌`/`生成新令牌`
- 勾选 `仓库管理` 权限
- 保存 token

## 挂载 Obsidian 笔记文件夹

在 iOS/iPadOS 设备上，一个软件无法直接读取另一个软件的文件夹数据。好在 iSH 提供了挂载的功能，可以将系统中的 Documents/Obsidian 挂载到 iSH 中。

```sh
mkdir -p ~/obsidian
mount -t ios ~/Documents/Obsidian ~/obsidian
```

执行命令后会弹出系统页面来选择具体要挂载的目录，此时需选择到 obsidian 中具体仓库的目录而不是 obsidian 根目录。  
完成后移动到对应目录。

```sh
cd ~/obsidian
```

## 配置 Git

```sh
# 初始化 Git 仓库
git init
git branch -M main

# 添加远程仓库
git remote add origin https://github.com/username/obsidian-notes.git
```

可能遇到的问题：[[#Git “dubious ownership” 警告]]

## 拉取仓库

```sh
git pull origin main --allow-unrelated-histories
```

可能遇到的问题：[[#Git “未跟踪文件冲突” 错误]]

此时打开 Obsidian 理论上已经可以看到完整仓库了，稍后在 Obsidian-Git 插件设置中找到 `Authentication`/`commit author`，补全信息即可实现后续自动同步。

---

## 问题

### Git: “dubious ownership” 警告
###### 错误信息
```sh
fatal: detected dubious ownership in repository at '/root/obsidian'
```

意思是 Git 认为你当前仓库所在的目录 `/root/obsidian` 的 **所有者和运行 Git 的用户不一致**（因为挂载 iOS 文件夹后，文件的所有者通常是 root 或其他 UID），为了安全默认不允许操作。
###### 解决方法
```sh
git config --global --add safe.directory /root/obsidian
```

### Git: “未跟踪文件冲突” 错误
###### 错误信息
```sh
error: The following untracked working tree files would be overwritten by merge:
        .obsidian/app.json
        ...
Please move or remove them before you merge.
Aborting
```

###### 解决方法

保留远程仓库并覆盖本地

```sh
# 强制重置工作区，丢弃本地未跟踪文件
git fetch origin
git reset --hard origin/main

# 删除未跟踪文件
git clean -fd
```

执行后本地所有未保存的更改会丢失。