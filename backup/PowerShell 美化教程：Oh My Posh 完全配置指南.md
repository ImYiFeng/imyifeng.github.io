## 0. 安装最新版 PowerShell

### 为什么需要升级？
- Windows 自带的 PowerShell 5.0 功能有限
- 新版 PowerShell 7+ 支持跨平台、性能优化和更多新特性

### 安装步骤：
1. 前往 [官方仓库](https://github.com/PowerShell/PowerShell) 下载最新稳定版
2. 安装完成后：
   - 按 `Win + S` 搜索「终端」
   - 打开「终端设置」→「启动」→「默认配置文件」→ 选择「PowerShell 7」
3. 验证版本：
   ```powershell
   $PSVersionTable.PSVersion
   ```

---

## 1. 安装 Oh My Posh

### 一键安装命令：
```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force
Invoke-Expression ((New-Object System.Net.WebClient).DownloadString('https://ohmyposh.dev/install.ps1'))
```

### 验证安装：
```powershell
oh-my-posh --version  # 显示版本号即成功
```

> 💡 提示：如果提示命令不存在，请重启终端或手动刷新环境变量

---

## 2. 配置 Nerd 字体

### 为什么需要特殊字体？
- **Nerd Fonts** 是集成了 2,000+ 图标的字体补丁
- 支持 Powerline 符号和开发常用图标（文件类型、Git 状态等）
- 普通编程字体无法显示这些特殊符号

### 安装步骤：
1. 前往 [Nerd Fonts 官网](https://www.nerdfonts.com/font-downloads) 下载
2. 解压后右键字体文件 →「安装」
3. 终端设置：
   - 打开「默认值」→「外观」→「字体」
   - 选择带有「NF」标识的字体（如 `MesloLGS NF`）

---

## 3. 基础主题配置

### 永久生效配置：
```powershell
# 允许执行本地脚本
Set-ExecutionPolicy RemoteSigned -Scope LocalMachine

# 创建/编辑配置文件
if (!(Test-Path $PROFILE)) {
    New-Item -Path $PROFILE -Type File -Force
}
notepad $PROFILE
```

### 配置文件内容：
```powershell
oh-my-posh init pwsh | Invoke-Expression
```

### 立即生效：
```powershell
. $PROFILE  # 重新加载配置
```

---

## 4. 主题定制指南

### 主题选择技巧：
1. 访问 [官方主题库](https://ohmyposh.dev/docs/themes) 预览效果
2. 推荐新手主题：
   - **jandedobbeleer**：信息全面，适合大屏
   - **quick-term**：紧凑型（笔者同款）

### 指定主题配置：
```powershell
# 修改配置文件内容为：
oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH/quick-term.omp.json" | Invoke-Expression
```