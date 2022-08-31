+++
title = "Program Design"
author = ["Shawn Dennis Lin"]
date = 2021-09-09T00:00:00+08:00
draft = false
+++

## Program Design {#program-design}

-   [常見的五個開源專案授權條款，使用軟體更自由](https://noob.tw/open-source-licenses/)

### namespace {#namespace}

-   [ ] [命名空間 - wiki](https://zh.wikipedia.org/wiki/%E5%91%BD%E5%90%8D%E7%A9%BA%E9%97%B4)
-   [ ] [2.1.1. 匿名命名空間 - Google 開源專案風格指南(繁體中文版)](https://tw-google-styleguide.readthedocs.io/en/latest/google-cpp-styleguide/scoping.html)

### HardCode {#hardcode}

## C/C++

+ [Day 11: 中場休息 CMake 教學 - iT 邦幫忙::一起幫忙解決難題，拯救 IT 人的一天](https://ithelp.ithome.com.tw/articles/10221101)

## JAVA {#java}

1.  java structure of web
2.  maven vs Gradle
3.  SpringBoot structure
4.  Familiar with object-oriented concepts(bring java book)
5.  Finish reading [Java SE 6 技術手冊](https://caterpillar.gitbooks.io/javase6tutorial/content/c4%5F1.html)(8 or 11 up), [SpringBoot](https://morosedog.gitlab.io/springboot-20190313-springboot1/)

### API {#api}

-   [Web API 設計](https://docs.microsoft.com/zh-tw/azure/architecture/best-practices/api-design)
-   [Spring Boot-第2課-設計RESTful API](https://medium.com/chikuwa-tech-study/spring-boot-%E7%AC%AC2%E8%AA%B2-restful-api%E4%BB%8B%E7%B4%B9-955f776da32d)
-   [淺談 REST 軟體架構風格 (Part.I) - 從了解 REST 到設計 RESTful！](https://blog.toright.com/posts/725/representational-state-transfer-%E8%BB%9F%E9%AB%94%E6%9E%B6%E6%A7%8B%E9%A2%A8%E6%A0%BC%E4%BB%8B%E7%B4%B9-part-i-%E5%BE%9E%E4%BA%86%E8%A7%A3-rest-%E5%88%B0%E8%A8%AD%E8%A8%88-restful%EF%BC%81.html)

#### else {#else}

-   [開源框架: Spring Gossip](https://openhome.cc/Gossip/SpringGossip/)
-   [HTTP Status](https://developer.mozilla.org/zh-TW/docs/Web/HTTP/Status)

#### QA {#qa}

Q1. 為什麼在Service定義過了method, 在Repository還要定義一次?  

### Spring {#spring}

#### run spring-boot project {#run-spring-boot-project}

```sh
./mvnw spring-boot:run
```

#### Spring bean {#spring-bean}

-   [Spring Boot-第6課-元件的運用與交互關係](https://medium.com/chikuwa-tech-study/spring-boot-%E7%AC%AC6%E8%AA%B2-%E5%85%83%E4%BB%B6%E7%9A%84%E9%81%8B%E7%94%A8%E8%88%87%E4%BE%9D%E8%B3%B4-8bb3bf1d4a28)

#### Spring Security {#spring-security}

-   JWT [JWT(JSON Web Token) — 原理介紹](https://medium.com/%E4%BC%81%E9%B5%9D%E4%B9%9F%E6%87%82%E7%A8%8B%E5%BC%8F%E8%A8%AD%E8%A8%88/jwt-json-web-token-%E5%8E%9F%E7%90%86%E4%BB%8B%E7%B4%B9-74abfafad7ba)

#### annotation {#annotation}

1.  @Restcontroller
2.  @PostConstruct [@PostConstruct註解](https://iter01.com/512905.html)
3.  [@Entity, @Table](https://blog.csdn.net/u013517229/article/details/89307158)
4.  [@Controller, @Service, @Repository, @Autowired, @Resource, @Component, @Qualifier](https://codertw.com/%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80/488347/)
5.  @AutoWired  
    -   使用@Autowired標記的全域變數，其資料型態必須是有添加特定標記的類別，  
        如「@Service」與「@Repository」等。
    -   [Spring Boot-第6課-元件的運用與交互關係](https://medium.com/chikuwa-tech-study/spring-boot-%E7%AC%AC6%E8%AA%B2-%E5%85%83%E4%BB%B6%E7%9A%84%E9%81%8B%E7%94%A8%E8%88%87%E4%BE%9D%E8%B3%B4-8bb3bf1d4a28)
6.  @Column [@Column](https://openhome.cc/Gossip/EJB3Gossip/FirstLocalJPA.html)

#### Hibernate {#hibernate}

-   update(Hibernate 2): [Hibernate更新某些欄位的幾種update方法](https://www.itread01.com/p/1398516.html)
-   update(Hibernate 3): [Hibernate 3 更新、刪除](https://openhome.cc/Gossip/HibernateGossip/UpdateDelete.html)

#### JBDC <code>[0/1]</code> {#jbdc}

-   [ ] how to controller user role in postgresQL

#### dependency {#dependency}

1.  JUnit

### Swagger {#swagger}

-   API [swagger注释API](https://blog.csdn.net/chinassj/article/details/81875038)
-   JWT token in header  
    [Spring Boot & Swagger UI. Set JWT token](https://stackoverflow.com/a/61341986)  
    [Set JWT with Spring Boot and Swagger UI](https://www.baeldung.com/spring-boot-swagger-jwt)

### adplatformbackend (project) {#adplatformbackend--project}

-   <https://adapi.isp99.com:8000/ad/>
-   <http://127.0.0.1:8000/api/swagger-ui.html>
-   <http://192.168.3.24:8000/api/swagger-ui.html>

#### run project {#run-project}

<!--list-separator-->

-  project

    ./mvnw spring-boot:run  
    \#+end\_src  

#### Question {#question}

1.  `variable in DTO` is reference to `Entity` ? (`AdPost`)
2.  how to ensure below:  
    
    ```java
    @ApiModelProperty(hidden = true)
    @JsonProperty(value = "XXX", required = true)
    ```
3.  So many `@ApiModelProperty(hidden = true)` in `Entity`, need to refactor to DTO?
4.  Both have `@JsonProperty(value = "short_url")` in `Entity` and `DTO` and it's the same variable, why?
5.  res? result? is equal to `basicDto.setResult?` or `.setMessage`?  
    need to add basic DTO?
6.  how to ensure the change is successful ? (program will run normal)  
    -   use swagger?

## Python {#python}

-   [My Python Library](https://github.com/shdennlin/python-library)
-   [Python 程式碼風格指引](https://iottalk.vip/static/pystyle/index.html)
-   [结构化您的工程](https://pythonguidecn.readthedocs.io/zh/latest/writing/structure.html)

### dereactor {#dereactor}

-   [Property](https://www.maxlist.xyz/2019/12/25/python-property/)

### Tools {#tools}

#### Poetry {#poetry}

-   Github: <https://github.com/python-poetry/poetry>
-   My basic configuration:  
    
    ```toml
    [tool.poetry]
    name = "<Project Name>"
    version = "1.0.0"
    description = "<Project Description>"
    authors = ["shdennlin <shawndennislin@gmail.com>"]
    
    [tool.poetry.dependencies]
    python = ">=3.8"
    
    [tool.poetry.dev-dependencies]
    jedi = ">=0.13.0"
    json-rpc = ">=1.8.1"
    service-factory = ">=0.1.5"
    flake8 = "^4.0.1"
    autoflake = "^1.4"
    importmagic = "^0.1.7"
    epc = "^0.0.5"
    yapf = "^0.31.0"
    toml = "^0.10.2"
    isort = "^5.10.1"
    
    [build-system]
    requires = ["poetry-core>=1.0.0"]
    build-backend = "poetry.core.masonry.api"
    ```

### Module {#module}

#### Click {#click}

-   [click.palletsprojects.com - 8.0.x](https://click.palletsprojects.com/en/8.0.x/)
-   [Python 用 Click 模組製作好用的指令](https://myapollo.com.tw/zh-tw/python-click/)

### Framework {#framework}

#### flask {#flask}

#### django {#django}

## Ruby on Rails {#ruby-on-rails}

-   introduction: [Ruby on Rails 伺服器的選擇](https://blog.chh.tw/posts/ruby-on-rails-server-options/)

### RVM {#rvm}

```text
export GEM_HOME=$HOME/.gem
```

add this in file ~/.bashrc  

#### Command {#command}

| man   | command                          | describe    | Ref |
|-------|----------------------------------|-------------|-----|
| `rvm` |                                  |             |     |
|       | `rvm list known`                 |             |     |
|       | `rvm get master`                 | update list |     |
|       | `rvm install 2.3.8`              |             |     |
|       | `rvm list`                       |             |     |
|       | `rvm alias create default 2.3.8` |             |     |
|       | `rvm use ruby-2.3.8`             |             |     |
|       | `ruby -v`                        |             |     |
|       | `rvm info`                       |             |     |
|       | `source ~/.rvm/scripts/rvm`      |             |     |

-   Official Website: <https://rvm.io/>
-   Install tutorial: <https://rvm.io/rvm/install>
-   Ref: [環境設定 為你自己學 Ruby on Rails](https://railsbook.tw/chapters/02-environment-setup.html)

#### Action {#action}

<!--list-separator-->

-  install bundler that matches with your `Gemfile.lock` use:

    `gem install bundler -v "$(grep -A 1 "BUNDLED WITH" Gemfile.lock | tail -n 1)"`  

<!--list-separator-->

-  downgrade\_rubygems

    ```sh
    $ gem -v
    2.0.3
    $ gem list rubygems-update
    $ gem uninstall -v 2.0.3 rubygems-update 
    
    $ gem install -v 1.8.24 rubygems-update
    $ update_rubygems
    $ gem -v
    1.8.24
    ```
    
    <https://gist.github.com/mmasashi/8245238>  

<!--list-separator-->

-  downgrade bundler

    ```sh
    gem install bundler:1.16.1 --default
    
    =Remove/delete the bundler.gemspec=
    
    ```

#### Tools {#tools}

-   [bundle-bungler](https://github.com/chrismo/bundle-bungler)  
    Bounce bundled gems between a local project folder and a shared location.

### Template {#template}

#### ERB {#erb}

#### Slim {#slim}

introduction: <https://symphonyh.github.io/cloudblog/2017/03/06/slim/>  

### Plugins {#plugins}

#### Capistrano {#capistrano}

<!--list-separator-->

-  使用capistrano从不同的git分支进行部署

    [使用capistrano从不同的git分支进行部署](https://www.codenong.com/1524204/)  

### Shell Script {#shell-script}

-   Tutorial: <http://linux.vbird.org/linux%5Fbasic/0340bashshell-scripts.php>

#### command {#command}

-   test (**-e**, **-f**, etc.)  
    <http://linux.vbird.org/linux%5Fbasic/0340bashshell-scripts.php#test>

## Design Pattern {#design-pattern}

### The Strategy Pattern {#the-strategy-pattern}

### The Observer Pattern: Keeping your Objects in the know {#the-observer-pattern-keeping-your-objects-in-the-know}

### The Decorator Pattern: Decorating Objects {#the-decorator-pattern-decorating-objects}

### The Factory Pattern: Baking with OO Goodness {#the-factory-pattern-baking-with-oo-goodness}

### The Singleton Pattern: One of a Kind Objects {#the-singleton-pattern-one-of-a-kind-objects}

### The Command Pattern: Encapsulating Invocation {#the-command-pattern-encapsulating-invocation}

### The Adapter and Facade Patterns: Being Adaptive {#the-adapter-and-facade-patterns-being-adaptive}

### The Template Method Pattern: Encapsulating Algorithms {#the-template-method-pattern-encapsulating-algorithms}

### The Iterator and Composite Patterns: Well-Managed Collections {#the-iterator-and-composite-patterns-well-managed-collections}

### The State Pattern: The State of Things {#the-state-pattern-the-state-of-things}

### The Proxy Pattern: Controlling Object Access {#the-proxy-pattern-controlling-object-access}

### Compound Patterns: Patterns of Patterns {#compound-patterns-patterns-of-patterns}

### Better Living with Patterns: Patterns in the Real World {#better-living-with-patterns-patterns-in-the-real-world}

### Leftover Patterns {#leftover-patterns}

### Ref book {#ref-book}

-   _Head First Design Patterns_ -> [Welcome to Head First Design Patterns](https://www.wickedlysmart.com/head-first-design-patterns/), [Table of contents](https://www.oreilly.com/library/view/head-first-design/0596007124/)