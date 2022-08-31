+++
title = "Web Developer"
author = ["Shawn Dennis Lin"]
date = 2021-09-08T00:00:00+08:00
lastmod = 2022-01-11T11:12:28+08:00
draft = false
+++

## Laravel - The PHP Framework for Web Artisans {#laravel-the-php-framework-for-web-artisans}

-   <https://laravel.com/>


## Front-end {#front-end}


## Back-end {#back-end}


### Web Server {#web-server}

Introduce  

-   <https://medium.com/starbugs/web-server-nginx-1-cf5188459108>


#### Nginx {#nginx}

Nginx (pronounced "engine X"), stylized as NGINX, nginx or NginX, is a web server that can also be used as a reverse proxy, load balancer, mail proxy and HTTP cache. The software was created by Igor Sysoev and publicly released in 2004. Nginx is free and open-source software, released under the terms of the 2-clause BSD license. A large fraction of web servers use NGINX, often as a load balancer.  

<!--list-separator-->

-  Install and Tutorial

    ```sh
    sudo apt-get install -y nginx
    sudo nginx -v
    sudo nginx
    curl -I 127.0.0.1
    ```
    
    -   GitHub: <https://github.com/nginx/nginx>
    -   Repository: <https://hg.nginx.org/nginx>
    -   Official Website: <https://www.nginx.com/>
    -   Install tutorial: <https://docs.nginx.com/nginx/admin-guide/installing-nginx/installing-nginx-open-source/>

<!--list-separator-->

