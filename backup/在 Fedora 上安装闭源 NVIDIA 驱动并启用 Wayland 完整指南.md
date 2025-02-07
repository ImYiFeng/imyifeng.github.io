## 一、环境准备

### 1. 检查显卡兼容性
```bash
lspci | grep -E "VGA|3D"
```
- 确认输出信息中包含 NVIDIA 显卡型号
- 访问 [NVIDIA 驱动下载页面](https://www.nvidia.cn/drivers/lookup/) 验证支持情况

### 2. 关闭独显直连（适用于双显卡笔记本）
- 请进入BIOS设置，不同厂商的设置方法不同，请自行查阅

### 3. 禁用安全启动
```bash
sudo mokutil --sb-state
```
- 若显示 `SecureBoot enabled` 需进入 BIOS/UEFI 关闭
- 常见关闭路径：Security → Secure Boot → Disable

### 4. 验证 Wayland 环境
```bash
sudo dnf list installed xorg-x11-server-Xwayland libxcb egl-wayland
```
- 若缺少组件，执行：
```bash
sudo dnf install xorg-x11-server-Xwayland libxcb egl-wayland
```

## 二、选择驱动并下载

| 驱动类型 | 适用场景                     | 更新周期      |
|----------|------------------------------|---------------|
| NFB      | 长期支持版（企业级）         | 2-3年         |
| LLB      | 旧显卡支持（Legacy）         | 不定期更新    |
| SLB      | 短期支持（推荐大多数用户）   | 每季度更新    |
| BETA     | 新功能测试（非生产环境使用） | 随新特性发布  |

*建议选择与内核版本最匹配的 SLB 驱动*
访问[NVIDIA 驱动下载页面](https://www.nvidia.cn/drivers/lookup/) 下载驱动

## 三、驱动安装流程

### 1. 给予安装程序权限
```bash
chmod +x NVIDIA-Linux-x86_64-*.run
```

### 2. 系统更新
```bash
sudo dnf update
reboot
```

### 3. 安装编译依赖
```bash
su -
dnf install @base-x kernel-devel kernel-headers gcc make dkms acpid libglvnd-glx libglvnd-opengl libglvnd-devel pkgconfig xorg-x11-server-Xwayland libxcb egl-wayland
```

### 4. 禁用 Nouveau 驱动
```bash
echo "blacklist nouveau" >> /etc/modprobe.d/blacklist.conf
echo "options nvidia NVreg_PreserveVideoMemoryAllocations=1" >> /etc/modprobe.d/nvidia.conf
echo "options nvidia-drm modeset=1 fbdev=1" >> /etc/modprobe.d/nvidia.conf
```

### 5. 更新引导配置
```bash
grub2-mkconfig -o /boot/grub2/grub.cfg
mv /boot/initramfs-$(uname -r).img /boot/initramfs-$(uname -r)-nouveau.img
dracut /boot/initramfs-$(uname -r).img $(uname -r)
```

### 6. 进入文本模式
```bash
systemctl set-default multi-user.target
reboot
```

## 四、编译安装驱动

### 1. 执行安装程序
```bash
su -
./NVIDIA-Linux-x86_64-*.run
```

### 2. 关键选项配置
1. **Multiple kernel module types are available for this system**: 
- 选择 `NVIDIA Proprietary`
3. **Install NVIDIA's 32-bit compatibility libraries?**: 
- 选择 `Yes`
5. **Would you lite to register the kernel module sources with DKMS?**: 
- 选择 `Yes`
7. **The initramfs will likely need to be rebuild due to the following conditon(s):**: 
- 选择 `Yes`
9. **Would you like to ruyn the nvidia-xconfig utility to automatically update your X configuration...**: 
- 选择 `Yes`

### 3. 恢复图形模式
```bash
systemctl set-default graphical.target && reboot
```

## 五、完成安装

### 1. 启动NVIDIA服务
```bash
su -
systemctl enable nvidia-suspend.service
systemctl enable nvidia-hibernate.service
systemctl enable nvidia-resume.service
```

### 2. 验证安装
```bash
nvidia-smi
```
- 应显示GPU状态
```bash
echo $XDG_SESSION_TYPE
```
- 应输出wayland