Windows 和 Linux 系统时间不一致通常是因为两者对硬件时钟的处理方式不同。Windows 将硬件时钟（RTC）视为本地时间，而 Linux 默认将其视为 UTC 时间。以下是解决方法：

### 方法一：让 Linux 使用本地时间
1. **编辑配置文件**  
   在 Linux 中打开终端，编辑 `/etc/adjtime` 文件：
   ```bash
   sudo nano /etc/adjtime
   ```
   将 `UTC` 改为 `LOCAL`。

2. **更新硬件时钟**  
   保存并退出后，运行以下命令更新硬件时钟：
   ```bash
   sudo hwclock --systohc
   ```

3. **重启系统**  
   重启后，时间应保持一致。

### 方法二：让 Windows 使用 UTC 时间
1. **修改注册表**  
   在 Windows 中按 `Win + R`，输入 `regedit`，打开注册表编辑器。  
   找到路径：
   ```
   HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation
   ```
   右键新建一个 `DWORD (32-bit) Value`，命名为 `RealTimeIsUniversal`，并将其值设为 `1`。

2. **重启系统**  
   重启后，Windows 会将硬件时钟视为 UTC 时间。

### 方法三：手动同步时间
1. **在 Linux 中同步时间**  
   使用以下命令同步时间：
   ```bash
   sudo timedatectl set-ntp true
   ```

2. **在 Windows 中同步时间**  
   打开“设置” -> “时间和语言” -> “日期和时间”，启用“自动设置时间”。

### 总结
- **方法一**：Linux 使用本地时间。
- **方法二**：Windows 使用 UTC 时间。
- **方法三**：手动同步时间。

选择适合你的方法即可解决时间不一致问题。