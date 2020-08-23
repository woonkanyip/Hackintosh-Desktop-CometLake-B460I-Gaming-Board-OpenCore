# Hackintosh-Desktop-CometLake-B460I-Gaming-Board-OpenCore

# 电脑硬件描述

 主板:  ASUS B460I Gaming
 CPU:  i5 10400
 内存:  海盗船RGB 8G*2
 显卡:  AMD RX560D 4G
 WIFI: BCM94360CS2
2. 安装盘的制作

 2.1 重要一点: 如果不知道USB的ID地址,只能用主板上的TypeC接口进行安排
     TpyeC接口建议外接转换器(最少要有两个USB口,要不然装完机后就没有USB口接键盘和鼠标)
     这个TpyeC口可以识别2.0的U盘和3.0的U盘
 2.2 安装OpenCore等相关请参考
     大神资料 https://github.com/dortania/OpenCore-Install-Guide/tree/master/installer-guide
 2.3 OpenCore的配置 请参考 
     大神资料:Config配件文件 CometLake
     https://github.com/dortania/OpenCore-Install-Guide/blob/master/config.plist/comet-lake.md
 2.4 选用KEXT时一定要加上 USBInjectAll 和 XHCI-unsupported
     USBInjectAll 是主要的USB驱动文件
     XHCI-unsupported 是USB空壳文件, 这个文件后期比较重要, 是驱动和定制USB的关键
     加上这两个文件后, 全部USB口基本能识别2.0的U盘及设备, 3.0的U盘和设备还是认不了, 要到后期进行定制
 2.5 用独显的朋友, 主板BIOS需更新到 0401版本, 
     这样才能在接了独显的情况下打开核显, 系统可以进行相关软硬件的加速功能
 2.6 教程制作的是恢复用的小型系统, 安装时需要联网下载安排包.
     如果用大容量的U盘制作安装盘时, 可以在制作U盘时可以直接下载完整的安装包进行制作.
3. 系统安装

 3.1 BIOS 设置, 教程比较多, 请查阅大神资料
 3.2 这主板安装时, VT-D的打开和关闭对安装的系统的系统的运行不影响, 只是VT-D打开后, 系统加载时间慢一些.
 3.3 安装步骤就是那几项，具体不详细说明。如有出错就按网上教程自行排错一下。
4. USB定制

 4.1 USB定制需要用到 Hackintool软件。
 4.2 打开Hackintool软件后点击USB项，这时会出现本机的USB端口。记录下类型为XHC设备ID。
     如华硕B460I-Gaming主板的设备ID是 0xA3AF, 芯片组显示为 300
 4.3 记录下这两个内容后打开XHCI-unsupported KEXT。方法为 右键选显示包内容，双击Contents，使用Plist软件打开info.plist
     (我是直接用ProperTree打开的，因为配置config时已下载，就直接用起来)
     在info.plist中有一栏是300芯片组是，其中已有常用的USB设备ID，在这下栏中加入之前的设备ID 0xA3AF，保存重启后就可以认出
     USB 3.0的U盘。
 4.4 定制黑苹果的USB端口
     网上很多黑苹果的大神都说，USB端口超过15个会影响其他功能
     (其中就有休眠功能，反正我是长期开着高性能的主，对我没什么用。定制就定制呗)。
     根据需要进定制，端口少于或等于15个，定制完毕导出，得到一个USBPORT.KEXT。
     将USBPORT.KEXT复制到OpenCore的Kexts中，并重新关联一下config配置文件。
