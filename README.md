# c8812
install linux to huawei c8812 android device

# 注意 NOTE
为android设备安装linux的原理和方法是通用的，但该仓库目前仅仅测试设备huawei c8812

# 快速体验 
从RAM中启动linux，直到加载rootfs， 由于zImage文件烧写到RAM中，因此并不会破坏原有的android系统。

## 特点（features)
- 使能了framebuffer console， 因此通过屏幕能够看到kernel的大部分启动信息， 源码后续上传
- rootfs采用debain，字符终端模式已经测试成功，后续上传
- 使能了usb虚拟串口，能够通过usb虚拟串口登录，测试成功，后续上传
- adb，adbd还未移植， 桌面系统， wifi，蓝牙等还未调试，后续再说

## 方法（methods)
1. 切换c8812设备到bootloader模式
	关机状态下，同时按住音量-和电源键，保持10秒钟，确认屏幕停留在logo状态后，USB连接手机和电脑。
2. 从内存中启动zImage
	cd c8812-bin
	sudo fastboot -b 0x00200000 boot zImage

## 备注
如果你有自己现成的rootfs， 可以将其存放到SD卡， 例如我的存放在SD卡的第二个分区，分区类型为ext4,然后使用如下命令就可以成功挂载rootfs
	cd c8812-bin
	sudo fastboot -c "root=/dev/mmcblk1p2" -b 0x00200000 boot zImage
