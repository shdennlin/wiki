+++
title = "Establish Build"
author = ["Shawn Dennis Lin"]
date = 2021-09-09T00:00:00+08:00
draft = false
+++

-   official website: <https://www.redmine.org>
-   Download Page: <https://www.redmine.org/projects/redmine/wiki/Download>
-   Installation Guide: <https://www.redmine.org/projects/redmine/wiki/redmineinstall>
-   Ref: <https://www.redmine.org/projects/redmine/wiki/HowTo%5FInstall%5FRedmine%5Fon%5FDebian%5F9>


## Establish Redmine from the beginning {#establish-redmine-from-the-beginning}


### VM initial {#vm-initial}

```sh
# update
sudo apt update && sudo apt upgrade -y
# change time zone
sudo dpkg-reconfigure tzdata
```


### Download Redmine {#download-redmine}

```sh
#  insatll version-control
sudo apt-get install -y subversion git
sudo apt install redmine-pgsql libpq-dev libcurl4-gnutls-dev

# add user
sudo adduser redmine --disabled-password
sudo usermod -aG sudo redmine
sudo su redmine
cd

# get redmine-4.2
svn co https://svn.redmine.org/redmine/branches/4.2-stable redmine-4.2
```


### Install PostgreSQL {#install-postgresql}

Step1. install PostgreSQL  

```sh
# Create the file repository configuration:
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'

# Import the repository signing key:
sudo apt install wget
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -

# Update the package lists:
sudo apt-get update

# Install the latest version of PostgreSQL.
# If you want a specific version, use 'postgresql-12' or similar instead of 'postgresql':
sudo apt-get -y install postgresql-13 
```

Step2. Create an empty database and accompanying user  

```sh
sudo -u postgres psql
```

```sql
CREATE ROLE redmine LOGIN ENCRYPTED PASSWORD 'my_password' NOINHERIT VALID UNTIL 'infinity';
CREATE DATABASE redmine WITH ENCODING='UTF8' OWNER=redmine;
ALTER DATABASE "redmine" SET datestyle="ISO,MDY";

\du
\l
show datestyle;
```

Step3. Database connection configuration  

```sh
sudo su redmine
cd
cp ~/redmine-4.2/config/database.yml.example ~/redmine-4.2/config/database.yml
vi ~/redmine-4.2/config/database.yml
```


### Install Ruby, redmine and Dependencies installation {#install-ruby-redmine-and-dependencies-installation}

see <https://rvm.io/rvm/install>  
Step1. Install ruby  

```sh
sudo apt-get install gnupg2 -y

sudo su redmine
cd
gpg --keyserver hkp://pool.sks-keyservers.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB

\curl -sSL https://get.rvm.io | bash -s stable
echo "source $HOME/.rvm/scripts/rvm" >> ~/.bash_profile
source ~/.rvm/scripts/rvm
type rvm | head -n 1

rvm install 2.7.3
rvm use 2.7.3
rvm use 2.7.3 --default
rvm list
ruby -v

echo "export GEM_HOME=\$HOME/.gem" >> ~/.bashrc
source ~/.bashrc
```

Step2. Install Redmine  

```sh
cd ~/redmine-4.2
gem install bundler
bundle install --without development test
bundle exec rake generate_secret_token
RAILS_ENV=production bundle exec rake db:migrate
RAILS_ENV=production bundle exec rake redmine:load_default_data

# =====================
mkdir -p tmp tmp/pdf public/plugin_assets
sudo chown -R redmine:redmine files log tmp public/plugin_assets
sudo chmod -R 755 files log tmp public/plugin_assets

sudo find files log tmp public/plugin_assets -type f -exec chmod -x {} +

# Test the installation
bundle exec rails server webrick -e production
# open http://localhost:3000/

```


### Passenger + Nginx {#passenger-plus-nginx}

Ref: <https://www.phusionpassenger.com/library/install/nginx/install/oss/rubygems%5Frvm/>  
Step 1: install gem  

```sh
gem install passenger --no-rdoc --no-ri
```

Step 3: run the Passenger Nginx module installer  

```sh
source ~/.bashrc
source ~/.bash_profile
# NOTE RAM need 2GB or more
rvmsudo passenger-install-nginx-module
```

