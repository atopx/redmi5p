# Redmi 5Plus Liunx(PostmarketOS) Installation Tutorial

### Setup 1 unlock bootloader
>  Reference: [https://www.miui.com/unlock/index.html](https://www.miui.com/unlock/index.html)
>
> Notice1: `miflush_unlock` requires a windows os
> 
>  Notice2: If the unlock tool does not recognize the phone, you need to install the driver manually in the device manager, select the path miflush_unlock/driver.

1. Download Xiaomi Official Unlock Tool (`miflush_unlock`): [https://www.miui.com/unlock/download.html](https://www.miui.com/unlock/download.html)
2. Run miflush_unlock.exe, login to Xiaomi account
3. Go to "Settings -> Developer Options -> Device Unlocked Status" to bind your xiaomi account and device.
4. Enter Bootloader mode manually (after powering off the computer, press and hold the Power On and Volume Down buttons at the same time).
5. Connect your phone via USB and click the "Unlock" button


### Setup 2 Download android sdk

> [https://developer.android.google.cn/tools/releases/platforms?hl=en](https://developer.android.google.cn/tools/releases/platforms?hl=en)
> 
> macos can be installed using homebrew, `brew install android-platform-tools`

1. Download android platform-tools
2. Configuring Environment Variables

### Setup 3 Download PostmarketOS images

> https://images.postmarketos.org/bpo/v23.12/xiaomi-vince/phosh/20240327-0824/
> Decompression command: `xz --decompress xxx.xz`
1. 20240327-0824-postmarketOS-v23.12-phosh-22.3-xiaomi-vince-boot.img.xz
2. 20240327-0824-postmarketOS-v23.12-phosh-22.3-xiaomi-vince-lk2nd.img.xz
3. 20240327-0824-postmarketOS-v23.12-phosh-22.3-xiaomi-vince.img.xz



### Setup 4 Write images to phone
> Notice: Run `fastboot devices` to make sure your device is detected.

```
# 1. flush lk2nd 
fastboot flash boot 20240327-0824-postmarketOS-v23.12-phosh-22.3-xiaomi-vince-lk2nd.img
# 2. wait for the reboot to complete
fastboot reboot
# 3. flush boot
fastboot flash boot 20240327-0824-postmarketOS-v23.12-phosh-22.3-xiaomi-vince-boot.img
# 4. flush os
fastboot flash userdata 20240327-0824-postmarketOS-v23.12-phosh-22.3-xiaomi-vince.img
# 5. wipe the system partition
fastboot erase system
# 6. reboot
fastboot reboot
```

If all goes correctly, you should now be running postmarketOS! Enjoy!

### Setup 5 Login your OS
username: user
password: 147147
PIN: 147147


### Finally

**Replace `/etc/apk/repositories` with the following**
```
http://mirrors.tuna.tsinghua.edu.cn/postmarketOS/master
http://mirrors.tuna.tsinghua.edu.cn/alpine/edge/main
http://mirrors.tuna.tsinghua.edu.cn/alpine/edge/community
```

**Update Mirror**
```
sudo apk update
sudo apk upgrade -a
```
