---
Title: Linux Useful Tools
Description: >
  Useful tools can improve your development efficiency
---

## System tools

### • Boot-Repair

<https://help.ubuntu.com/community/Boot-Repair>

A simple tool to repair frequent boot issues you may encounter in Ubuntu

```bash
sudo add-apt-repository ppa:yannubuntu/boot-repair && sudo apt update
sudo apt install -y boot-repair && boot-repair
```

### • TLP

<https://linrunner.de/tlp/index.html>

Optimize Linux Laptop Battery Life

```bash
sudo apt install tlp tlp-rdw
sudo apt-get install smartmontools
sudo systemctl start tlp

sudo tlp-stat | less
```

## GUI tools

### • Angry IP scanner

<https://angryip.org/>

Fast and friendly network scanner

### • Crow Translate

<https://crow-translate.github.io/>

A simple and lightweight translator

### • Drawio Desktop

<https://github.com/jgraph/drawio-desktop>

A diagramming and whiteboarding desktop app based on Electron that wraps the core draw.io editor.

### • Fcitx 5

<https://fcitx-im.org/wiki/Install_Fcitx_5>

Input method framework with extension support

```bash
sudo apt-get install -y fcitx fcitx-table-boshiamy fcitx-chewing
```

### • Free File Sync

<https://freefilesync.org/>

Open Source File Synchronization & Backup Software

### • Open Broadcaster Software Studio (OBS)

<https://obsproject.com/>

Free and open source software for video recording and live streaming

### • QDirStat

<https://github.com/shundhammer/qdirstat>

Qt-based directory statistics (KDirStat without any KDE - from the original KDirStat author)

```bash
sudo apt-get install -y qdirstat
```

### • Rclone

<https://rclone.org/>

A command-line program to manage files on cloud storage. It is a feature-rich alternative to cloud vendors' web storage interfaces. Over 40 cloud storage products support rclone including S3 object stores, business & consumer file storage services, as well as standard transfer protocols.

### • Remmina

<https://remmina.org/>

Remote access screen and file sharing to your desktop

### • linux-wifi-hotspot

<https://github.com/lakinduakash/linux-wifi-hotspot>

Feature-rich wifi hotspot creator for Linux, which provides both GUI and command-line interface.

## Terminal Tools

### • aria2

<https://aria2.github.io/>

aria2 is a lightweight multi-protocol & multi-source command-line download utility. It supports HTTP/HTTPS, FTP, SFTP, BitTorrent and Metalink. aria2 can be manipulated via built-in JSON-RPC and XML-RPC interfaces.

```bash
sudo apt-get install -y aria2
```

### • bat

<https://github.com/sharkdp/bat>

A cat(1) clone with wings.

```bash
sudo apt install -y bat
```

### • dua

<https://github.com/Byron/dua-cli>

View disk space usage and delete unwanted data, fast.

```bash
curl -LSfs https://raw.githubusercontent.com/Byron/dua-cli/master/ci/install.sh |
sh -s -- --git Byron/dua-cli --target x86_64-unknown-linux-musl --crate dua --tag v2.17.4
```

### • exa

<https://the.exa.website/>

A modern replacement for ls.
`exa` is a modern replacement for `ls`. It supports colours, Git integration, and other niceties.

```shell
sudo apt-get install -y exa
```

### • fd

<https://github.com/sharkdp/fd>

A simple, fast and user-friendly alternative to 'find'

```bash
sudo apt-get install -y fd-find
```

### • fzf

<https://github.com/junegunn/fzf>

A command-line fuzzy finder

```bash
sudo apt-get install fzf
```

### • fzf-tab

<https://github.com/Aloxaf/fzf-tab>

Replace zsh's default completion selection menu with fzf!

### • locate

<https://linuxhint.com/linux-locate-command/>

the quickest and simplest way to search for files and directories by their names.

```bash
sudo apt install mlocate
```

### • mosh

<https://mosh.org>

Mosh is a remote terminal application that supports intermittent connectivity, allows roaming, and provides speculative local echo and line editing of user keystrokes.

```bash
sudo apt-get install mosh
```

### • process monitor

- [BPYTOP](https://github.com/aristocratos/bpytop)
  Linux/OSX/FreeBSD resource monitor

  ```bash
  sudo apt install bpytop
  ```

- [nvitop](https://github.com/XuehaiPan/nvitop)
  An interactive NVIDIA-GPU process viewer, the one-stop solution for GPU process management.

  ```bash
  pip3 install --upgrade nvitop
  ```

### • ripgrep

<https://github.com/BurntSushi/ripgrep>

ripgrep recursively searches directories for a regex pattern while respecting your gitignore

```bash
sudo apt-get install -y ripgrep
```

### • the Silver Searcher

<https://github.com/ggreer/the_silver_searcher>

A code-searching tool similar to ack, but faster.

```bash
sudo apt-get install silversearcher-ag
```

### • xclip

<https://github.com/astrand/xclip>

Command line interface to the X11 clipboard

```bash
sudo apt-get install -y xclip
```

### • xxh

<https://github.com/xxh/xxh>

Bring your favorite shell wherever you go through the ssh.

```bash
pip3 install xxh-xxh
```

### • zoxide

<https://github.com/ajeetdsouza/zoxide>

zoxide is a smarter cd command, inspired by z and autojump.

### • zsh

<https://www.zsh.org/>

Zsh is a shell designed for interactive use, although it is also a powerful scripting language

```bash
sudo apt-get install -y zsh
```
