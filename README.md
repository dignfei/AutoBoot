# AutoBoot

支持文件复制、删除、剪切、重命名、编辑、查看等操作，集成文本编辑器和文件预览；文件写入操作受分区格式限制。支持浏览 ntfs ReFS  ext 等任意分区，启动 efi/img/iso/wim/vhdx 等绝大多数文件、任意包含操作系统的分区。 无需手写菜单无需编辑 bcd文件。
**把硬盘变成启动工具箱，系统、PE、镜像集中管理。**

AutoBoot 自动扫描硬盘上的 Windows 和 ISO、WIM、VHD/VHDX、EFI 文件，生成启动菜单。支持 Legacy BIOS / x64 UEFI，自带资源管理器、文件预览和自定义动态背景。


## 下载

进入本仓库的 [**Releases**](https://github.com/dignfei/AutoBoot/releases/latest) 页面下载：

| 文件 | 用途 |
| --- | --- |
| `AutoBoot-BCD-release.zip` | 安装到已有 Windows 启动菜单 |
| `AutoBoot-BIOS-UEFI.iso` | 虚拟机光驱或刻录光盘启动 |

## 安装

1. 解压 `AutoBoot-BCD-release.zip`。
2. 将整个 `AutoBoot` 文件夹复制到电脑**实际启动分区的根目录**。
3. 在这台电脑已安装的 Windows 中，右键 `AutoBoot\Install-BootMenu.bat`，选择**以管理员身份运行**。
4. 重启，在 Windows 启动菜单中选择 AutoBoot。

> UEFI 通常放在 ESP 分区，BIOS 通常放在系统保留分区或含有 `bootmgr` 的分区，不一定是 C 盘。隐藏分区需要先挂载再复制；安装脚本不会自动挂载分区或复制文件。

安装会添加或更新本工具的启动菜单项，保留原有 Windows 引导文件，不修改默认启动项和等待时间。

**ISO 用法：**将 ISO 挂载到虚拟机 DVD，或刻录成光盘后从光驱启动，无需安装。该 ISO 不保证直接原始写入 U 盘后可启动。

## 使用

将镜像放到可读取分区的**根目录或第一层文件夹**，例如：

```text
D:\WinPE.iso
D:\ISO\Windows.iso
E:\VHD\Win11.vhdx
```

进入 AutoBoot 后选择对应条目即可。更深目录中的文件，可通过**资源管理器**手动查找。

- 默认启动不成功时，将“镜像操作”切换到**先选方式**，选择其他适用的启动方式。
- 增删镜像或接入硬盘后，选择**重新扫描**。
- 方向键选择，回车执行，Esc 返回；资源管理器中按 **F7** 返回自动菜单。
- UEFI 图形菜单支持鼠标选择和点击，能否使用取决于主板固件。

## 自定义背景

将 PNG、JPG、JPEG、GIF 图片放进 `AutoBoot\background\`，支持中文文件名和 GIF 动画。进入菜单随机选图，停留时每 10 秒自动轮换。

ZIP 安装版可直接增删图片；修改 ISO 内的背景需要重新制作 ISO。

## 升级

先移走旧的 `AutoBoot` 文件夹，再复制新版完整文件夹，重新以管理员身份运行新版 `Install-BootMenu.bat`。请勿直接合并覆盖，以免旧配置残留。

## 兼容性与反馈

支持 Legacy BIOS 和 x64 UEFI，支持启动绝大多数文件，Secure Boot 不在当前支持范围内。

遇到问题请在 Issues 中提供：电脑或虚拟机型号、BIOS/UEFI 模式、安装方式、镜像名称、分区格式，以及报错照片或复现步骤。