-  Configuration

    -   PHP-FPM: [How to Configure Nginx to Execute PHP Using PHP-FPM](https://www.thegeekstuff.com/2013/12/nginx-php-fpm/)
    -   upstream: [nginx实现负载均衡upstream](http://www.shixinke.com/nginx/nginx-upstream)
    -   map: [nginx map使用方法](http://www.ttlsa.com/nginx/using-nginx-map-method/)
    -   sendfile: [sendfile()对nginx性能的提升](https://blog.51cto.com/laoxu/1417294) [sendfile](https://thoughts.t37.net/nginx-optimization-understanding-sendfile-tcp-nodelay-and-tcp-nopush-c55cdd276765)
    -   proxy\_pass:

<!--list-separator-->

-  QA

    <!--list-separator-->
    
    -  What does [::] mean in my nginx config file
    
        -   [What does [::] mean in my nginx config file](https://stackoverflow.com/questions/34305351/what-does-mean-in-my-nginx-config-file)

<!--list-separator-->

-  Action

    <!--list-separator-->
    
    -  Nginx Configuration Versioning Strategy
    
        -   [Nginx Configuration Versioning Strategy](https://stackoverflow.com/a/44163566)
        
        <!--listend-->
        
        ```sh
        # Pull changes
        git pull
        
        # Sync changes excluding .git directory
        rsync -qauh ./* "/etc/nginx" --exclude=".git"
        
        # Set proper permissions
        chmod -R 644 /etc/nginx
        find /etc/nginx -type d -exec chmod 755 {} \;
        
        # If you store SSL certs under `/etc/nginx/ssl`
        # Set proper permission for SSL certs 
        chmod -R 600 /etc/nginx/ssl
        chmod -R 400 /etc/nginx/ssl/*
        
        # Reload nginx config
        # but only if configtest is passed
        nginx -t && service nginx reload
        ```
    
    <!--list-separator-->
    
    -  Nginx 多網站配置
    
        -   [Nginx 多網站配置](#nginx-多網站配置)

<!--list-separator-->

-  Problem

    -   [How to fix 404 not found nginx problem?](https://www.digitalocean.com/community/questions/how-to-fix-404-not-found-nginx-problem)
    -   

<!--list-separator-->

-  Tools

    -   [How to Install phpMyAdmin with Nginx on Ubuntu 18.04](https://linuxize.com/post/how-to-install-phpmyadmin-with-nginx-on-ubuntu-18-04/)


#### apache2 {#apache2}

<!--list-separator-->

-  Problem

    -   [Ubuntu 安裝 phpmyadmin 並且換 Port (使用 apache)](https://yiyingloveart.blogspot.com/2015/05/ubuntu-phpmyadmin-port-apache.html)
    -   


#### Porblem {#porblem}

-   [How to Configure Nginx and Apache Together on the same Ubuntu VPS or Dedicated Server](https://hostadvice.com/how-to/how-to-configure-nginx-and-apache-together-in-ubuntu/)
-   [Replace Apache with NGINX on Ubuntu 18.04](https://lowendbox.com/blog/how-to-replace-apache-with-nginx-on-ubuntu-18-04/)


### App Server {#app-server}


#### Passenger {#passenger}

<!--list-separator-->

-  Introduction

    -   [ ] [Passenger 介紹](https://blog.infolink.com.tw/2019/passenger-introduction/)
    -   [ ] [Rails 部署工具，原來是這樣](https://5xruby.tw/posts/rails-deploy)


### database {#database}


#### PostgreSQL {#postgresql}

<!--list-separator-->

-  Install and Tutorial

    -   **[Installing PostgreSQL in Ubuntu 20.04](https://www.tecmint.com/install-postgresql-and-pgadmin-in-ubuntu/)** (useful)
    -   [Set Up a PostgreSQL Database on Linux](https://www.microfocus.com/documentation/idol/IDOL%5F12%5F0/MediaServer/Guides/html/English/Content/Getting%5FStarted/Configure/%5FTRN%5FSet%5Fup%5FPostgreSQL%5FLinux.htm)
    -   [YoLinux Tutorial: The PostgreSQL Database and Linux](http://www.yolinux.com/TUTORIALS/LinuxTutorialPostgreSQL.html)
    -   [Postgres 設定](https://oldgrayduck.blogspot.com/2012/08/postgrespostgres.html?m=1)

<!--list-separator-->

-  Initialize step

    1.  start the database server (Linux)  
        `sudo systemctl start postgresql.service`
    
    2.  enter postgresql (Linux)  
        
        ```shell
        ## method 1
        sudo su - postgres
        cd
        psql
        # or
        psql nineder_backend
        
        ## method 2
        sudo -u postgres psql nineder_backend
        ```
    
    3.  remove postgresql password  
        [PostgreSQL: Remove password requirement for user postgres](https://dba.stackexchange.com/a/126176)
    
    4.  CREATE DATABASE and EXTENSION  
        \#+begin\_src shell (psgl)  
        CREATE DATABASE nineder\_backend;  
        CREATE EXTENSION IF NOT EXISTS hstore;  
        \#+end\_SEC

<!--list-separator-->

-  Roles and Privileges

    -   [[PSQL] PostgreSQL 角色權限 Roles and Privileges](https://pjchender.dev/database/psql-roles-privilege/)
    -   [PostgreSQL 資料庫角色、使用者權限管理設定教學](https://officeguide.cc/postgresql-database-users-and-roles-configuration-tutorial/)

<!--list-separator-->

-  Extensions

    <!--list-separator-->
    
    -  hstore
    
        \#+begin\_src shell (psgl)  
        CREATE EXTENSION IF NOT EXISTS hstore;  
        \#+end\_SEC  

<!--list-separator-->

-  Command

    | command | describe          |
    |---------|-------------------|
    | \du     | List of roles     |
    | \l      | List of databases |

<!--list-separator-->

-  SQL

    <!--list-separator-->
    
    -  Create Schema
    
        Ref: <https://docs.postgresql.tw/the-sql-language/ddl/schemas>  
        
        ```sql
        CREATE SCHEMA myschema;
        ```
    
    <!--list-separator-->
    
    -  Create Role (Read Only)
    
        ```sql
        CREATE ROLE readonly WITH LOGIN;
        GRANT CONNECT ON DATABASE nineder_backend TO readonly;
        GRANT USAGE ON SCHEMA public TO readonly;
        GRANT SELECT ON ALL TABLES IN SCHEMA public TO readonly;
        ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT SELECT ON TABLES TO readonly;
        ```
        
        -   Ref: [[PSQL] PostgreSQL 角色權限 Roles and Privileges](https://pjchender.dev/database/psql-roles-privilege/)
        -   Ref: [PostgreSQL 資料庫角色、使用者權限管理設定教學](https://officeguide.cc/postgresql-database-users-and-roles-configuration-tutorial/)

<!--list-separator-->

-  Action

    <!--list-separator-->
    
    -  check current role
    
        ```sql
        SELECT current_user;  -- user name of current execution context
        -- or
        SELECT session_user;  -- session user name
        ```

<!--list-separator-->

-  Problem

    <!--list-separator-->
    
    -  Skipping acquire of configured file 'main/binary-i386/Packages'
    
        Ans: <https://stackoverflow.com/a/62547895/14740020>  
    
    <!--list-separator-->
    
    -  pgAdmin4 (web or app) doesn't have show anything
    
        Ans: [Installing PostgreSQL in Ubuntu 20.04](https://www.tecmint.com/install-postgresql-and-pgadmin-in-ubuntu/) #Accessing pgAdmin4 Web Interface  
    
    <!--list-separator-->
    
    -  How To Drop A Postgres Role/User With privileges
    
        Ans: [How To Drop A Postgres Role/User With privileges](https://dev.to/vumdao/how-to-drop-a-postgres-role-user-with-privileges-2h1i)  

<!--list-separator-->

-  ref:

    1.  [PostgreSQL 正體中文使用手冊](https://docs.postgresql.tw/)
    2.  [Reset Forgotten Password For postgres User](https://www.postgresqltutorial.com/postgresql-reset-password/)


#### mongo {#mongo}

<!--list-separator-->

-  Install and Tutorial

    -   [Install MongoDB Community Edition on Ubuntu](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/#run-mongodb-community-edition)

<!--list-separator-->

-  command

    -   add mongo database  
        
        ```shell
        
        ```


#### MySQL ( MariaDB) {#mysql--mariadb}

<!--list-separator-->

-  Install and Tutorial

    ```sh
    sudo apt install mariadb-server mariadb-client
    sudo mysql_secure_installation
    ```

<!--list-separator-->

-  Command

    <!--list-separator-->
    
    -  Database
    
        | command                    | describe          |
        |----------------------------|-------------------|
        | `SHOW DATABASES;`          | List of databases |
        | `CREATE DATABASE db_name;` | Create database   |
        | `USE [DATABASES];`         | select database   |
    
    <!--list-separator-->
    
    -  User
    
        | command                                                            | describe                                   |
        |--------------------------------------------------------------------|--------------------------------------------|
        | `CREATE USER 'root'@'localhost' IDENTIFIED BY 'password';`         | Create User                                |
        | `SELECT User, Host, Password FROM mysql.user;`                     | List of all user                           |
        | `SHOW GRANTS FOR 'bloguser'@'localhost';`                          | List grants for a mysql user               |
        | `REVOKE ALL PRIVILEGES, GRANT OPTION FROM 'bloguser'@'localhost';` | Revoke all grants for a mysql user         |
        | `DROP USER 'bloguser'@'localhost';`                                | Remove/Delete the user from the user table |
        | `ALTER USER 'root'@'localhost' IDENTIFIED BY 'password';`          | Change Password                            |
    
    <!--list-separator-->
    
    -  PRIVILEGES
    
        | command                                                        | describe                           |
        |----------------------------------------------------------------|------------------------------------|
        | `SHOW GRANTS FOR 'root'@'localhost';`                          | Show GRANT                         |
        | `GRANT ALL PRIVILEGES ON newdatabase.* TO 'user'@'localhost';` | Give PRIVILEGES                    |
        | `REVOKE ALL PRIVILEGES, GRANT OPTION FROM 'user'@'localhost';` | Revoke all grants for a mysql user |
        | `flush privileges`                                             | Refresh privileges                 |

<!--list-separator-->

-  Action

    <!--list-separator-->
    
    -  [Reset the MySQL root password](https://www.a2hosting.com/kb/developer-corner/mysql/reset-mysql-root-password)

<!--list-separator-->

-  Install Mysql 5.7

    -   [How To Install MySQL 5.7 on Ubuntu 20.04](https://computingforgeeks.com/how-to-install-mysql-on-ubuntu-focal/) (useful)
    -   [Can’t connect to local MySQL server through socket ‘/var/run/mysqld/mysqld.sock’ (2) in Linux Subsystem for Windows 10](https://medium.com/@alef.duarte/cant-connect-to-local-mysql-server-through-socket-var-run-mysqld-mysqld-sock-155d580f3a06)

<!--list-separator-->

-  Remove and Reinstall mysql

    ```shell
    sudo apt-get --purge remove "mysql*"
    sudo apt autoremove
    sudo mv /etc/mysql/ /tmp/mysql_configs/
    ```


#### Redis {#redis}

Redis is an in-memory database that persists on disk. The data model is key-value, but many different kind of values are supported: Strings, Lists, Sets, Sorted Sets, Hashes, Streams, HyperLogLogs, Bitmaps.  

<!--list-separator-->

-  Install and Tutorial

    ```sh
    sudo add-apt-repository ppa:redislabs/redis &&\
    sudo apt-get update &&\
    sudo apt-get install -y redis
    ```
    
    -   GitHub: <https://github.com/redis/redis>
    -   Official Website: <https://redis.io/>
    -   Install tutorial: <https://redis.io/download>

<!--list-separator-->

-  Ref

    -   [Amazon-Redis](https://aws.amazon.com/tw/redis/)


### Layered pattern <code>[2/4]</code> {#layered-pattern}

-   [X] [隨手 Design Pattern (2) - 軟體分層設計模式 (Software Layered Architecture Pattern)](https://raychiutw.github.io/2019/%E9%9A%A8%E6%89%8B-Design-Pattern-2-%E8%BB%9F%E9%AB%94%E5%88%86%E5%B1%A4%E8%A8%AD%E8%A8%88%E6%A8%A1%E5%BC%8F-Software-Layered-Architecture-Pattern/)
-   [X] [一次搞懂POJO、PO、DTO、VO、BO](https://hackmd.io/@MonsterLee/HJyAdgRBB)
-   [ ] [Software Architecture: The 5 Patterns You Need to Know](https://dzone.com/articles/software-architecture-the-5-patterns-you-need-to-k)
-   [ ] [DDD分層架構的三種模式](https://www.mdeditor.tw/pl/pOIC/zh-tw)


#### DTO <code>[2/4]</code> {#dto}

-   [ ] [恕我直言，在座的各位根本不會寫 Java](https://www.ipshop.xyz/13732.html)
-   [X] [DTO作用](https://blog.csdn.net/gunshuan5241/article/details/77717643)
-   [X] [深入了解DTO及如何使用DTO](https://kknews.cc/zh-tw/code/9zkxb6l.html)
-   [ ] [Data Transfer Object使用心得及時機](https://www.petekcchen.com/2010/12/how-to-use-data-transfer-object.html)


### Tools {#tools}


#### Elastic Search {#elastic-search}

Elasticsearch is a search engine based on the Lucene library. It provides a distributed, multitenant-capable full-text search engine with an HTTP web interface and schema-free JSON documents. Elasticsearch is developed in Java and is dual-licensed under the source-available Server Side Public License and the Elastic license, while other parts fall under the proprietary (source-available) Elastic License. Official clients are available in Java, .NET (C#), PHP, Python, Apache Groovy, Ruby and many other languages. According to the DB-Engines ranking, Elasticsearch is the most popular enterprise search engine followed by Apache Solr, also based on Lucene.  

<!--list-separator-->

-  Install and Tutorial

    ```sh
    # APT or YUM (RECOMMEND)(to see Install with Repositories)
    wget -qO - https://packages.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
    echo "deb https://packages.elastic.co/elasticsearch/2.x/debian stable main" | sudo tee -a /etc/apt/sources.list.d/elasticsearch-2.x.list
    sudo apt-get update && sudo apt-get install elasticsearch
    whereis elasticsearch
    sudo update-rc.d elasticsearch defaults 95 10
    sudo /bin/systemctl daemon-reload
    sudo /bin/systemctl enable elasticsearch.service
    
    # install manually
    cd ~/Downloads
    curl -L -O https://download.elastic.co/elasticsearch/release/org/elasticsearch/distribution/tar/elasticsearch/2.4.6/elasticsearch-2.4.6.tar.gz
    tar -xvf elasticsearch-2.4.6.tar.gz
    cd elasticsearch-2.4.6/bin
    ./elasticsearch
    ./elasticsearch --cluster.name my_cluster_name --node.name my_node_name
    ```
    
    -   Official Website: <https://www.elastic.co/>
    -   Install tutorial: <https://www.elastic.co/guide/en/elasticsearch/reference/index.html>
    -   Install with Repositories: <https://www.elastic.co/guide/en/elasticsearch/reference/index.html>

<!--list-separator-->

-  compare

    | RDBMS       | ElasticSearch |
    |-------------|---------------|
    | Server      | Node          |
    | DB          | Index         |
    | Table       | Type          |
    | Primary key | Id            |
    | Row         | Document      |
    | Column      | Field         |
    | Schema      | Mapping       |

<!--list-separator-->

-  Configuration

    <!--list-separator-->
    
    -  Default Configuration location
    
        `/etc/elasticsearch/elasticsearch.yml`  

<!--list-separator-->

-  Ref <code>[2/6]</code>

    -   [X] [Wiki-Elasticsearch](https://zh.wikipedia.org/wiki/Elasticsearch)
    -   [X] [介紹超強大的分散式搜尋引擎 Elasticsearch](https://its-security.blogspot.com/2018/02/introduction-elasticsearch.html)
    -   [ ] [ElasticSearch 全文字搜尋引擎 — 基本概念介紹](https://medium.com/happy-friday/elasticsearch-%E5%85%A8%E6%96%87%E5%AD%97%E6%90%9C%E5%B0%8B%E5%BC%95%E6%93%8E-%E5%9F%BA%E6%9C%AC%E6%A6%82%E5%BF%B5%E4%BB%8B%E7%B4%B9-f38a0cab9717)
    -   [ ] [Elasticsearch 系統介紹與評估](https://yuanchieh.page/posts/2020/2020-07-08%5Felasticsearch-%E4%BB%8B%E7%B4%B9%E8%88%87%E8%A9%95%E4%BC%B0/)
    -   [ ] [日誌分析平臺ELK之搜尋引擎Elasticsearch叢集](https://iter01.com/536908.html)
    -   [ ] [Elasticsearch plugin 開發環境](https://medium.com/bimap-elk/elasticsearch-plugin-%E9%96%8B%E7%99%BC%E7%92%B0%E5%A2%83-8c35dfb49445)


#### Memcached {#memcached}

<!--list-separator-->

-  Install and Tutorial

    Memcached is a high performance multithreaded event-based key/value cache store intended to be used in a distributed system.  
    
    ```sh
    sudo apt-get install libevent-dev
    sudo apt-get install memcached
    ```
    
    -   GitHub: <https://github.com/memcached/memcached>
    -   Official Website: <https://memcached.org/>
    -   Install tutorial: <https://github.com/memcached/memcached/wiki/Install>

<!--list-separator-->

-  Configuration

    <!--list-separator-->
    
    -  Default Configuration location
    
        `/etc/memcached.conf`  

<!--list-separator-->

-  Ref <code>[2/4]</code>

    -   [X] [Wiki](https://zh.wikipedia.org/wiki/Memcached)
    -   [X] [Amazon-Memcached](https://aws.amazon.com/tw/memcached/)
    -   [ ] [Logstash：运用 memcache 过滤器进行大规模的数据丰富](https://blog.csdn.net/UbuntuTouch/article/details/106915969)
    -   [ ] [很詳細的memcache介紹——工作流程、實現原理、訪問模型和指令匯總](https://kknews.cc/zh-tw/code/n94ye65.html)


#### ImageMagick {#imagemagick}

ImageMagick is a free and open-source cross-platform software suite for displaying, creating, converting, modifying, and editing raster images. Created in 1987 by John Cristy, it can read and write over 200 image file formats. It and its components are widely used in open-source applications.  

```sh
cd ~/Downloads &&\
git clone --depth 1 https://github.com/ImageMagick/ImageMagick.git ImageMagick-7.0.11 &&\
cd ImageMagick-7.0.11 &&\
./configure &&\
make

./configure --with-modules
sudo make install
sudo ldconfig /usr/local/lib
/usr/local/bin/convert logo: logo.gif
magick identify -version
```

-   GitHub: <https://github.com/ImageMagick/ImageMagick>
-   Official Website: <https://imagemagick.org/index.php>
-   Install tutorial: <https://imagemagick.org/script/install-source.php>


#### jwt.io [jwt.io](https://jwt.io/) {#jwt-dot-io-jwt-dot-io}

JSON Web Tokens are an open, industry standard RFC 7519 method for representing  
claims securely between two parties.  
JWT.IO allows you to decode, verify and generate JWT.  


#### Swagger {#swagger}


#### phpmyadmin {#phpmyadmin}

-   Official Website: <https://www.phpmyadmin.net/>
-   Documentation: <https://docs.phpmyadmin.net/en/latest/>

<!--list-separator-->

-  Install

    ```sh
    sudo apt-get install phpmyadmin -y
    ```
    
    -   [How to Install phpMyAdmin with Nginx on Ubuntu 18.04](https://linuxize.com/post/how-to-install-phpmyadmin-with-nginx-on-ubuntu-18-04/)

<!--list-separator-->

-  Problem

    -   [PhpMyAdmin got 404 not found error on nginx ubuntu 16.04](https://www.digitalocean.com/community/questions/phpmyadmin-got-404-not-found-error-on-nginx-ubuntu-16-04)


## DevOps {#devops}


### CI/CD流程 {#ci-cd流程}

-   jenins => docker => harbor => k8s


#### Jenkins {#jenkins}

<!--list-separator-->

-  Install

    ```sh
    wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
    sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > \
        /etc/apt/sources.list.d/jenkins.list'
    sudo apt-get update
    sudo apt-get install jenkins
    ```
    
    -   Official Website: <https://www.jenkins.io/>
    -   Install tutorial: <https://www.jenkins.io/download/>

<!--list-separator-->

-  Step:

    1.  start jenkins  
        
        ```sh
        sudo systemctl start jenkins
        sudo systemctl enable jenkins
        ```
    2.  Jenkins Port 加入防火牆  
        
        ```sh
        firewall-cmd --permanent —add-port=8080/tcp
        firewall-cmd --reload
        ```
    3.  進入&解鎖 Jenkins  
        開啟 Jenkins 頁面 <http://localhost:8080>  
        (Ex. <http://127.0.0.1:8080>)  
        從 initialAdminPassword 檔案(紅字部份)取得密碼並解鎖
    4.  選擇自訂安裝方式  
        -   select github, gitlab Plug-in

<!--list-separator-->

-  Plugins

    1.  Local - force Jenkins to show UI always in English?  
        Ref: <https://superuser.com/a/1335820>


#### Capistrano {#capistrano}

-   [X] [Rails 部署工具，原來是這樣](https://5xruby.tw/posts/rails-deploy)


### DNS {#dns}

-   <https://www.icann.org/>
-   [PM筆記：HTTPS、A紀錄與CNAME](https://medium.com/%E4%B8%80%E5%80%8B%E4%BA%BA%E7%9A%84%E6%96%87%E8%97%9D%E5%BE%A9%E8%88%88/pm%E7%AD%86%E8%A8%98-https-a%E7%B4%80%E9%8C%84%E8%88%87cname-91f6f2a1ee2f)
-   [Wildcard '\*' versus Exact Match '@' DNS records](https://www.apexdigital.co.nz/blog/wildcard-versus-exact-match-dns-records/)


### Docker {#docker}


#### official website {#official-website}

1.  [dockerhub](https://hub.docker.com/)
2.  [Docker: Empowering App Development for Developers](https://www.docker.com/)


#### Docker Compose {#docker-compose}

Ref:  

-   [Docker Compose – 安裝教學、指令用法及官方範例說明](https://www.jinnsblog.com/2020/12/docker-compose-tutorial.html)


#### Install & tutorial {#install-and-tutorial}

Install Docker Engine on Ubuntu: <https://docs.docker.com/engine/install/ubuntu/>  
Tutorial: [全面易懂的Docker指令大全](https://joshhu.gitbooks.io/dockercommands/content/)  


#### Command {#command}

| main      | command                                                                                            | describe                                          | Ref                                                                           |
|-----------|----------------------------------------------------------------------------------------------------|---------------------------------------------------|-------------------------------------------------------------------------------|
| `images`  | `docker images`                                                                                    | List images                                       |                                                                               |
| `create`  | `docker create [OPTIONS] IMAGE [COMMAND] [ARG...]`                                                 | Create a new container                            | [docker creat](https://docs.docker.com/engine/reference/commandline/create/)  |
| `ps`      | `docker ps`                                                                                        | List containers                                   |                                                                               |
| `pull`    | `docker pull [OPTIONS] NAME[:TAG @DIGEST]`                                                         | Pull an image or a repository from a registry     |                                                                               |
| `kill`    | `docker kill [OPTIONS] CONTAINER [CONTAINER...]`                                                   | Kill one or more running containers               |                                                                               |
| `rm`      | `docker rm $(docker ps -aq)`                                                                       | Kill all running containers                       |                                                                               |
| `run`     | `docker run -it --name cat --user test centos:latest /bin/sh`                                      | run image                                         |                                                                               |
| `exec`    | `docker exec -it <container name> <command>`                                                       |                                                   |                                                                               |
| `commit`  | `docker commit  [OPTIONS] CONTAINER [REPOSITORY[:TAG]]`                                            |                                                   | [docker commit](https://docs.docker.com/engine/reference/commandline/commit/) |
| `restart` | `docker restart <container name>`                                                                  |                                                   |                                                                               |
|           | `docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' container_name_or_id` | get a Docker container's IP address from the host |                                                                               |
|           |                                                                                                    |                                                   |                                                                               |


#### ref: {#ref}

1.  [X] [Install Docker Desktop on Windows (docker docs)](https://docs.docker.com/docker-for-windows/install/)
2.  [ ] [【Docker入門教學】](https://www.youtube.com/watch?v=bumV64OfLCs&list=PLliocbKHJNwubNT2oK-xlB1GXTXuLFb0I)(youtube)
3.  [X] [Docker 基礎概念 101](https://github.com/HcwXd/docker-tutorial)
4.  [ ] [Docker —— 從入門到實踐 正體中文版](https://philipzheng.gitbook.io/docker%5Fpractice/)


#### docker + wsl {#docker-plus-wsl}

1.  [ ] [在 WSL 2 上開始使用 Docker 遠端容器](https://docs.microsoft.com/zh-tw/windows/wsl/tutorials/wsl-containers)
2.  [ ] [WSL 與 Windows 的完美雙結合 — 在WSL 中安裝 Docker](https://medium.com/%E4%B8%80%E5%80%8B%E5%B0%8F%E5%B0%8F%E5%B7%A5%E7%A8%8B%E5%B8%AB%E7%9A%84%E9%9A%A8%E6%89%8B%E7%AD%86%E8%A8%98/wsl-%E8%88%87-windows-%E7%9A%84%E5%AE%8C%E7%BE%8E%E9%9B%99%E7%B5%90%E5%90%88-%E5%9C%A8wsl-%E4%B8%AD%E5%AE%89%E8%A3%9D-docker-e722e87ffa3b)
3.  [ ] [最近開始改用 WSL2 跑 docker 當開發環境](https://www.pigo.idv.tw/archives/3359)


#### Problem {#problem}

1.  [Change the location of docker images (windows-WSL2)](https://stackoverflow.com/questions/62441307/how-can-i-change-the-location-of-docker-images-when-using-docker-desktop-on-wsl2)

<span class="timestamp-wrapper"><span class="timestamp">[2020-12-21 Mon 22:10]</span></span>  


### Docker-compose {#docker-compose}


#### Install & tutorial {#install-and-tutorial}

-   [Install Docker Compose](https://docs.docker.com/compose/install/)
-   [Docker and Docker Compose on Raspberry Pi OS](https://withblue.ink/2020/06/24/docker-and-docker-compose-on-raspberry-pi-os.html)


### K8s {#k8s}


### minikube {#minikube}


### GCP {#gcp}


#### Backup VM instances {#backup-vm-instances}

`Flow: VM instances => Images => Cloud Storges => Download`  

1.  Stop `VM instances` (not recommend Keep instance running)  
    ![](/ox-hugo/Backup_VM_instances-stop.png)
2.  find `Vm instance disk name` (要備份disk的名稱)  
    ![](/ox-hugo/Backup_VM_instances-vm_boot_disk.png)
3.  Create image  
    Go to Images => CREATE IMAGE  
    ![](/ox-hugo/Backup_VM_instances-Create_img_button.png)  
    Enter and Create  
    ![](/ox-hugo/Backup_VM_instances-Create_Image.png)
4.  Check GCS have Bucket  
    ![](/ox-hugo/Backup_VM_instances-check_bucket.png)
5.  Select Images  
    ![](/ox-hugo/Backup_VM_instances-Select_Image.png)
6.  Export Images  
    ![](/ox-hugo/Backup_VM_instances-Export-Image.png)  
    Option  
    ![](/ox-hugo/Backup_VM_instances-Export-Image_Options.png)
7.  Go to Cloud Storage (your Store location), find your file(XXX.vmdk, XXX.vhdx, XXX.vpc, XXX.qcow2) and `Click Download`  
    ![](/ox-hugo/Backup_VM_instances-Downlaod_img.png)
8.  儲存到Google Drive

Note:  

1.  沒有辨法直接將GCS的資料存儲至Google drive, 需手動下載GCS的資料, 再上傳至Google Drive
2.  排程: 沒有自動排程的介面, 若真的有排程需求, 只能透過 `gcloud` 指令 + crontab 來達成


#### Restore VM instances: {#restore-vm-instances}

前提: 要回復的img有在GCS上面  

1.  至 GCE 的 Images 點選 `CREATE IMAGES`  
    ![](/ox-hugo/Restore_VM_instances-Create-img.png)
2.  Create Images  
    ![](/ox-hugo/Restore_VM_instances-Create-img-option.png)
3.  回復 instance  
    ![](/ox-hugo/Restore_VM_instances-restore_instance.png)
4.  按照想要的配置建立後，即可完成回復


#### GCE disk price {#gce-disk-price}

<!--list-separator-->

-  關於 `Regions and Zones`

    可參考: [Available regions and zones](https://cloud.google.com/compute/docs/regions-zones#available)  
    Regional: zones的集合, ex: asia-east1, northamerica-northeast1  
    Zonal: ex: asia-east1-a, asia-east1-b, northamerica-northeast1-a, northamerica-northeast1-b, etc.  

<!--list-separator-->

-  [GCP存儲選項](https://cloud.google.com/compute/docs/disks?hl=zh-tw)

    -   [Zonal persistent disk](https://cloud.google.com/compute/docs/disks?hl=zh-tw#pdspecs): Efficient, reliable block storage.
    -   [Regional persistent disk](https://cloud.google.com/compute/docs/disks?hl=zh-tw#repds): Regional block storage `replicated in two zones.` `(在同一個Region做異地備份)`
    -   [Local SSD](https://cloud.google.com/compute/docs/disks?hl=zh-tw#localssds): High performance, transient, local block storage.
    -   [Cloud Storage buckets](https://cloud.google.com/compute/docs/disks?hl=zh-tw#gcsbuckets): Affordable object storage. `(可以連接至 Google Cloud Storage的資料)`
    -   [Filestore](https://cloud.google.com/filestore/docs/mounting-fileshares?hl=zh-tw): High performance file storage for Google Cloud users. `share on a Compute Engine virtual machine (VM) instance` ( [use mount or etc](https://cloud.google.com/filestore/docs/mounting-fileshares?hl=zh-tw) )
    
    |                               | Zonal standard PD                                                                                                        | Regional standard PD                                                                                                     | Zonal balanced PD                                                                                                        | Regional balanced PD                                                                                                     | Zonal SSD PD                                                                                                         | Regional SSD PD                                                                                                     | Zonal extreme PD                                                                                                         | Local SSDs                                                                                             | Cloud Storage buckets                                                                |
    |-------------------------------|--------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
    | Storage type                  | Efficient and reliable block storage                                                                                     | Efficient and reliable block storage with synchronous replication across two zones in a region                           | Cost-effective and reliable block storage                                                                                | Cost-effective and reliable block storage with synchronous replication across two zones in a region                      | Fast and reliable block storage                                                                                      | Fast and reliable block storage with synchronous replication across two zones in a region                           | Highest performance persistent block storage option                                                                      | High performance local block storage                                                                   | Affordable object storage                                                            |
    | Minimum capacity per disk     | 10 GB                                                                                                                    | 200 GB                                                                                                                   | 10 GB                                                                                                                    | 10 GB                                                                                                                    | 10 GB                                                                                                                | 10 GB                                                                                                               | 200 GB                                                                                                                   | 375 GB                                                                                                 | n/a                                                                                  |
    | Maximum capacity per disk     | 64 TB                                                                                                                    | 64 TB                                                                                                                    | 64 TB                                                                                                                    | 64 TB                                                                                                                    | 64 TB                                                                                                                | 64 TB                                                                                                               | 64 TB                                                                                                                    | 375 GB                                                                                                 | n/a                                                                                  |
    | Capacity increment            | 1 GB                                                                                                                     | 1 GB                                                                                                                     | 1 GB                                                                                                                     | 1 GB                                                                                                                     | 1 GB                                                                                                                 | 1 GB                                                                                                                | 1 GB                                                                                                                     | 375 GB                                                                                                 | n/a                                                                                  |
    | Maximum capacity per instance | 257 TB\*                                                                                                                 | 257 TB\*                                                                                                                 | 257 TB\*                                                                                                                 | 257 TB\*                                                                                                                 | 257 TB\*                                                                                                             | 257 TB\*                                                                                                            | 257 TB\*                                                                                                                 | 9 TB                                                                                                   | Almost infinite                                                                      |
    | Scope of access               | Zone                                                                                                                     | Zone                                                                                                                     | Zone                                                                                                                     | Zone                                                                                                                     | Zone                                                                                                                 | Zone                                                                                                                | Zone                                                                                                                     | Instance                                                                                               | Global                                                                               |
    | Data redundancy               | Zonal                                                                                                                    | Multi-zonal                                                                                                              | Zonal                                                                                                                    | Multi-zonal                                                                                                              | Zonal                                                                                                                | Multi-zonal                                                                                                         | Zonal                                                                                                                    | None                                                                                                   | Regional, dual-regional or multi-regional                                            |
    | Encryption at rest            | Yes                                                                                                                      | Yes                                                                                                                      | Yes                                                                                                                      | Yes                                                                                                                      | Yes                                                                                                                  | Yes                                                                                                                 | Yes                                                                                                                      | Yes                                                                                                    | Yes                                                                                  |
    | Custom encryption keys        | Yes                                                                                                                      | Yes                                                                                                                      | Yes                                                                                                                      | Yes                                                                                                                      | Yes                                                                                                                  | Yes                                                                                                                 | Yes                                                                                                                      | No                                                                                                     | Yes                                                                                  |
    | Machine type support          | All machine types                                                                                                        | All machine types                                                                                                        | Most machine types                                                                                                       | Most machine types                                                                                                       | Most machine types                                                                                                   | Most machine types                                                                                                  | Most machine types                                                                                                       | Most machine types                                                                                     | All machine types                                                                    |
    | How-to                        | [Add a standard persistent disk](https://cloud.google.com/compute/docs/disks/add-persistent-disk?hl=zh-tw#create%5Fdisk) | [Add a regional standard persistent disk](https://cloud.google.com/compute/docs/disks/regional-persistent-disk?hl=zh-tw) | [Add a balanced persistent disk](https://cloud.google.com/compute/docs/disks/add-persistent-disk?hl=zh-tw#create%5Fdisk) | [Add a regional balanced persistent disk](https://cloud.google.com/compute/docs/disks/regional-persistent-disk?hl=zh-tw) | [Add an SSD persistent disk](https://cloud.google.com/compute/docs/disks/add-persistent-disk?hl=zh-tw#create%5Fdisk) | [Add a regional SSD persistent disk](https://cloud.google.com/compute/docs/disks/regional-persistent-disk?hl=zh-tw) | [Add an extreme persistent disk](https://cloud.google.com/compute/docs/disks/add-persistent-disk?hl=zh-tw#create%5Fdisk) | [Add a local SSD](https://cloud.google.com/compute/docs/disks/local-ssd?hl=zh-tw#create%5Flocal%5Fssd) | [Connect a bucket](https://cloud.google.com/compute/docs/disks/gcs-buckets?hl=zh-tw) |

<!--list-separator-->

-  [磁碟類型](https://cloud.google.com/compute/docs/disks?hl=zh-tw#introduction)

    -   **標準永久性磁盤** (pd-standard) 由[标准普通硬盘 (HDD)](https://en.wikipedia.org/wiki/Hard%5Fdisk%5Fdrive) 提供支持, 適用於主要使用順序 I/O 的大型數據處理工作負載。
    -   **平衡永久性磁盤** (pd-balanced) 由[固态硬盘 (SSD)](https://en.wikipedia.org/wiki/Solid-state%5Fdrive) 提供支持, 是 SSD 永久性磁盤的替代方案，用於平衡性能和費用。由於平衡永久性磁盤與SSD 永久性磁盤具有相同的最大IOPS，並且每GB 的IOPS 更低，因此平衡永久性磁盤提供的性能水平適合大多數通用應用，價位介於標準永久性磁盤和SSD 永久性磁盤之間。
    -   **SSD 永久性磁盤** (pd-ssd) 由[固态硬盘 (SSD)](https://en.wikipedia.org/wiki/Solid-state%5Fdrive) 提供支持,適用於滿足企業應用和高性能數據庫的需求，與標準永久性磁盤相比，SSD 永久性磁盤具有更短的延遲時間和更多的 IOPS。 `SSD 永久性磁盤的設計旨在確保將延遲時間控制在數毫秒以內；實際的延遲時間取決於具體的應用。`
    
    {{< figure src="/ox-hugo/GCE-Disk-Price_Storage-Option.png" >}}  

<!--list-separator-->

-  [磁碟定價](https://cloud.google.com/compute/disks-image-pricing#disk)

    `所有磁碟相關費用皆會以使用秒數按比例計費`  
    以美國為例，200 GB 標準永久磁碟區整個月的費用為 $8.00 美元；如果您只佈建了半個月，則費用為 $4.00 美元。同樣地，200 GB SSD 永久磁碟區整個月的費用為 $34.00 美元；如果您只佈建了半個月，則費用為 $17.00 美元。  
    佈建的磁碟空間包含所有已使用和未使用的空間。如果您佈建了 200 GB 磁碟，無論您的使用情形為何，系統會向您收取整個磁碟空間的費用，直到您釋出磁碟空間為止。  
    
    <!--list-separator-->
    
    -  [永久磁碟定價](https://cloud.google.com/compute/disks-image-pricing?hl=zh-tw#persistentdisk) - 台灣 (asia-east1)
    
        | Type                                | Price (per GB / month in USD) |
        |-------------------------------------|-------------------------------|
        | Standard provisioned space          | $0.040                        |
        | SSD provisioned space               | $0.170                        |
        | Balanced provisioned space          | $0.100                        |
        | Regional standard provisioned space | $0.080                        |
        | Regional SSD provisioned space      | $0.340                        |
        | Regional balanced provisioned space | $0.200                        |
        | Snapshot storage                    | $0.026                        |
        | Multi-regional snapshot storage     | $0.026                        |
        | I/O operations                      | No additional charge          |
    
    <!--list-separator-->
    
    -  [永久磁碟快照](https://cloud.google.com/compute/disks-image-pricing?hl=zh-tw#persistent%5Fdisk%5Fsnapshots)
    
        如果專案中有任何快照，您每個月都必須支付相關的儲存空間費用。在您建立或還原快照時，系統可能也會根據快照的儲存位置向您收取網路費用  
    
    <!--list-separator-->
    
    -  [本機 SSD 定價](https://cloud.google.com/compute/disks-image-pricing?hl=zh-tw#localssdpricing) - 台灣 (asia-east1)
    
        | 類型            | 價格 (每 GB 月費，以美元計價) | 先占價格 (每 GB 月費，以美元計價) | 承諾使用 1 年的價格 (每 GB 月費，以美元計價) | 承諾使用 3 年的價格 (每 GB 月費，以美元計價) |
        |---------------|--------------------|----------------------|-----------------------------|-----------------------------|
        | 已佈建的本機 SSD 儲存空間 | $0.080             | $0.048               | $0.051 美元                 | $0.036 美元                 |

<!--list-separator-->

-  總結

    1.  在一般使用情況下, 若負載不大, 可使用標準儲存空間(Standard provisioned space)
    2.  若要平衡性能和費用, 可選擇 **平衡永久性磁盤** (pd-balanced) 由於平衡永久性磁盤與SSD 永久性磁盤具有相同的最大IOPS，並且每GB 的IOPS 更低，因此平衡永久性磁盤提供的性能水平適合大多數通用應用，價位介於標準永久性磁盤和SSD 永久性磁盤之間。
    3.  高性能要求: 使用 **SSD 永久性磁盤** (pd-ssd)
    4.  如果資料要異地備份, 則需要使用 [Regional persistent disk](https://cloud.google.com/compute/docs/disks?hl=zh-tw#repds)


#### Transferring data between Google Drive and Google Cloud Storage using Google Colab {#transferring-data-between-google-drive-and-google-cloud-storage-using-google-colab}

<https://philipplies.medium.com/transferring-data-from-google-drive-to-google-cloud-storage-using-google-colab-96e088a8c041>  


## Project {#project}


### Wordpres {#wordpres}


#### Child Theme {#child-theme}

-   [Home / Theme Handbook / Advanced Theme Topics / Child Themes](https://developer.wordpress.org/themes/advanced-topics/child-themes/)