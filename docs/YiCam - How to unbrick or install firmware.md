## YiCam - How to unbrick or install firmware

> Camera Model - YDXJ01XY

### Steps

1. Unzip Z13-ELF.zip

2. Install drivers using DirectUSBII-Setup.exe

   Important: run the installation using adminstrator more, 
   This is because these are unsigned drivers, so run it in Admin mode.

3. Follow the installation steps in the 
   Z13 guidence for flashing the camera without disassembling.pptx

4. Install - autoexec.ash from `wifi_client_mode` in 
   https://github.com/ravisayal/Xiaomi_Yi_autoexec

5. Run `cc.exe` to connect 

   https://github.com/ravisayal/Xiaomi_Yi

   `Xiaomi Yi Camera Control&Configure GUI and via python scripts`

6. Connect to YiCam using telnet

```
# ps auxf |grep -v '\['
    1 root       0:02 init
  656 root       0:00 vffs /tmp/fuse_a -l a -o big_writes -o atomic_o_trunc -s
  659 root       0:00 vffs /tmp/fuse_d -l d -C 1 -o big_writes -s
  662 root       0:00 vffs /tmp/fuse_z -l z -s
  677 root       0:00 ombra
  681 root       0:00 amba_mq_handler
  682 root       0:00 /usr/bin/AmbaStreamSVC
  688 root       0:00 /usr/bin/lu_lnxfio_stream
  690 root       0:00 /usr/bin/amba_qrconfig
  747 root       0:00 telnetd
  754 root       0:00 network_message_daemon
  764 root       0:01 /usr/local/share/script/bsa_server -d /dev/ttyS1 -p /usr/local/share/script/bcm4330.hcd -u /tmp/fuse/ -all=0
  768 root       0:00 lu_example_util
  770 root       0:03 i_example_util
  782 root       0:00 AmbaOnDemandRTSPServer
  784 root       0:00 -/bin/sh
  787 root       0:00 cgiBridge
  791 root       0:00 /usr/local/share/script/app_manager
  792 root       0:00 /usr/local/share/script/app_ble
  793 root       0:06 /usr/local/share/script/app_hh
  961 root       0:00 /usr/bin/wpa_supplicant -Dnl80211 -iwlan0 -c/tmp/fuse_d/wifi/wpa_supplicant.conf -B
  970 root       0:00 udhcpc -i wlan0 -A 2 -b -t 30
  973 root       0:00 -sh
  993 root       0:00 cherokee-worker -a -C /etc/cherokee.conf -j -s -d
 1002 root       0:00 ps auxf

```
> rtsp process : `AmbaOnDemandRTSPServer`

> webserver process :  `cherokee-worker -a -C /etc/cherokee.conf -j -s -d`

