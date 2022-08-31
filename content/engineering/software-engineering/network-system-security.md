+++
title = "Network System Security"
author = ["Shawn Dennis Lin"]
date = 2021-09-09T00:00:00+08:00
draft = false
+++

## CTF -- Catch The Flag {#ctf-catch-the-flag}

### Web Exploitation {#web-exploitation}

### Cryptography {#cryptography}

### Reverse Engineering {#reverse-engineering}

### Forensics {#forensics}

- exiftool  
    ex: `exiftool XXX.jpg`

### General Skills {#general-skills}

- base64  
    ex: `echo "XXX" | base64 -d`
- convert ASCII values into ASCII characters  
    `echo "XXX" | awk '{ printf("%c" ,$0); }'`
- nc  
  - [Netcat（Linux nc 指令）網路管理者工具實用範例](https://blog.gtwang.org/linux/linux-utility-netcat-examples/)
- [Rockstar](https://codewithrockstar.com/online)

### Binary Exploitation {#binary-exploitation}

### Uncategorized {#uncategorized}

## Network System Security {#network-system-security}

### SSL {#ssl}

#### 研究Certbot : 自動更新SSL {#研究certbot-自動更新ssl}

Ref: [RHEL / CentOS 安裝 Certbot 取得及更新 Let’s Encrypt 憑證](https://www.opencli.com/linux/rhel-centos-install-certbot-get-lets-encrypt-certs)  

#### 萬用網域的SSL憑證 {#萬用網域的ssl憑證}

- Ref: [如何使用 Certbot 命令列工具建立免費的 TLS/SSL 頂層網域憑證](https://blog.miniasp.com/post/2021/02/11/Create-SSL-TLS-certificates-from-LetsEncrypt-using-Certbot)

<!--list-separator-->

- 憑證檔

    > This directory contains your keys and certificates.  
    >
    > \`privkey.pem\`  : the private key for your certificate.  
    > \`fullchain.pem\`: the certificate file used in most server software.  
    > \`chain.pem\`    : used for OCSP stapling in Nginx >=1.3.7.  
    > \`cert.pem\`     : will break many server configurations, and should not be used  
    >                 without reading further documentation (see link below).  
    >
    > WARNING: DO NOT MOVE OR RENAME THESE FILES!  
    >         Certbot expects these files to remain in this location in order  
    >         to function properly!  
    >
    > We recommend not moving these files. For more information, see the Certbot  
    > User Guide at <https://certbot.eff.org/docs/using.html#where-are-my-certificates>.  

<!--list-separator-->

- Let's Encrypt 設定過程

  - Setp  
    - Step1: 在 second-level domain 的 server 去申請 \*.nineder.com 和 nineder.com的SSL憑證
    - Step2: 在每一台server下, 要修改apache ssl設定檔 `httpd.conf` or `ssl.conf`
    - Step3: 編寫shell script 檔, 透過使用scp的方式, 將3個憑證檔發到每一個 server
    - shell script範例:  

            ```shell
            #!/bin/bash
            scp -P 2222 -Br "/etc/letsencrypt/live/nineder.com/*.pem@remote1_ip:/home/user/..../"
            scp -P 2222 -Br "/etc/letsencrypt/live/nineder.com/*.pem@remote2_ip:/home/user/..../"
            ```

            SCP 參考: <http://note.drx.tw/2008/03/ubuntuscp-part1.html>

  - 之後可能愈到問題點  
        1. 憑證檔的配置問題  
            `cert.pem`, `privkey.pem`, `fullchain.pem` 這3個檔案的位置可能在每一個不同的server下都不一樣, 所以進每一個server去查看配置

        2. scp 問題  
            - 要確定scp的port有沒有開啟, 如果要傳過去的server沒有開啟port, 可能會造成失敗
            - scp傳輸時需要密碼, 可生在ssh\_key, 即可做自動執行 <https://ithelp.ithome.com.tw/articles/10107224?sc=rss.iron>
            - 在寫scp傳輸的script時, 可以加一下判斷, 如果有更新, 在做傳輸 (可以直接寫在crontab 的 renew.sh)

        3. 更新憑證  
            在更新憑證後, 還是要對每一台server重新reload, 所以還是要寫crontab來安排重啟server, ex:  

            ```shell
            #!/bin/bash
            
            domain="adapi.isp99.com"
            path="/etc/letsencrypt/live/$domain"
            echo $path
            
            new_file="$path/test.pem"
            old_file="$path/test.pem.backup"
            if [ -f "$old_file" ]; then
                if cmp -s $old_file $new_file; then
                    echo "### SUCCESS: SSL certifcates not update ###"
                else
                    # systemctl reload httpd
                    echo "### SUCCESS: SSL certifcates update! ###"
                    echo "systemctl reload httpd"
                    cp $new_file $old_file
                fi
            else
                echo "$old_file not found."
                cp $new_file $old_file
                echo "bulid $old_file. successful"
            fi
            ```

#### 萬用 SSL 申請步驟 & Nginx 配置 {#萬用-ssl-申請步驟-and-nginx-配置}

1. 下載 cerbot (Dabian 9) (若不行, 可參考 [certbot instructions](https://certbot.eff.org/instructions) 去使用指令下載)  

    ```sh
    sudo apt install snapd
    sudo snap install core; sudo snap refresh core
    sudo snap install --classic certbot
    sudo ln -s /snap/bin/certbot /usr/bin/certbot
    ```

    確認 cerbot 安裝成功:  

    ```sh
    sudo certbot --version
    ```

2. 使用 cerbot 產生 SSL/TLS 憑證 (以 Nginx 為例)  
    Note: **需要擁有 nineder.com 域名的管理權限，下面的挑戰會用到**  
    請輸入以下命令產生 \*.nineder.com 萬用子網域憑證  

    ```sh
    sudo certbot certonly --manual --preferred-challenges=dns -m idd-shared@nineder.com -d *.nineder.com
    ```

    因為加入 `--manual` 參數的關係，接下來的操作都將會以「互動式」的方式完成設定  

    1. 顯示偵錯紀錄檔的路徑與要你輸入 `y` 同意服務使用條款  

        ```text
        Saving debug log to C:\Certbot\log\letsencrypt.log
        Plugins selected: Authenticator manual, Installer None
        ​
        - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
        Please read the Terms of Service at
        https://letsencrypt.org/documents/LE-SA-v1.2-November-15-2017.pdf. You must
        agree in order to register with the ACME server. Do you agree?
        ​- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
        (Y)es/(N)o: y
        ```

    2. 問你是不是要提供 E-mail 給 Electronic Frontier Foundation (EFF)？  

        ```text
        ​- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
        Would you be willing, once your first certificate is successfully issued, to
        share your email address with the Electronic Frontier Foundation, a founding
        partner of the Let's Encrypt project and the non-profit organization that
        develops Certbot? We'd like to send you email about our work encrypting the web,
        EFF news, campaigns, and ways to support digital freedom.
        ​- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
        (Y)es/(N)o: y
        Account registered.
        ```

        Note: **這個步驟會將你的 E-mail 自動註冊為 ACME 帳戶**
    3. 準備發出憑證請求  

        ```text
        Requesting a certificate for angular.tw and *.angular.tw
        Performing the following challenges:
        dns-01 challenge for nineder.com
        http-01 challenge for nineder.com
        ```

        上面的訊息說 會有 2 個 **挑戰** 要完成( `dns-01`, `http-01` ) (也有可能只有 1 個, 為 `dns-01` )
    4. 挑戰 1: `verbatim-01`  
        必須先新增一筆 `TXT` 紀錄到 `_acme-challenge.nineder.com` 的域名上，並將其值設定為 `WL_prmhxrXuRBbV3ObpbAn_2WJKdey1w0dHCuv-LmPc` `(改成顯示在shell的文字)` ，新增完後再按下 `Enter` 繼續  
        `EX: 會顯示的內容`  

        ```text
        ​- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
        Please deploy a DNS TXT record under the name
        _acme-challenge.angular.tw with the following value:
        
        WL_prmhxrXuRBbV3ObpbAn_2WJKdey1w0dHCuv-LmPc <==== 會變動的地方
        
        Before continuing, verify the record is deployed.
        ​- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
        Press Enter to Continue
        ```

        可參考下面圖片做設定  
        `改成圖片 dns_record.jpg`  
        Note: **一定要先設定好 DNS 紀錄才能按下 Enter 繼續**
    5. 挑戰 2: http-01  
        這個挑戰要你在官網建立一個特殊網址路徑的文字檔案，而且必須可以讓 Let's Encrypt 網站能夠公開存取該網址，而且一定只能走 Port 80 進行 HTTP 連線，不能使用任何其他埠號，如此一來才能驗證你就是該網站的擁有者  
        網址路徑： `http://nineder.com/.well-known/acme-challenge/IKibDaF4-FHZoGw1U6JTyGlBDMOtE-cQCFw13e4FaUc` `(改成顯示在shell的文字)`  
        檔案內容： `IKibDaF4-FHZoGw1U6JTyGlBDMOtE-cQCFw13e4FaUc.plEmWe4UXqKWJvuRWXDnZDtkeEh2omjTeQWuZHEKan4` `(改成顯示在shell的文字)`  
        /.well-known/acme-challenge/PuW9TG2w08zYv0RnBZkirjRLJ3PtA-exgVMc94dgFTY  

        `EX: 會顯示的內容`  

        ```text
        ​- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
        Create a file containing just this data:
        
        IKibDaF4-FHZoGw1U6JTyGlBDMOtE-cQCFw13e4FaUc.plEmWe4UXqKWJvuRWXDnZDtkeEh2omjTeQWuZHEKan4  <=== 檔案內容
        
        And make it available on your web server at this URL:
        
        http://nineder.com/.well-known/acme-challenge/IKibDaF4-FHZoGw1U6JTyGlBDMOtE-cQCFw13e4FaUc <=== 網址路徑
        
        (This must be set up in addition to the previous challenges; do not remove,
        replace, or undo the previous challenge tasks yet.)
        ​
        - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
        Press Enter to Continue
        ```

        Note: **網站一定要能夠接聽 Port 80 的 HTTP 連接**  
        最後用瀏覽器確定 `http-01` 挑戰的網址可以順利打開，才能按下 `Enter` 繼續
    6. 免費憑證申請成功，並顯示憑證檔路徑  
        當 `dns-01` 與 `http-01` 挑戰都能驗證成功，Certbot 會先幫你訂閱一個 EFF mailing list 郵件清單，並提示你 **憑證 PEM 檔案所在路徑與憑證到期日** :  

        ```text
        Waiting for verification...
        Cleaning up challenges
        Subscribe to the EFF mailing list (email: idd-shared@nineder.com).
        
        IMPORTANT NOTES:
        ​- Congratulations! Your certificate and chain have been saved at:
          /etc/letsencrypt/live/nineder.com/fullchain.pem   <==== 憑證 PEM 檔案所在路徑
          Your key file has been saved at:
          /etc/letsencrypt/live/nineder.com/privkey.pem   <==== 憑證 PEM 檔案所在路徑
          Your certificate will expire on 2021-05-11. To obtain a new or   <==== 到期日
          tweaked version of this certificate in the future, simply run
          certbot again. To non-interactively renew *all* of your
          certificates, run "certbot renew"
        ​- If you like Certbot, please consider supporting our work by:
        
          Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
          Donating to EFF:                    https://eff.org/donate-le
        ```

        到這一步憑證就申請完成, 接下來設定網站伺服器的 ssl 憑證路徑
3. 設定網站伺服器的 ssl 憑證  
    1. 找到 nginx config, 通常會在 `/etc/nginx/sites-available/default` 之類的
    2. 在檔案的找到要加入SSL憑證的server設定檔, 寫入  

        ```nginx
        server {
            # 略...
        
            listen 443 ssl;
        
            # RSA certificate
            ssl_certificate /etc/letsencrypt/live/nineder.com/fullchain.pem;
            ssl_certificate_key /etc/letsencrypt/live/nineder.com/privkey.pem;
        }
        ```

    3. 完成後使用  

        ```sh
        sudo systemctl reload nginx
        ```

        並查看狀態  

        ```sh
        sudo systemctl status nginx
        ```

參考: [如何使用 Certbot 命令列工具建立免費的 TLS/SSL 頂層網域憑證](https://blog.miniasp.com/post/2021/02/11/Create-SSL-TLS-certificates-from-LetsEncrypt-using-Certbot)  

#### Auto-Renew Let's Encrypt Wildcard Certificate {#auto-renew-let-s-encrypt-wildcard-certificate}

Ref:  

1. [How to Create and Auto-Renew Let's Encrypt Wildcard Certificate?](https://developerinsider.co/how-to-create-and-auto-renew-lets-encrypt-wildcard-certificate/)
2. [DNS Plugins](https://certbot.eff.org/docs/using.html?highlight=dns#dns-plugins)
3. [Auto-Renew Let’s Encrypt Wildcard Certificate using Google Cloud DNS](https://itsmetommy.com/2019/08/03/auto-renew-lets-encrypt-wildcard-certificate-using-google-cloud-dns/)

#### 更新SSL {#更新ssl}

<!--list-separator-->

- gcp store 儲存ssl

    Step:  

    1. 查看有什麼儲存地方  

        ```sh
        gsutil ls -l
        ```

    2. Create a bucket  

        ```sh
        gsutil mb -b on -l ASIA-EAST1 gs://nineder.com-ssl
        ```

    Ref: [https://cloud.google.com/storage/docs/quickstart-gsutil](https://cloud.google.com/storage/docs/quickstart-gsutil)  

<!--list-separator-->

- 使用git管理

    use git and Jenkins  

#### Ref: {#ref}

1. [教學課程：在 中使用 Let's Encrypt SSL 憑證與 LAMP 執行個體Amazon Lightsail](https://lightsail.aws.amazon.com/ls/docs/zh%5Ftw/articles/amazon-lightsail-using-lets-encrypt-certificates-with-lamp#request-a-lets-encrypt-certificate-lamp)
2. [如何使用 Certbot 命令列工具建立免費的 TLS/SSL 頂層網域憑證](https://blog.miniasp.com/post/2021/02/11/Create-SSL-TLS-certificates-from-LetsEncrypt-using-Certbot)
3. [Let's Encrypt Wildcard 申請流程](http://blog.tonycube.com/2019/02/lets-encrypt-wildcard.html)
4. [Auto-Renew Let’s Encrypt Wildcard Certificate using Google Cloud DNS](https://itsmetommy.com/2019/08/03/auto-renew-lets-encrypt-wildcard-certificate-using-google-cloud-dns/)

### WebSocket {#websocket}

- [WebSocket-wiki](https://zh.wikipedia.org/wiki/WebSocket)

## Internet {#internet}

### IPv4 vs. IPv6 {#ipv4-vs-dot-ipv6}

- [認識IPv4與IPv6的差異](https://www.ithome.com.tw/tech/92046)
- [Understanding IP Address and Subnets](https://www.zymr.com/understanding-ip-address-subnets/)

### DHCP [DHCP](https://zh.wikipedia.org/wiki/%E5%8A%A8%E6%80%81%E4%B8%BB%E6%9C%BA%E8%AE%BE%E7%BD%AE%E5%8D%8F%E8%AE%AE) {#dhcp-dhcp}

### HTTP header fields {#http-header-fields}

- [HTTP header fields](https://zh.wikipedia.org/wiki/HTTP%E5%A4%B4%E5%AD%97%E6%AE%B5)
