## 1. 跳过联网
- 安装系统时请不要联网，如果插入了网线，请拔掉。
- 安装完系统进入自定义开箱体验(OOBE)界面后，一路下一步到“让我们为你连接到网络”界面。
- 按 `Shift + F10`（注：部分笔记本需要 `Shift + Fn + F10`），打开命令提示符。
- 输入 `OOBE\BypassNRO.cmd`，按下回车，会自动重启。
- 重启后，则会出现“我没有 Internet 连接”选项，使用此选项即可跳过联网使用本地账户进入系统。

## 2. 禁用更新
### 方法一：使用 Optimizer 软件
- 开源地址：[https://github.com/hellzerg/optimizer](https://github.com/hellzerg/optimizer)
- 下载进入软件后选择上方“Windows11”选项卡，在“Windows Update”选项类别下勾选所有选项，即可禁用 Windows 更新。

### 方法二：使用组策略编辑器（仅适用于专业版、企业版系统）
这里提供两种方法，请任选其一
#### 彻底禁用更新
- 按下 `Win + R` 键，输入 `gpedit.msc`，按回车，进入组策略编辑器。
- 在左侧树形结构中，找到“计算机配置” -> “管理模板” -> “Windows 组件” -> “Windows 更新” -> “管理最终用户体验”。
- 双击“配置自动更新”，将其改为“已禁用”。
- 双击“删除使用所有 Windows 更新功能的访问权限”，将其改为“已启用”。

#### 限制更新特定版本
- 操作同上，进入“管理从 Windows 更新提供的更新”。
- 双击“选择目标功能更新版本”，更改为“已启用”。
- 在下方填入目标版本，例如，在第一个输入框填入“Windows 11”，第二个输入框输入“23H2”，即可限制更新到 23H2 版本，无法更新到更新版本。

## 3. 数字激活
- 开源地址：[https://github.com/massgravel/Microsoft-Activation-Scripts](https://github.com/massgravel/Microsoft-Activation-Scripts)
- 右键任务栏 Windows 徽标，选择“终端管理员”或者“Powershell 管理员”，以管理员权限运行 PowerShell。
- 若运行的为命令提示符（cmd），在 cmd 中输入 `powershell`，再按回车，即可进入 PowerShell。
- 在 PowerShell 中输入：
```powershell
irm https://get.activated.win | iex
```
- 按下回车，等待一段时间，可以看到运行了 Microsoft Activation Scripts。
- 按照提示输入 `1`，即可数字激活（HWID 激活）Windows 系统。