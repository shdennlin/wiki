+++
title = "Tools"
author = ["Shawn Dennis Lin"]
date = 2021-09-09T00:00:00+08:00
draft = false
+++

## Tools {#tools}


### ssh key {#ssh-key}


#### build ssh-key {#build-ssh-key}

```sh
ssh-keygen -t rsa -f ~/.ssh/sslsend -C "sslsend"
```


#### ssh config {#ssh-config}

Location: `~/.ssh/config`  

```sh
Host alias-name                      # 用來連線的 alias 名稱
HostName server.name                 # host domain 或 ip
Port port-number                     # host 的 SSH port
IdentitiesOnly yes                   # 使用指定的 key
IdentityFile ~/.ssh/private_ssh_file # 指定 pem 或 pub 的 key 路徑
User username-on-remote-machine      # (選填)登入 SSH 的 username，
                                     #  只連 git 的話，可以不必要
ForwardX11 yes                       # (選填) 啟用回傳 GUI 
```

example:  

```sh
Host shdennlin
Hostname github.com
IdentityFile ~/.ssh/shdennlin-nb-ubuntu
IdentitiesOnly yes
Port 22
User git
```

test:  

```sh
ssh -T git@shdennlin
```

git clone repository:  

```sh
# Type1: ssh protocol
git clone ssh://alias-name/project.git
git clone ssh://user-name@alias-name/project.git

# Type2: Recommend
git clone alias-name:project.git
git clone user-name@alias-name:project.git
```

