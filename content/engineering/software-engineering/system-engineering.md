+++
title = "System Engineering"
author = ["Shawn Dennis Lin"]
date = 2021-09-09T00:00:00+08:00
draft = false
+++

## Linux {#linux}

-   [Linux目錄結構](http://linux-wiki.cn/wiki/zh-tw/Linux%E7%9B%AE%E5%BD%95%E7%BB%93%E6%9E%84)
-   [為什麼伺服器要選擇 Linux](https://kknews.cc/zh-tw/code/ggepgbe.html)
-   [使用 SysRq 鍵讓當機的 Linux 安全地重新開機](https://blog.gtwang.org/linux/safe-reboot-of-linux-using-magic-sysrq-key/)


### Command {#command}

| man                         | command                                             | describe                                                       | Ref                                                                                                              |   |
|-----------------------------|-----------------------------------------------------|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------|---|
| User                        |                                                     |                                                                |                                                                                                                  |   |
| `adduser`, `addgroup`       |                                                     | add a user or group to the system                              |                                                                                                                  |   |
|                             | --disabled-password                                 |                                                                |                                                                                                                  |   |
| `chown`                     | `chown -R <user>:<group> <folder_1> ... <folder_n>` | Chown User and Group Recursively                               | [How To Chown Recursively on Linux](https://devconnected.com/how-to-chown-recursive-on-linux/)                   |   |
| `passwd`                    |                                                     |                                                                |                                                                                                                  |   |
| `groups`                    |                                                     | print the groups a user is in                                  |                                                                                                                  |   |
|                             | `sudo usermod -a -G <GROUP> <yourusername>`         | Add your user to <GROUP> group                                 |                                                                                                                  |   |
|                             | `gpasswd -d <user> <group>`                         | remote <group> from <user>                                     |                                                                                                                  |   |
| `userdel`                   | `userdel [options] LOGIN`                           | delete a user account and related files (need to use `sudo -`) | [移除 Linux 使用者](https://tw.godaddy.com/help/linux-19158)                                                     |   |
|                             | `userdel -r <user>`                                 |                                                                |                                                                                                                  |   |
|                             |                                                     |                                                                |                                                                                                                  |   |
| System                      |                                                     |                                                                |                                                                                                                  |   |
| `lsof`                      |                                                     | list open files                                                |                                                                                                                  |   |
|                             | `sudo lsof -i -P -n ¦ grep LISTEN`                  | check if port is in use in                                     |                                                                                                                  |   |
|                             | `sudo netstat -tupln ¦ grep LISTEN`                 |                                                                |                                                                                                                  |   |
| `df`                        |                                                     | report file system disk space usage                            |                                                                                                                  |   |
|                             | `df -h`                                             | print sizes in powers of 1024 (e.g., 1023M)                    |                                                                                                                  |   |
|                             | `sodu df -sh [path]`                                | Get the Size of a Directory                                    |                                                                                                                  |   |
| `mount`                     |                                                     | mount a filesystem                                             |                                                                                                                  |   |
| `umount`                    |                                                     | unmount file systems                                           |                                                                                                                  |   |
| `fdisk`                     | `fdisk [options] device`                            | manipulate disk partition table                                |                                                                                                                  |   |
|                             | `fdisk -l [device...]`                              | list disk                                                      |                                                                                                                  |   |
| `mkfs`                      |                                                     | build a Linux filesystem                                       |                                                                                                                  |   |
| `e2label`                   | `e2label device [ volume-label ]`                   | Change the label on an ext2/ext3/ext4 filesystem               |                                                                                                                  |   |
| `lsblk`                     |                                                     | list block devices                                             |                                                                                                                  |   |
| `parted`, `dd`, `mkfs.ext4` |                                                     |                                                                | [Format USB Drives and SD Cards](https://linuxize.com/post/how-to-format-usb-sd-card-linux/)                     |   |
| `mlabel`                    | `sudo mlabel -i /dev/sdb1 -s ::"LABEL HERE "`       | change a USB stick name                                        | [change a USB stick name](https://superuser.com/a/1022998)                                                       |   |
| `apt`, `dpkg`               |                                                     |                                                                | [一些套件相關的技巧](https://samwhelp.github.io/book-ubuntu-basic-skill/book/content/package/index.html)         |   |
| `timedatectl`               | `timedatectl list-timezones`                        |                                                                |                                                                                                                  |   |
|                             | `sudo timedatectl set-timezone Asia/Taipei`         |                                                                | [How to Set or Change the Time Zone in Linux](https://linuxize.com/post/how-to-set-or-change-timezone-in-linux/) |   |
| file                        |                                                     |                                                                |                                                                                                                  |   |
| `tail`                      |                                                     | output the last part of files                                  |                                                                                                                  |   |
| `dd`                        |                                                     | convert and copy a file                                        |                                                                                                                  |   |
| `find`                      |                                                     | search for files in a directory hierarchy                      | [linux-find(TW)](https://blog.miniasp.com/post/2010/08/27/Linux-find-command-tips-and-notice)                    |   |
|                             | `sudo find / -iname 'filename' -type f`             |                                                                |                                                                                                                  |   |
|                             | `sudo find / -iname 'dirname' -type d`              |                                                                |                                                                                                                  |   |
| `rsync`                     | `rsync [OPTION...] SRC... [DEST]`                   | a fast, versatile, remote (and local) file-copying tool        |                                                                                                                  |   |
|                             | `rsync -avh --del SRC DEST --exclude='path'`        |                                                                |                                                                                                                  |   |
|                             | `rsync --info=progress2 source dest`                | copy with progress bar                                         |                                                                                                                  |   |
| `wget`                      |                                                     | The non-interactive network downloader.                        |                                                                                                                  |   |
|                             | `wget <uri> -P /path/to/folder`                     | path of file                                                   |                                                                                                                  |   |
|                             | `wget <uri> -O /path/to/file.ext`                   | path of dictionary                                             |                                                                                                                  |   |
| `chmod`                     | `find . -type d -print0 ¦ xargs -0 chmod 755`       | chmod all folder mode to 755                                   |                                                                                                                  |   |
|                             | `find . -type f -print0 ¦ xargs -0 chmod 644`       | chmod all file mode to 644                                     |                                                                                                                  |   |
|                             |                                                     |                                                                |                                                                                                                  |   |
| server                      |                                                     |                                                                |                                                                                                                  |   |
| `nslookup`                  | `nslookup [-option] [name ¦ -] [server]`            |                                                                | [Nslookup](https://code.yidas.com/nslookup/)                                                                     |   |
|                             | `nslookup -type=any domain.com`                     |                                                                |                                                                                                                  |   |
| network                     |                                                     |                                                                |                                                                                                                  |   |
| `nc`                        |                                                     |                                                                | [Netcat（Linux nc 指令）網路管理者工具實用範](https://blog.gtwang.org/linux/linux-utility-netcat-examples/)      |   |
|                             |                                                     |                                                                |                                                                                                                  |   |


#### journalctl {#journalctl}

| command                       | describe | Ref |   |
|-------------------------------|----------|-----|---|
| By Unit                       |          |     |   |
| `journalctl -u nginx.service` |          |     |   |


#### grep {#grep}

| command   | describe | Ref |   |
|-----------|----------|-----|---|
| `grep -C` |          |     |   |


### System {#system}


#### Locales & Language pack {#locales-and-language-pack}

```sh
sudo apt install -y locales locales-all

sudo apt install -y locales
sudo localedef -i zh_TW -f UTF-8 zh_TW.UTF-8
sudo localedef -i en_US -f UTF-8 en_US.UTF-8
sudo update-locale

```

-   [Linux字符集和系统语言设置-LANG,locale,LC\_ALL,POSIX等命令及参数详解](https://blog.csdn.net/weixin%5F33695082/article/details/92792632)
-   [How to Change or Set System Locales in Linux](https://www.tecmint.com/set-system-locales-in-linux/)


### Systemd {#systemd}

-   [Systemd 定时器教程](https://www.ruanyifeng.com/blog/2018/03/systemd-timer.html)


### Action {#action}


#### Format SD card {#format-sd-card}

-   [Format an sd card to fat32 in linux using fdisk](https://ragnyll.gitlab.io/2018/05/22/format-a-sd-card-to-fat-32linux.html)


#### Rename a volume {#rename-a-volume}

-   [Rename a volume](https://superuser.com/a/582998)


#### Change login background {#change-login-background}

1.  find
2.  

<!--listend-->

-   <https://vitux.com/how-to-change-login-lock-screen-background-in-ubuntu/>


#### SMB server {#smb-server}


### Problem {#problem}


#### -bash: sudo: command not found {#bash-sudo-command-not-found}

<https://unix.stackexchange.com/a/425664>  


#### Fix apt-get update “the following signatures couldn’t be verified because the public key is not available” {#fix-apt-get-update-the-following-signatures-couldn-t-be-verified-because-the-public-key-is-not-available}

-   [Fix apt-get update “the following signatures couldn’t be verified because the public key is not available”](https://chrisjean.com/fix-apt-get-update-the-following-signatures-couldnt-be-verified-because-the-public-key-is-not-available/)


#### crontab {#crontab}

-   [Linux 設定 crontab 例行性工作排程教學與範例](https://blog.gtwang.org/linux/linux-crontab-cron-job-tutorial-and-examples/)
-   [corntab log](https://askubuntu.com/questions/56683/where-is-the-cron-crontab-log)


### WSL {#wsl}


#### Problem {#problem}

<!--list-separator-->

-  release disk space back to the host OS

    `In Posershell`  
    
    ```sh
    wsl --shutdown
    cd "<dir>" # example C:\Users\shawn\AppData\Local\Packages\CanonicalGroupLimited.Ubuntu20.04onWindows_79rhkp1fndgsc\LocalState
    optimize-vhd -Path .\ext4.vhdx -Mode full
    ```
    
    Ref: <https://github.com/microsoft/WSL/issues/4699>  

<!--list-separator-->

-  Access a localhost running in Windows from inside WSL2

    Get IP address in cmd: `ipconfig /all`  
    windows host: `C:\Windows\System32\drivers\etc\hosts`  
    Ref: [Access a localhost running in Windows from inside WSL2?](https://stackoverflow.com/a/66504604)  

<!--list-separator-->

-  localhostForwarding

    create a file called `.wslconfig` in `C:\Users<your_username>.wslconfig`  
    
    ```sh
    [wsl2]
    localhostForwarding=true
    ```
    
    Ref: [Access a localhost running in Windows from inside WSL2?](https://stackoverflow.com/a/65910122)  


### Kali Linux {#kali-linux}


#### OS information {#os-information}

`neofetch`  

```nil
..............                                     shdennlin@shdennlinLnb 
            ..,;:ccc,.                             ---------------------- 
          ......''';lxO.                           OS: Kali GNU/Linux Rolling x86_64 
.....''''..........,:ld;                           Host: 81LK IdeaPad L340-15IRH Gaming 
           .';;;:::;,,.x,                          Kernel: 5.14.0-kali2-amd64 
      ..'''.            0Xxoc:,.  ...              Uptime: 36 mins 
  ....                ,ONkc;,;cokOdc',.            Packages: 3316 (dpkg), 4 (snap) 
 .                   OMo           ':ddo.          Shell: zsh 5.8 
                    dMc               :OO;         Resolution: 1920x1080, 1920x1080 
                    0M.                 .:o.       DE: Plasma 5.23.2 
                    ;Wd                            WM: KWin 
                     ;XO,                          Theme: Kali-Dark [Plasma], Breeze [GTK2/3] 
                       ,d0Odlc;,..                 Icons: Flat-Remix-Blue-Dark [Plasma], Flat-Remix-Blue-Dark [GTK2/3] 
                           ..',;:cdOOd::,.         Terminal: konsole 
                                    .:d;.':;.      CPU: Intel i5-9300H (8) @ 4.100GHz 
                                       'd,  .'     GPU: Intel CoffeeLake-H GT2 [UHD Graphics 630] 
                                         ;l   ..   GPU: NVIDIA GeForce GTX 1050 3 GB Max-Q 
                                          .o       Memory: 4166MiB / 15886MiB 
                                            c
                                            .'                             
                                             .                             
```


#### Install Nvidia driver {#install-nvidia-driver}

**Install**  

```sh
sudo apt update && sudo apt -y upgrade
sudo apt install -y nvidia-driver nvidia-cuda-toolkit
```

**Check**  

1.  lspci|grep VGA
2.  nvidia-smi
3.  xrandr
4.  lspci -v

Ref: <https://www.kali.org/docs/general-use/install-nvidia-drivers-on-kali-linux/>  


#### Display Configuration {#display-configuration}

1.  `$ sudo vi /etc/X11/xorg.conf` and add  
    
    ```conf
    Section "ServerLayout"
    Identifier "layout"
    Screen 0 "nvidia"
    Inactive "intel"
    EndSection
    
    Section "Device"
    Identifier "nvidia"
    Driver "nvidia"
    BusID  "PCI:1:0:0"
    EndSection
    
    Section "Screen"
    Identifier "nvidia"
    Device "nvidia"
    EndSection
    
    Section "Device"
    Identifier "intel"
    Driver "modesetting"
    Option "AccelMethod"  "uxa"
    EndSection
    
    Section "Screen"
    Identifier "intel"
    Device "intel"
    EndSection
    ```
    
    Ref: <https://github.com/Bumblebee-Project/Bumblebee/wiki/Multi-monitor-setup>

2.  Change display managers  
    `$ sudo dpkg-reconfigure gdm3` and select `sddm`  
    Ref: [什麽是gdm3，kdm，lightdm？如何安裝和刪除它們？](https://ubuntuqa.com/zh-tw/article/6577.html)

3.  add script after start sddm `$ sudo vi /usr/share/sddm/scripts/Xsetup` and add below  
    
    ```sh
    display1="HDMI-0"
    display2="eDP-1-1"
    
    xrandr --setprovideroutputsource modesetting NVIDIA-0
    xrandr --auto
    xrandr --output $display1 --mode 1920x1080 --primary
    xrandr --output $display2 --right-of $display1 --mode 1920x1080
    ```
    
    `NOTE`: You need to change display variable by your self, you can use `$ xrandr` to see your connected

4.  (Option) install `autorandr`  
    
    ```sh
    sudo apt install autorandr
    ```
    
    Ref: <https://github.com/phillipberndt/autorandr>


#### Snaps in application launcher (KDE) {#snaps-in-application-launcher--kde}

`$ sudo -E vi /etc/zsh/zprofile` and add add the following line:  

```sh
emulate sh -c 'source /etc/profile'
emulate sh -c 'source /etc/profile.d/apps-bin-path.sh'
```

Ref: <https://www.reddit.com/r/kde/comments/9pjos2/comment/eh0v1um/?utm%5Fsource=share&utm%5Fmedium=web2x&context=3>  


#### Snap Error {#snap-error}

ERROR:  

```sh
snap-confine has elevated permissions and is not confined but should be. Refusing to continue to avoid permission escalation attacks
```

Edit `/lib/apparmor/rc.apparmor.functions` and edit `ADDITIONAL_PROFILE_DIR=` to below:  

```sh
ADDITIONAL_PROFILE_DIR=/var/lib/snapd/apparmor/profiles/
```

Answer: <https://github.com/ubuntu/microk8s/issues/249#issuecomment-985227413>  


## Windows {#windows}


### Command {#command}

| man     | command                                              | describe          | Ref |
|---------|------------------------------------------------------|-------------------|-----|
| `netsh` | `netsh int ipv4 show excludedportrange protocol=tcp` | show wdinows port |     |