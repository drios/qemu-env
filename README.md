qemu-env
========

kompiled kernel and modules for qemu-system-arm and supported cpu - able to host standard RPI images (rasp, xbian, debian wheezy)

attached is script to start the VM. "$@" is to pass any other arguments, for example "-vnc IP:screen#" to export the video as vnc server available through network or localy. to get network in brigde mode, tap support through kernel module is needed + existing bridge interface (linux. for other platforms check docs). discs are emulated through emulated scsi (/dev/sdX).

initramfs is generated the standard xbian way from inside the VM. the only difference to standard RPI is kernel module versions mismash. the VM can be started with the standard initramfs.gz as well, but the modules will not start due to the mishmash. 

```
export QEMU_AUDIO_DRV=none
#-nographic -serial stdio 
qemu-system-arm "$@" -initrd /mnt/Public/xbian-boot/qemu/initramfs.gz -hda /mnt/Public/xbian/XBian1.0Alpha5.img.new  -cpu arm1176 -M  versatilepb -m 256  -net nic -net tap,ifname=tap9,script=/etc/qemu-ifup   -kernel /mnt/Public/xbian-boot/qemu/zImage -append "rw bcm2708_fb.fbwidth=1280 bcm2708_fb.fbheight=1024  dwc_otg.lpm_enable=0 kgdboc=ttyAMA0,115200 console=tty1 root=LABEL=xbian-root-btrfs,nodatacow,autodefrag,compress=lzo,relatime,noatime,thread_pool=3 rootwait rootfstype=btrfs ip=dhcp quiet "
```