[How to setup SSH config ：使用 SSH 設定檔簡化指令與連線網址](https://medium.com/%E6%B5%A6%E5%B3%B6%E5%A4%AA%E9%83%8E%E7%9A%84%E6%B0%B4%E6%97%8F%E7%BC%B8/how-to-setup-ssh-config-%E4%BD%BF%E7%94%A8-ssh-%E8%A8%AD%E5%AE%9A%E6%AA%94-74ad46f99818)  


#### scp {#scp}

```sh
scp -i ~/.ssh/sslsend ~/scp_test/scp_test1 itintern.nb.ubuntu@192.168.3.24:/home/itintern.nb.ubuntu/scp_test1
```


#### SSH Port Forawrding / Agent Forwarding {#ssh-port-forawrding-agent-forwarding}

-   [ ] [SSH agent forwarding 的應用](https://ihower.tw/blog/archives/7837)
-   [ ] [SSH Port Forwarding / Agent Forwarding](https://myapollo.com.tw/zh-tw/ssh-port-forwarding/)


#### Action or Problem {#action-or-problem}

<!--list-separator-->

-  How to Stop SSH Session From Getting Timed Out

    `vi ~/.ssh/config` and add  
    
    ```sh
    Host *
    ServerAliveInterval 300
    ServerAliveCountMax 2
    ```
    
    These settings will make the SSH client or server send a null packet to the other side every 300 seconds (5 minutes), and give up if it doesn’t receive any response after 2 tries, at which point the connection is likely to have been discarded anyway.  
    
    Ref: [How to Stop SSH Session From Getting Timed Out](https://www.thegeekdiary.com/how-to-stop-ssh-session-from-getting-timed-out/)  

<!--list-separator-->

-  在設定 windows ssh key 時，會連線不上 git lab

    ```shell
    Unable to start ssh-agent service, error:1058
    ```
    
    參考網址: <https://blog.alantsai.net/posts/2015/09/use-ssh-in-windows-for-github>  
    
    **[解決辦法]**  
    參考: <https://blog.alantsai.net/posts/2018/11/faq-start-sshagent-error-1058-on-windows-1803-cannot-use-ssh-agent>  
    
    **[系統資訊]**  
    
    | OS Name              | Microsoft Windows 10 Pro |
    |----------------------|--------------------------|
    | Version              | 10.0.19042 Build 19042   |
    | Other OS Description | Not Available            |
    | OS Manufacturer      | Microsoft Corporation    |

<!--list-separator-->

-  [error] Permission denied (publickey,gssapi-keyex,gssapi-with-mic)

    1.  `sudo vi /etc/ssh/sshd_config`  
        
        ```shell
        RSAAuthentication yes 
        PubkeyAuthentication yes
        AuthorizedKeysFile .ssh/authorized_keys
        PasswordAuthentication yes
        PermitRootLogin no
        ChallengeResponseAuthentication no
        
        GSSAPIAuthentication no
        GSSAPIKeyExchange no
        GSSAPICleanupCredentials no
        ```
    2.  type below  
        
        ```shell
        sudo systemctl reload sshd
        sudo systemctl restart sshd
        sudo service sshd restart
        
        chmod 600 ~/.ssh/authorized_keys
        ```

<!--list-separator-->

-  Nineder GCP ERROR

    情況: 要從公司 GCP 的 sever 中傳輸資料時, 會出現 error  
    範例: 要從 `itintern.nb.ubuntu@postgresql-11-test(192.168.3.20)` 中把 `itintern.nb.ubuntu@192.168.3.24:/home/itintern.nb.ubuntu/gcp24` 的檔案拉回來  
    note: 已經在 2 台 server 都有設定過 ssh 的連接(ssh-key)  
    以下是試過的方法:  
    
    1.  先使用 ssh 連接 2 台 server 看看  
        
        ```sh
        ssh -i ~/.ssh/itintern itintern.nb.ubuntu@192.168.3.24
        ```
        
        會需要密碼來驗證:  
        
        ```text
        Password:  
        ```
        
        結論: 無法使用
    
    2.  在其中一台 server(ex: itintern.nb.ubuntu@postgresql-11-test)中使用 scp  
        
        ```sh
        $ scp -i ~/.ssh/itintern itintern.nb.ubuntu@192.168.3.24:/home/itintern.nb.ubuntu/gcp24 ~/gcp24
        ```
        
        會需要密碼來驗證:  
        
        ```text
        Password: 
        ```
        
        結論: 無法使用
    
    3.  在其中一台 server(ex: itintern.nb.ubuntu@postgresql-11-test)中使用 `gcloud compute copy-files`   
        
        ```sh
        $ gcloud compute copy-files itintern.nb.ubuntu@stage-playground:~/gcp24 .
        ```
        
        會需要密碼來驗證:  
        
        ```text
        Updating project ssh metadata...done.                                                    
        Waiting for SSH key to propagate.
        Password: 
        ```
        
        結論: 無法使用
    
    4.  在其中一台 server(ex: itintern.nb.ubuntu@postgresql-11-test)中使用 `gcloud compute scp`  
        
        ```sh
        $ gcloud compute scp itintern.nb.ubuntu@satge-playground:~/gcp24 .
        ```
        
        出現  
        
        ```text
        Did you mean zone [asia-east1-b] for instance: [satge-playground] 
        (Y/n)?  y
        ERROR: (gcloud.compute.scp) Could not fetch resource:
        ​- The resource 'projects/sh99-production/zones/asia-east1-b/instances/satge-playground' was not found
        ```
        
        解決:  
        很有可能就是帳號的授權問題。這時只需要輸入以下指令重新授權：  
        
        ```sh
        $ gcloud auth login
        ```
        
        之後設定專案  
        
        ```sh
        $ gcloud config set project <your-project>
        ```
        
        結論: 權限不足, 暫時無法使用

<!--list-separator-->

-  ssh remote host identification has changed

    <https://stackoverflow.com/a/23150466/14740020>  


### git {#git}


#### save account and password {#save-account-and-password}

-   [Git 設定自動儲存帳號、密碼教學](https://officeguide.cc/git-save-username-and-password-tutorial/)

<!--listend-->

```sh
# 設定自動儲存帳號與密碼
git config --global credential.helper store

# 設定自動暫存帳號與密碼（存在記憶體 15 分鐘）
git config --global credential.helper cache

# 帳號與密碼暫存一小時
git config credential.helper 'cache --timeout=3600'
```


#### git flow {#git-flow}

<!--list-separator-->

-  Git Flow

    主要的分支有 `master`, `develop`, `hotfix`, `release` 以及 `feature` 這五種分支, Master 以及 Develop 這兩個分支又被稱做長期分支, 因為他們會一直存活在整個 Git Flow 裡, 而其它的分支大多會因任務結束而被刪除。  
    
    -   Master 分支  
        主要是用來放穩定、隨時可上線的版本。這個分支的來源只能從別的分支合併過來，開發者不會直接 Commit 到這個分支。因為是穩定版本，所以通常也會在這個分支上的 Commit 上打上版本號標籤。
    
    -   Develop 分支  
        這個分支主要是所有開發的基礎分支，當要新增功能的時候，所有的 Feature 分支都是從這個分支切出去的。而 Feature 分支的功能完成後，也都會合併回來這個分支。
    
    -   Hotfix 分支  
        當線上產品發生緊急問題的時候，會從 Master 分支開一個 Hotfix 分支出來進行修復，Hotfix 分支修復完成之後，會合併回 Master 分支，也同時會合併一份到 Develop 分支。  
        為什麼要合併回 Develop 分支？如果不這麼做，等到時候 Develop 分支完成並且合併回 Master 分支的時候，那個問題就又再次出現了。  
        那為什麼一開始不從 Develop 分支切出來修？因為 Develop 分支的功能可能尚在開發中，這時候硬是要從這裡切出去修再合併回 Master 分支，只會造成更大的災難。
    
    -   Release 分支  
        當認為 Develop 分支夠成熟了，就可以把 Develop 分支合併到 Release 分支，在這邊進行算是上線前的最後測試。測試完成後，Release 分支將會同時合併到 Master 以及 Develop 這兩個分支上。Master 分支是上線版本，而合併回 Develop 分支的目的，是因為可能在 Release 分支上還會測到並修正一些問題，所以需要跟 Develop 分支同步，免得之後的版本又再度出現同樣的問題。
    
    -   Feature 分支  
        當要開始新增功能的時候，就是使用 Feature 分支的時候了。Feature 分支都是從 Develop 分支來的，完成之後會再併回 Develop 分支。
    
    Ref: <https://nvie.com/posts/a-successful-git-branching-model/>  

<!--list-separator-->

-  GitHub Flow

    5 stages:  
    
    1.  Create A Branch (建立一個分支)
    2.  Add Commits (新增 Commits)
    3.  Open a Pull Request (開一個推送請求 PR)
    4.  Discuss And Review (討論及審查)
    5.  Deploy (部署)
    6.  Merge (合併)
    
    Ref: <https://ithelp.ithome.com.tw/articles/10228090>  

<!--list-separator-->

-  GitLab Flow

    1.  branch: `main`, `production`, `stable`
    
    Ref: <https://about.gitlab.com/topics/version-control/what-is-gitlab-flow/>  

<!--list-separator-->

-  Summary

    1.  Prefer to use `Git Flow`
    2.  develop branch merge to master need to use `git merge --no-ff` or `git merge --squash`


#### Error {#error}

```text
server certificate verification failed. CAfile: none CRLfile: none
```

Solve: <https://stackoverflow.com/a/21181447>  

`import_ssl.sh`  

```sh
#!/bin/bash
# Git 伺服器資訊
hostname=gitlabnew.nineder.com # your hostname
port=443

# 取得自己 OS 中放置 CA 的位置, 要先檢查一下有沒有憑證
trust_cert_file_location='/etc/ssl/certs/ca-certificates.crt'
# or
# trust_cert_file_location=`curl-config --ca`

# 匯入 Git 伺服器憑證
sudo bash -c "echo -n | openssl s_client -showcerts -connect $hostname:$port \
    2>/dev/null  | sed -ne '/-BEGIN CERTIFICATE-/,/-END CERTIFICATE-/p'  \
    >> $trust_cert_file_location"

```