Step 4: validate installation  

```sh
rvmsudo passenger-config validate-install
```


### Using Nginx {#using-nginx}

-   Starting Nginx  
    You can start Nginx by running:  
    `sudo /opt/nginx/sbin/nginx`
-   Shutting down Nginx  
    You can shut down Nginx by killing its PID with the kill command. To find out what Nginx's PID is, use the ps command. For example:  
    `ps auxw | grep nginx`

-   Restarting Nginx  
    Restarting Nginx is the same as shutting down Nginx, and starting it again. For example:  
    
    ```sh
    sudo kill $(cat /opt/nginx/logs/nginx.pid)
    sudo /opt/nginx/sbin/nginx
    ```


#### Nginx Configuration {#nginx-configuration}

1.  `sudo -E vi /opt/nginx/conf/nginx.conf`
2.  uncomment `user nobody` and set to `user redmine`


### Install SSL {#install-ssl}

Ref: <https://certbot.eff.org/lets-encrypt/debianbuster-nginx>  

Step1. Install SSL by Let's encrypt  

```sh
# install certbot
sudo apt install -y snapd
sudo snap install core; sudo snap refresh core
sudo snap install --classic certbot
sudo ln -s /snap/bin/certbot /usr/bin/certbot
sudo certbot --version
# auto build ssl by certbot
sudo certbot certonly \
     --webroot -w /home/redmine/redmine-4.2/public \
     -d redmine.shdennlin.org \
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

2.  reload Nginx  
    
    ```sh
    # test Nginx
    sudo /opt/nginx/sbin/nginx -t
    
    # restart nginx
    sudo kill $(cat /opt/nginx/logs/nginx.pid)
    sudo /opt/nginx/sbin/nginx
    # show nginx status
    ps auxw | grep nginx
    ```


### Install Additional dependencies {#install-additional-dependencies}


#### Ghostscript {#ghostscript}

Ref: <https://www.ghostscript.com/doc/9.54.0/Install.htm>  
Ghostscript is an interpreter for the PostScript®  language and PDF files. It is available under either the GNU GPL Affero license or  licensed for commercial use from Artifex Software, Inc. It has been under active development for over 30 years and has been ported to several different systems during this time. Ghostscript consists of a PostScript interpreter layer and a graphics library.  

```sh
wget https://github.com/ArtifexSoftware/ghostpdl-downloads/releases/download/gs9540/ghostscript-9.54.0.tar.gz
tar -xvzf ghostscript-9.54.0.tar.gz
rm -rf ghostscript-9.54.0.tar.gz
cd ghostscript-9.54.0
./configure
make 
sudo make install
```


#### FreeType {#freetype}

Ref: <https://www.freetype.org/download.html#stable-releases>  

```sh
wget https://download.savannah.gnu.org/releases/freetype/freetype-2.10.0.tar.gz
tar -xvzf freetype-2.10.0.tar.gz
rm -rf freetype-2.10.0.tar.gz
cd freetype-2.10.0
./configure
make 
sudo make install
```


#### ImageMagick {#imagemagick}

Ref: <https://imagemagick.org/script/install-source.php>  

```sh
sudo apt-get install -y libltdl-dev
git clone --depth 1 https://github.com/ImageMagick/ImageMagick.git ImageMagick-7.0.11
cd ImageMagick-7.0.11
./configure --with-modules
make
sudo make install
sudo ldconfig /usr/local/lib
/usr/local/bin/convert logo: logo.gif
make check

# check
magick identify -version
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
wget -O redmine_agile-1_6_1-light.zip <URL> 
unzip redmine_agile-1_6_1-light
rm -rf redmine_agile-1_6_1-light.zip

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
wget -O redmine_checklists-3_1_18-light.zip <URL> 
unzip redmine_checklists-3_1_18-light.zip
rm -rf redmine_checklists-3_1_18-light.zip

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
cd PurpleMine2
git reset --hard v2.14.0
```


## Action {#action}


### Restart Redmine {#restart-redmine}

```sh
touch /home/redmine/redmine-4.2/tmp/restart.txt
```

Ref: <https://stackoverflow.com/a/31787437/14740020>
