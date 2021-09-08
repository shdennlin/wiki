+++
title = "Establish Build with Docker"
author = ["Shawn Dennis Lin"]
date = 2021-09-09T00:00:00+08:00
draft = false
+++

-   official website: <https://www.redmine.org>
-   Download Page: <https://www.redmine.org/projects/redmine/wiki/Download>
-   Installation Guide: <https://www.redmine.org/projects/redmine/wiki/redmineinstall>
-   Ref: <https://www.redmine.org/projects/redmine/wiki/HowTo%5FInstall%5FRedmine%5Fon%5FDebian%5F9>
-   official docker hub: <https://hub.docker.com/%5F/redmine>


## Establish Redmine from the beginning {#establish-redmine-from-the-beginning}


### VM initial {#vm-initial}

```sh
# update
sudo apt update && sudo apt upgrade -y
# change time zone
sudo dpkg-reconfigure tzdata

# isntall git
sudo apt install -y git

# install docker
# https://docs.docker.com/engine/install/debian/#install-using-the-repository
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo docker run hello-world

# add user in docker group
sudo groupadd docker
sudo usermod -aG docker $USER

# isntall docker compose https://docs.docker.com/compose/install/
sudo apt install -y python3-pip libffi-dev
sudo pip3 install docker-compose:w
docker-compose --version
```


### Download Redmine and run {#download-redmine-and-run}


### Nginx {#nginx}

```sh
sudo apt install -y ngninx
```


### Install SSL {#install-ssl}

Ref: <https://certbot.eff.org/lets-encrypt/debianbuster-nginx>  


#### Set server account {#set-server-account}

```sh
gcloud auth activate-service-account shdennlin-dns@shdennlin.iam.gserviceaccount.com --key-file=shdennlin-c83d109ebef3.json
```

Note: shdennlin-c83d109ebef3.json is server account secret  


#### give dns admin permissions {#give-dns-admin-permissions}

```sh
gcloud projects add-iam-policy-binding shdennlin \
  --member=serviceAccount:shdennlin-dns@shdennlin.iam.gserviceaccount.com\
  --role=roles/dns.admin
```


#### Install SSL by Let's encrypt {#install-ssl-by-let-s-encrypt}

```sh
# install certbot
sudo apt install -y snapd
sudo snap install core; sudo snap refresh core
sudo snap install --classic certbot

snap set certbot trust-plugin-with-root=ok
sudo snap install certbot-dns-google
sudo ln -s /snap/bin/certbot /usr/bin/certbot
sudo certbot --version
```


#### Create Wildcard SSL Certificate {#create-wildcard-ssl-certificate}

```sh
sudo certbot certonly \
     --dns-google \
     --dns-google-credentials ~/.secrets/certbot/shdennlin-c83d109ebef3.json \
     -d "*.shdennlin.org" \
     -m shawndennislin@gmail.com \
     --agree-tos

sudo certbot certonly \
     --dns-google \
     -d shdennlin.org \
     -d *.shdennlin.org \
     -m shawndennislin@gmail.com \
     --agree-tos
# Test automatic renewal 
sudo certbot renew --dry-run
```

Step2. SSL configuration in nginx  

1.  `sudo -E vi /opt/nginx/conf/nginx.conf`  
    
    ```nginx
    server {
        # omit...
    
        listen 443 ssl;
    
        # RSA certificate
        ssl_certificate /etc/letsencrypt/live/redmine.shdennlin.org/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/redmine.shdennlin.org/privkey.pem;
    }
    ```


### Gmail Configuration {#gmail-configuration}

Ref: <https://www.redmine.org/projects/redmine/wiki/emailconfiguration#GMail-Google-Apps>  

-   Error: `5.7.8 Username and Password not accepted. Learn more....`  
    Solve: <https://stackoverflow.com/a/58947125/14740020>
-   Error: `send-mail: Authorization failed 534 5.7.14`  
    Slove: <https://serverfault.com/a/672182>


## Plugins {#plugins}

Ref: <https://www.redmine.org/plugins>  


#### WYSIWYG Editor {#wysiwyg-editor}

Ref: <https://redmine.org/plugins/redmine%5Fwysiwyg%5Feditor>  
Github: <https://github.com/taqueci/redmine%5Fwysiwyg%5Feditor>  

```sh
cd ~/redmine-4.2/plugins
git clone https://github.com/taqueci/redmine_wysiwyg_editor.git
cd redmine_wysiwyg_editor
git reset --hard 0.21.1
touch /home/redmine/redmine-4.2/tmp/restart.txt
```


#### Agile {#agile}

Ref: <https://www.redmine.org/plugins/redmine%5Fagile>  
Install: <https://www.redmineup.com/pages/help/agile/installing-redmine-agile-plugin-on-linux?utm%5Fsource=Main&utm%5Fmedium=email&utm%5Fcampaign=Download%5Fplugin%5Femail&utm%5Fterm=download%5Fplugin%5Femail&utm%5Fcontent=installation%5Fguide>  

```sh
cd ~/redmine-4.2/plugins
wget -O redmine_agile.zip <URL> 
unzip redmine_agile.zip
rm -rf redmine_agile.zip

cd ~/redmine-4.2
bundle install --without development test --no-deployment
bundle exec rake redmine:plugins NAME=redmine_agile RAILS_ENV=production
touch /home/redmine/redmine-4.2/tmp/restart.txt
```


#### checklist {#checklist}

Ref: <https://www.redmine.org/plugins/redmine%5Fchecklists>  
Install: <https://www.redmineup.com/pages/help/checklists/installing-redmine-checklists-plugin-on-linux?utm%5Fsource=Main&utm%5Fmedium=email&utm%5Fcampaign=Download%5Fplugin%5Femail&utm%5Fterm=download%5Fplugin%5Femail&utm%5Fcontent=installation%5Fguide>  

```sh
cd ~/redmine-4.2/plugins
wget -O redmine_checklists-3_1_19-light.zip <URL> 
unzip redmine_checklists-3_1_19-light.zip
rm -rf redmine_checklists-3_1_19-light.zip

cd ~/redmine-4.2
bundle install --without development test --no-deployment
bundle exec rake redmine:plugins NAME=redmine_checklists RAILS_ENV=production
touch /home/redmine/redmine-4.2/tmp/restart.txt
```


#### Attach image from clipboard (can't use in Redmine 4.2.1.stable.20997) {#attach-image-from-clipboard--can-t-use-in-redmine-4-dot-2-dot-1-dot-stable-dot-20997}

Ref: <https://www.redmine.org/plugins/clipboard%5Fimage%5Fpaste>  
Install: <https://github.com/peclik/clipboard%5Fimage%5Fpaste/blob/master/README.textile>  

```sh
cd ~/redmine-4.2/plugins
git clone https://github.com/peclik/clipboard_image_paste.git
cd clipboard_image_paste
git reset --hard v1.9

cd ~/redmine-4.2
touch /home/redmine/redmine-4.2/tmp/restart.txt
```


## Themes {#themes}

Ref: <https://www.redmine.org/projects/redmine/wiki/theme%5Flist>  


### PurpleMine 2 {#purplemine-2}

Github: <https://github.com/mrliptontea/PurpleMine2>  

```sh
cd ~/redmine-4.2/public/themes/
git clone https://github.com/mrliptontea/PurpleMine2.git
cd Purple Mine2
git reset --hard v2.14.0
```


## Action {#action}


### Restart Redmine {#restart-redmine}

```sh
docker-compose restart redmine
```
