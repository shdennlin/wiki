+++
title = "System Engineering"
author = ["Shawn Dennis Lin"]
date = 2021-09-09T00:00:00+08:00
draft = false
+++

## Linux {#linux}

-   [Linux目錄結構](http://linux-wiki.cn/wiki/zh-tw/Linux%E7%9B%AE%E5%BD%95%E7%BB%93%E6%9E%84)
-   [為什麼伺服器要選擇 Linux](https://kknews.cc/zh-tw/code/ggepgbe.html)


### Command {#command}

| man                   | command                                             | describe                                                       | Ref                                                                                            |
|-----------------------|-----------------------------------------------------|----------------------------------------------------------------|------------------------------------------------------------------------------------------------|
| User                  |                                                     |                                                                |                                                                                                |
| `adduser`, `addgroup` |                                                     | add a user or group to the system                              |                                                                                                |
|                       | --disabled-password                                 |                                                                |                                                                                                |
| `chown`               | `chown -R <user>:<group> <folder_1> ... <folder_n>` | Chown User and Group Recursively                               | [How To Chown Recursively on Linux](https://devconnected.com/how-to-chown-recursive-on-linux/) |
| `passwd`              |                                                     |                                                                |                                                                                                |
| `groups`              |                                                     | print the groups a user is in                                  |                                                                                                |
|                       | `sudo usermod -a -G <GROUP> <yourusername>`         | Add your user to <GROUP> group                                 |                                                                                                |
|                       | `gpasswd -d <user> <group>`                         | remote <group> from <user>                                     |                                                                                                |
| `userdel`             | `userdel [options] LOGIN`                           | delete a user account and related files (need to use `sudo -`) | [移除 Linux 使用者](https://tw.godaddy.com/help/linux-19158)                                   |
|                       | `userdel -r <user>`                                 |                                                                |                                                                                                |
| System                |                                                     |                                                                |                                                                                                |
| `lsof`                |                                                     | list open files                                                |                                                                                                |
|                       | `sudo lsof -i -P -n \ grep LISTEN`                  | check if port is in use in                                     |                                                                                                |
|                       | `sudo netstat -tupln \ grep LISTEN`                 |                                                                |                                                                                                |
| `df`                  |                                                     | report file system disk space usage                            |                                                                                                |
|                       | `df -h`                                             | print sizes in powers of 1024 (e.g., 1023M)                    |                                                                                                |
|                       | `sodu df -sh [path]`                                | Get the Size of a Directory                                    |                                                                                                |
| `mount`               |                                                     | mount a filesystem                                             |                                                                                                |
| `umount`              |                                                     | unmount file systems                                           |                                                                                                |
| `fdisk`               | `fdisk [options] device`                            | manipulate disk partition table                                |                                                                                                |
|                       | `fdisk -l [device...]`                              | list disk                                                      |                                                                                                |
| `mkfs`                |                                                     | build a Linux filesystem                                       |                                                                                                |
| `e2label`             | `e2label device [ volume-label ]`                   | Change the label on an ext2/ext3/ext4 filesystem               |                                                                                                |
| `lsblk`               |                                                     | list block devices                                             |                                                                                                |
|                       |                                                     |                                                                |                                                                                                |
| file                  |                                                     |                                                                |                                                                                                |
| `tail`                |                                                     | output the last part of files                                  |                                                                                                |
| `dd`                  |                                                     | convert and copy a file                                        |                                                                                                |
| `find`                |                                                     | search for files in a directory hierarchy                      | [linux-find(TW)](https://blog.miniasp.com/post/2010/08/27/Linux-find-command-tips-and-notice)  |
|                       | `sudo find / -iname 'filename' -type f`             |                                                                |                                                                                                |
|                       | `sudo find / -iname 'dirname' -type d`              |                                                                |                                                                                                |
| `rsync`               | `rsync [OPTION...] SRC... [DEST]`                   | a fast, versatile, remote (and local) file-copying tool        |                                                                                                |
|                       | `rsync -avh --del SRC DEST --exclude='path'`        |                                                                |                                                                                                |
| `wget`                |                                                     | The non-interactive network downloader.                        |                                                                                                |
|                       | `wget <uri> -P /path/to/folder`                     | path of file                                                   |                                                                                                |
|                       | `wget <uri> -O /path/to/file.ext`                   | path of dictionary                                             |                                                                                                |
|                       |                                                     |                                                                |                                                                                                |
| server                |                                                     |                                                                |                                                                                                |
| `nslookup`            | `nslookup [-option] [name \ -] [server]`            |                                                                | [Nslookup](https://code.yidas.com/nslookup/)                                                   |
|                       | `nslookup -type=any domain.com`                     |                                                                |                                                                                                |
|                       |                                                     |                                                                |                                                                                                |


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


### Problem {#problem}


#### -bash: sudo: command not found {#bash-sudo-command-not-found}

<https://unix.stackexchange.com/a/425664>  


#### Fix apt-get update “the following signatures couldn’t be verified because the public key is not available” {#fix-apt-get-update-the-following-signatures-couldn-t-be-verified-because-the-public-key-is-not-available}

-   [Fix apt-get update “the following signatures couldn’t be verified because the public key is not available”](https://chrisjean.com/fix-apt-get-update-the-following-signatures-couldnt-be-verified-because-the-public-key-is-not-available/)


#### crontab {#crontab}

-   [Linux 設定 crontab 例行性工作排程教學與範例](https://blog.gtwang.org/linux/linux-crontab-cron-job-tutorial-and-examples/)
-   [corntab log](https://askubuntu.com/questions/56683/where-is-the-cron-crontab-log)


## Internet {#internet}


### IPv4 vs. IPv6 {#ipv4-vs-dot-ipv6}

-   [認識IPv4與IPv6的差異](https://www.ithome.com.tw/tech/92046)


### DHCP [DHCP](https://zh.wikipedia.org/wiki/%E5%8A%A8%E6%80%81%E4%B8%BB%E6%9C%BA%E8%AE%BE%E7%BD%AE%E5%8D%8F%E8%AE%AE) {#dhcp-dhcp}


### HTTP header fields {#http-header-fields}

-   [HTTP header fields](https://zh.wikipedia.org/wiki/HTTP%E5%A4%B4%E5%AD%97%E6%AE%B5)
