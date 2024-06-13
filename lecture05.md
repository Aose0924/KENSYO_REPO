# 第５回課題  
## 全体構成図
### EC2インスタンス×2、S3ストレージ×1、ALB×1の構成とする。  
  
![構成図](/構成図.svg)  
  
## EC2 上にサンプルアプリケーションをデプロイして動作（サンプルは第 3 回で案内済みのものを使用）  
### 事前準備（パッケージ導入） ap-northeast-1a/ap-northeast-1c 
  
#### git導入  
sudo su -  
yum update  
yum install git  
git clone https://github.com/yuta-ushijima/raisetech-live8-sample-app  
  
#### EC2 instance connect接続設定  
yum list installed | grep ec2-instance-connect  
yum list installed jq || sudo yum install -y jq  
curl -s https://ip-ranges.amazonaws.com/ip-ranges.json | \  
   jq '.prefixes[] | select(.region == "ap-northeast-1" and .service == "EC2_INSTANCE_CONNECT")'  
  
####リージョン確認  
curl -s http://169.254.169.254/latest/meta-data/local-hostname | cut -d '.' -f2  
aws ec2 enable-serial-console-access --region  
  
#### RVM導入  
gem install rvm  
gpg2 --keyserver hkp://keyserver.ubuntu.com --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB   
curl -sSL https://get.rvm.io | bash -s stable  
usermod -G rvm ec2-user  
  
#### ruby-3.2.3導入  
rvm install "ruby-3.2.3"  
rvm use 3.2.3  
  
#### bundler導入  
gem install bundler -v 2.3.14  
  
#### NVM導入  
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash  
source ~/.bashrc  
nvm --version  
nvm install 17.9.1  
  
####NPM導入  
npm install -g yarn@1.22.19  
  
#### rails導入  
gem install rails -v 7.1.3.2  
  
#### mysql接続  
yum -y install mysql  
mysql -u admin -p -h raisetech5.cjcyo6gekjgm.ap-northeast-1.rds.amazonaws.com  
  
#### brew導入  
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"  
(echo; echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"') >> /home/ec2-user/.bashrc  
eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"  
sudo yum groupinstall 'Development Tools'  
brew install gcc  
brew install libxml2  
gem install nokogiri -v '1.10.10'  -- --use-system-libraries --with-xml2-include=$(brew --prefix libxml2)/include/libxml2
  
#### openssl導入  
brew install openssl  
gem install mysql2 -v '0.5.6' -- --with-opt-dir="$(brew --prefix openssl)"  
gem update --system 3.5.9  
  
#### bundle導入  
yum install mysql-devel  
cd raisetech-live8-sample-app/  
bundle install  
  
#### MYSQLセットアップ 
cd raisetech-live8-sample-app/  
cat config/database.yml  
>  default: &default  
>    adapter: mysql2  
>    encoding: utf8mb4  
>    pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>  
>    socket: /var/lib/mysql/mysql.sock  
>    username: "admin"  
>    password: "!QAZxsw2"  
>    host: raisetech5.cjcyo6gekjgm.ap-northeast-1.rds.amazonaws.com  
  
[ec2-user@ip-10-0-16-114 raisetech-live8-sample-app]$ bin/dev  
>  14:34:34 web.1  | started with pid 3580  
>  14:34:34 js.1   | started with pid 3581  
>  14:34:35 js.1   | yarn run v1.22.19  
>  14:34:35 js.1   | $ webpack --config ./config/webpack/webpack.config.js --watch  
>  14:34:36 web.1  | => Booting Puma  
>  14:34:36 web.1  | => Rails 7.1.3.2 application starting in development  
>  14:34:36 web.1  | => Run `bin/rails server --help` for more startup options  
>  14:34:36 web.1  | Puma starting in single mode...  
>  14:34:36 web.1  | * Puma version: 6.4.2 (ruby 3.2.3-p157) ("The Eagle of Durango")  
>  14:34:36 web.1  | *  Min threads: 5  
>  14:34:36 web.1  | *  Max threads: 5  
>  14:34:36 web.1  | *  Environment: development  
>  14:34:36 web.1  | *          PID: 3580  
>  14:34:36 web.1  | * Listening on http://0.0.0.0:3000  
>  14:34:36 web.1  | Use Ctrl-C to stop  
>  14:34:44 js.1   | asset application.css 144 KiB [compared for emit] (name: application)  
>  14:34:44 js.1   | asset application.js 82.5 KiB [compared for emit] [minimized] (name: application)  
>  14:34:44 js.1   | Entrypoint application 227 KiB = application.css 144 KiB application.js 82.5 KiB  
>  14:34:44 js.1   | orphan modules 307 KiB (javascript) 1.01 KiB (runtime) [orphan] 34 modules  
>  14:34:44 js.1   | runtime modules 695 bytes 3 modules  
>  14:34:44 js.1   | cacheable modules 156 KiB (javascript) 144 KiB (css/mini-extract)  
>  14:34:44 js.1   |   modules by path ./app/javascript/stylesheets/*.scss 50 bytes (javascript) 144 KiB (css/mini-extract)  
>  14:34:44 js.1   |     ./app/javascript/stylesheets/application.scss 50 bytes [built] [code generated]  
>  14:34:44 js.1   |     css ./node_modules/css-loader/dist/cjs.js!./node_modules/sass-loader/dist/cjs.js!./app/javascript/stylesheets/application.scss 144 KiB [built] [code generated]  
>  14:34:44 js.1   |   ./app/javascript/application.js + 6 modules 137 KiB [built] [code generated]  
>  14:34:44 js.1   |   ./node_modules/@hotwired/turbo-rails/node_modules/@rails/actioncable/src/index.js + 9 modules 19.1 KiB [built] [code generated]  
>  14:34:44 js.1   |  
>  14:34:44 js.1   | WARNING in ./app/javascript/stylesheets/application.scss (./app/javascript/stylesheets/application.scss.webpack[javascript/auto]!=!./node_modules/css-loader/dist/cjs.js!./node_modules/sass-loader/dist/cjs.js!./app/javascript/stylesheets/application.scss)  
>  14:34:44 js.1   | Module Warning (from ./node_modules/sass-loader/dist/cjs.js):  
>  14:34:44 js.1   | Deprecation Using / for division outside of calc() is deprecated and will be removed in Dart Sass 2.0.0.  
>  14:34:44 js.1   |  
>  14:34:44 js.1   | Recommendation: math.div($custom-control-indicator-size, 2) or calc($custom-control-indicator-size / 2)  
>  14:34:44 js.1   |  
>  14:34:44 js.1   | More info and automated migrator: https://sass-lang.com/d/slash-div  
>  14:34:44 js.1   |  
>  14:34:44 js.1   | node_modules/bootstrap/scss/_variables.scss 568:49  @import  
>  14:34:44 js.1   | node_modules/bootstrap/scss/bootstrap.scss 9:9      @import  
>  14:34:44 js.1   | app/javascript/stylesheets/application.scss 1:9     root stylesheet  
>  14:34:44 js.1   |  @ ./app/javascript/stylesheets/application.scss  
>  14:34:44 js.1   |  
>  14:34:44 js.1   | WARNING in ./app/javascript/stylesheets/application.scss (./app/javascript/stylesheets/application.scss.webpack[javascript/auto]!=!./node_modules/css-loader/dist/cjs.js!./node_modules/sass-loader/dist/cjs.js!./app/javascript/stylesheets/application.scss)  
>  14:34:44 js.1   | Module Warning (from ./node_modules/sass-loader/dist/cjs.js):  
>  14:34:44 js.1   | Deprecation Using / for division outside of calc() is deprecated and will be removed in Dart Sass 2.0.0.  
>  14:34:44 js.1   |  
>  14:34:44 js.1   | Recommendation: math.div($input-padding-y, 2) or calc($input-padding-y / 2)  
>  14:34:44 js.1   |  
>  14:34:44 js.1   | More info and automated migrator: https://sass-lang.com/d/slash-div  
>  14:34:44 js.1   |  
>  14:34:44 js.1   | node_modules/bootstrap/scss/_variables.scss 498:73  @import  
>  14:34:44 js.1   | node_modules/bootstrap/scss/bootstrap.scss 9:9      @import  
>  14:34:44 js.1   | app/javascript/stylesheets/application.scss 1:9     root stylesheet  
>  14:34:44 js.1   |  @ ./app/javascript/stylesheets/application.scss  
>  14:34:44 js.1   |  
>  14:34:44 js.1   | WARNING in ./app/javascript/stylesheets/application.scss (./app/javascript/stylesheets/application.scss.webpack[javascript/auto]!=!./node_modules/css-loader/dist/cjs.js!./node_modules/sass-loader/dist/cjs.js!./app/javascript/stylesheets/application.scss)  
>  14:34:44 js.1   | Module Warning (from ./node_modules/sass-loader/dist/cjs.js):  
>  14:34:44 js.1   | Deprecation Using / for division outside of calc() is deprecated and will be removed in Dart Sass 2.0.0.  
>  14:34:44 js.1   |  
>  14:34:44 js.1   | Recommendation: math.div($spacer, 2) or calc($spacer / 2)  
>  14:34:44 js.1   |  
>  14:34:44 js.1   | More info and automated migrator: https://sass-lang.com/d/slash-div  
>  14:34:44 js.1   |  
>  14:34:44 js.1   | node_modules/bootstrap/scss/_variables.scss 302:31  @import  
>  14:34:44 js.1   | node_modules/bootstrap/scss/bootstrap.scss 9:9      @import  
>  14:34:44 js.1   | app/javascript/stylesheets/application.scss 1:9     root stylesheet  
>  14:34:44 js.1   |  @ ./app/javascript/stylesheets/application.scss  
>  14:34:44 js.1   |  
>  14:34:44 js.1   | WARNING in ./app/javascript/stylesheets/application.scss (./app/javascript/stylesheets/application.scss.webpack[javascript/auto]!=!./node_modules/css-loader/dist/cjs.js!./node_modules/sass-loader/dist/cjs.js!./app/javascript/stylesheets/application.scss)  
>  14:34:44 js.1   | Module Warning (from ./node_modules/sass-loader/dist/cjs.js):  
>  14:34:44 js.1   | Deprecation Using / for division outside of calc() is deprecated and will be removed in Dart Sass 2.0.0.  
>  14:34:44 js.1   |  
>  14:34:44 js.1   | Recommendation: math.div($spacer, 2) or calc($spacer / 2)  
>  14:34:44 js.1   |  
>  14:34:44 js.1   | More info and automated migrator: https://sass-lang.com/d/slash-div  
>  14:34:44 js.1   |  
>  14:34:44 js.1   | node_modules/bootstrap/scss/_variables.scss 713:37  @import  
>  14:34:44 js.1   | node_modules/bootstrap/scss/bootstrap.scss 9:9      @import  
>  14:34:44 js.1   | app/javascript/stylesheets/application.scss 1:9     root stylesheet  
>  14:34:44 js.1   |  @ ./app/javascript/stylesheets/application.scss  
>  14:34:44 js.1   |  
>  14:34:44 js.1   | WARNING in ./app/javascript/stylesheets/application.scss (./app/javascript/stylesheets/application.scss.webpack[javascript/auto]!=!./node_modules/css-loader/dist/cjs.js!./node_modules/sass-loader/dist/cjs.js!./app/javascript/stylesheets/application.scss)  
>  14:34:44 js.1   | Module Warning (from ./node_modules/sass-loader/dist/cjs.js):  
>  14:34:44 js.1   | Deprecation Using / for division outside of calc() is deprecated and will be removed in Dart Sass 2.0.0.  
>  14:34:44 js.1   |  
>  14:34:44 js.1   | Recommendation: math.div($spacer, 2) or calc($spacer / 2)  
>  14:34:44 js.1   |  
>  14:34:44 js.1   | More info and automated migrator: https://sass-lang.com/d/slash-div  
>  14:34:44 js.1   |  
>  14:34:44 js.1   | node_modules/bootstrap/scss/_variables.scss 718:37  @import  
>  14:34:44 js.1   | node_modules/bootstrap/scss/bootstrap.scss 9:9      @import  
>  14:34:44 js.1   | app/javascript/stylesheets/application.scss 1:9     root stylesheet  
>  14:34:44 js.1   |  @ ./app/javascript/stylesheets/application.scss  
>  14:34:44 js.1   |  
>  14:34:44 js.1   | WARNING in ./app/javascript/stylesheets/application.scss (./app/javascript/stylesheets/application.scss.webpack[javascript/auto]!=!./node_modules/css-loader/dist/cjs.js!./node_modules/sass-loader/dist/cjs.js!./app/javascript/stylesheets/application.scss)  
>  14:34:44 js.1   | Module Warning (from ./node_modules/sass-loader/dist/cjs.js):  
>  14:34:44 js.1   | 64 repetitive deprecation warnings omitted.  
>  14:34:44 js.1   |  
>  14:34:44 js.1   | null  
>  14:34:44 js.1   |  @ ./app/javascript/stylesheets/application.scss  
>  14:34:44 js.1   |  
>  14:34:44 js.1   | WARNING in configuration  
>  14:34:44 js.1   | The value 'hashed' for option 'optimization.moduleIds' is deprecated. Use 'deterministic' instead.  
>  14:34:44 js.1   |  
>  14:34:44 js.1   | 6 warnings have detailed information that is not shown.  
>  14:34:44 js.1   | Use 'stats.errorDetails: true' resp. '--stats-error-details' to show it.  
>  14:34:44 js.1   |  
>  14:34:44 js.1   | webpack 5.76.0 compiled with 7 warnings in 7644 ms  
>  14:37:11 web.1  | Started GET "/" for 112.70.9.133 at 2024-05-05 >  14:37:11 +0000  
>  14:37:11 web.1  | Cannot render console from 112.70.9.133! Allowed networks: 127.0.0.0/127.255.255.255, ::1  
>  14:37:11 web.1  |   ActiveRecord::SchemaMigration Load (3.8ms)  SELECT `schema_migrations`.`version` FROM `schema_migrations` ORDER BY `schema_migrations`.`version` ASC  
>  14:37:11 web.1  | Processing by FruitsController#index as HTML  
>  14:37:11 web.1  |   Rendering layout layouts/application.html.slim  
>  14:37:11 web.1  |   Rendering fruits/index.html.slim within layouts/application  
>  14:37:11 web.1  |   Fruit Load (3.7ms)  SELECT `fruits`.* FROM `fruits` ORDER BY `fruits`.`row_order` ASC  
>  14:37:11 web.1  |   ? app/views/fruits/index.html.slim:13  
>  14:37:11 web.1  |   Rendered fruits/index.html.slim within layouts/application (Duration: 20.7ms | Allocations: 17654)  
>  14:37:11 web.1  |   Rendered layouts/_navigation_links.html.erb (Duration: 0.3ms | Allocations: 167)  
>  14:37:11 web.1  |   Rendered layouts/_navigation.html.slim (Duration: 5.1ms | Allocations: 5850)  
>  14:37:11 web.1  |   Rendered layouts/_messages.html.slim (Duration: 3.2ms | Allocations: 3873)  
>  14:37:11 web.1  |   Rendered layout layouts/application.html.slim (Duration: 36.5ms | Allocations: 35346)  
>  14:37:11 web.1  | Completed 200 OK in 110ms (Views: 39.2ms | ActiveRecord: 16.5ms | Allocations: 47948)  
>  14:37:11 web.1  |  
>  14:37:11 web.1  |  
>  14:37:11 web.1  | /usr/local/rvm/gems/ruby-3.2.3/gems/rack-3.0.9.1/lib/rack/file.rb:5: warning: Rack::File is deprecated and will be removed in Rack 3.1  
  
---------------  
![組み込みサーバー（Puma）でのRailsアプリケーション動作確認_1](/組み込みサーバー（Puma）でのRailsアプリケーション動作確認_1.PNG)  
---------------  
  
### 組み込みサーバーとUnix Socketを使ったRailsアプリの動作確認  
  
---------------  
![2_1](/2_1.PNG)  
---------------  

[ec2-user@ip-10-0-16-114 ~]$ curl --unix-socket ///home/ec2-user/raisetech-live8-sample-app/tmp/sockets/puma.sock http://16.183.119.94:3000/  
>  <!DOCTYPE html><html><head><meta content="width=device-width, initial-scale=1.0" name="viewport" /><title>Sortable Table Sandbox</title><meta content="Sortable Table Sandbox" name="description" /><link rel="stylesheet" href="/assets/application-fae796cccb5b5aaf5177cf1d6ca3509489d1f3bf2a19c4d23891f96164eb2624.css" media="all" /><script src="/assets/application-8d908e86837bb7536ce498750f979adb25f4937fe41eff2ad642ce1fe9275add.js" data-turbo-track="reload" defer="defer"></script><meta name="csrf-param" content="authenticity_token" />  
>  <meta name="csrf-token" content="TTD9aDNjIlNoh45in-CSbDzeZetr530K2yv6_HenKYUXNJdaSqN9kQvlAHxcd6ef_2XvrmPN5C1dakG3hLOUbQ" /></head><body><header><nav class="navbar navbar-inverse navbar-fixed-top navbar-dark bg-dark"><div class="container"><div class="navbar-header"><but> ton class="navbar-toggler" data-target=".navbar-collapse" data-toggle="collapse" type="button"><span class="sr-only sr-only-focusable">Toggle navigation</span><span class="icon-bar"></span><span class="icon-bar"></span><span class="icon-bar"></span></button><a class="navbar-brand" href="/">Home</a></div><div class="collapse navbar-collapse"><ul class="nav navbar-nav"></ul></div></div></nav></header><mai> n role="main"><div class="container"><div class="row"><div class="col->  md-12"><h1>Listing fruits</h1><table class="table table-bordered table-sortable"><thead><tr><th>Name</th><th>image</th><th></th><th></th><th></th></tr></thead><tbody></tbody></table><br /><a href="> /fruits/new">New Fruit</a></div></div></div></main><script async nonce="" type="text/javascript" id="mini-profiler" src="/mini-profiler-resources/includes.js?v=35a79b300ab5afa978cb59af0b05e059" data-css-url="/mini-profiler-resources/includes.css?v=35a79b300ab5afa978cb59> af0b05e059" data-version="35a79b300ab5afa978cb59af0b05e059" data-path="/mini-profiler-resources/" data-current-id="p6imdiv5zyxfdm1f38iv" data-ids="p6imdiv5zyxfdm1f38iv,3xjmrtce9tc1tyv8tdpa,gl11cbswoaozhsb3qrw3,8o6x1itvzzlvn7va87s1,fsgmzvvtgs9wji5cf1tn,4lh44tqrgsfp8nn11t> pf,46oh593jjg338x8bukmo,w162dxduf99xz3zwujbh,3wi04qp1aps82iqycee" data-horizontal-position="left" data-vertical-position="top" data-trivial="false" data-children="false" data-max-traces="20" data-controls="false" data-total-sql-count="false" data-authorized="true" data-> toggle-shortcut="alt+p" data-start-hidden="false" data-collapse-results="true" data-html-container="body" data-hidden-custom-fields="" data-turbo-permanent="false"></script>  
>  </body></html>  
[ec2-user@ip-10-0-16-114 ~]$  
  
  
### Nginxの単体起動確認  
[root@ip-10-0-16-114 ~]# systemctl start nginx  
[root@ip-10-0-16-114 ~]# systemctl status nginx  
>  ● nginx.service - The nginx HTTP and reverse proxy server  
>     Loaded: loaded (/usr/lib/systemd/system/nginx.service; disabled; vendor preset: disabled)  
>     Active: active (running) since Fri 2024-05-10 17:21:34 UTC; 5s ago  
>    Process: 4040 ExecStart=/usr/sbin/nginx (code=exited, status=0/SUCCESS)  
>    Process: 4034 ExecStartPre=/usr/sbin/nginx -t (code=exited, status=0/SUCCESS)  
>    Process: 4033 ExecStartPre=/usr/bin/rm -f /run/nginx.pid (code=exited, status=0/SUCCESS)  
>   Main PID: 4042 (nginx)  
>     CGroup: /system.slice/nginx.service  
>             tq4042 nginx: master process /usr/sbin/nginx  
>             mq4043 nginx: worker process  
>    
>  May 10 17:21:34 ip-10-0-16-114.ap-northeast-1.compute.internal systemd[1]: St...  
>  May 10 17:21:34 ip-10-0-16-114.ap-northeast-1.compute.internal nginx[4034]: n...  
>  May 10 17:21:34 ip-10-0-16-114.ap-northeast-1.compute.internal nginx[4034]: n...  
>  May 10 17:21:34 ip-10-0-16-114.ap-northeast-1.compute.internal systemd[1]: St...  
>  Hint: Some lines were ellipsized, use -l to show in full.  
[root@ip-10-0-16-114 ~]#  
  
---------------  
![NGINXの単体起動確認_1](/NGINXの単体起動確認_1.PNG)  
---------------  
  
  
### Nginxと組み込みサーバー、Unix Socketを組み合わせてのRailsアプリケーション動作確認  
[ec2-user@ip-10-0-16-114 raisetech-live8-sample-app]$ bundle exec rails s  
>  => Booting Puma  
>  => Rails 7.1.3.2 application starting in development  
>  => Run `bin/rails server --help` for more startup options  
>  A server is already running (pid: 3625, file: /home/ec2-user/raisetech-live8-sample-app/tmp/pids/server.pid).  
Exiting  
[ec2-user@ip-10-0-16-114 raisetech-live8-sample-app]$  
  
  
### ALB構成  
  
---------------  
![ロードバランサ0604-2_1](/ロードバランサ0604-2_1.PNG)  
---------------  
![ロードバランサ0604-2_2](/ロードバランサ0604-2_2.PNG)  
---------------  
![ロードバランサ0604-2_3](/ロードバランサ0604-2_3.PNG)  
---------------  

### ALB動作確認  
#### index.htmlの内容確認
##### ap-northeast-1c
---------------  
![ロードバランサ0604-3_1](/ロードバランサ0604-3_1.PNG)  
---------------  
##### ap-northeast-1a
---------------  
![ロードバランサ0604-3_2](/ロードバランサ0604-3_2.PNG)  
---------------  
  
####  ロードバランサ DNS名に接続
##### ap-northeast-1cに接続されていることを確認
---------------  
![ロードバランサ0604-1_1](/ロードバランサ0604-1_1.PNG)  
---------------  
  
##### ap-northeast-1aに接続されていることを確認
---------------  
![ロードバランサ0604-1_2](/ロードバランサ0604-1_2.PNG)  
---------------  
  
### S3作成  
  
---------------  
![S3-0604-1_1](/S3-0604-1_1.PNG)  
---------------  
![S3-0604-1_2](/S3-0604-1_2.PNG)  
---------------  
![S3-0604-1_3](/S3-0604-1_3.PNG)  
---------------  
![S3-0604-1_4](/S3-0604-1_4.PNG)  
---------------  
  
### S3接続確認  
#### S3に格納したファイルにアクセスできることを確認  
##### ap-northeast-1c
[ec2-user@ip-10-0-16-114 ~]$ aws s3 cp s3://raisetech5-s3/raitech5.txt /tmp/  
>  download: s3://raisetech5-s3/raitech5.txt to ../../tmp/raitech5.txt  
[ec2-user@ip-10-0-16-114 ~]$ cat ../../tmp/raitech5.txt  
>  TEST[ec2-user@ip-10-0-16-114 ~]$  
[ec2-user@ip-10-0-16-114 ~]$  
  
##### ap-northeast-1a
[ec2-user@ip-10-0-2-71 tmp]$ aws s3 cp s3://raisetech5-s3/raitech5.txt /tmp/  
>  download: s3://raisetech5-s3/raitech5.txt to ./raitech5.txt  
[ec2-user@ip-10-0-2-71 tmp]$  
[ec2-user@ip-10-0-2-71 tmp]$ cat ../../tmp/raitech5.txt  
>  TEST[ec2-user@ip-10-0-2-71 tmp]$  
[ec2-user@ip-10-0-2-71 tmp]$
  
  
### ↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓
### ↓↓ エビデンス追加分
### ↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓
#### ALBを経由してアプリケーション（第3回課題で利用したもの）に接続
##### /etc/nginx/conf.d/にrails-app.confを追加
>  \# cat /etc/nginx/conf.d/rails-app.conf  
>  upstream rails-app {  
>      # UNIXドメインソケット通信の設定  
>      server 127.0.0.1:3000;  
>  }  
>    
>  server {  
>      # 80番ポート(HTTP)を許可  
>      listen 80;  
>    
>      # ホスト名  
>      server_name localhost;  
>    
>      # 静的ファイル（画像など）のパスをドキュメントルートに設定  
>      root /home/ec2-user/raisetech-live8-sample-app/public;  
>    
>      location / {  
>        # ドキュメントルート配下を以下の順で検索  
>        # URIのパスに対するファイル（静的コンテンツ）が存在すれば、そのファイル返 す。  
>        # 存在しなければ、動的コンテンツとして@rails-appに内部リダイレクト。  
>        try_files $uri @rails-app;  
>      }  
>    
>      # nginxのリバースプロキシ設定  
>      # 上記の@rails-appが呼び出された場合のみ以下の設定が読み込まれる  
>      location @rails-app {  
>          # サーバの指示通りにリダイレクト  
>          proxy_redirect off;  
>    
>          # proxy_set_headerを利用することでサーバーに情報を転送できる  
>          proxy_set_header Host $http_host; # ホスト名  
>          proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for; # 送信元の 経路情報  
>          proxy_set_header X-Real-IP $remote_addr; #送信元のIPアドレス  
>    
>          # upstreamの名前を記述  
>          proxy_pass http://rails-app;  
>      }  
>  }  
>  \#  
##### nginx再起動  
>  su -  
>  systemctl restart nginx  
##### Blocked hostエラー回避  
>  su - ec2-user  
>  vi /home/ec2-user/raisetech-live8-sample-app/config/environments  
>  以下を追記  
>  Rails.application.configure do  
>    config.hosts << "raisetech5-lb-1842311282.ap-northeast-1.elb.amazonaws.com"  
>  end  
##### アプリケーション（第3回課題で利用したもの）を起動  
>  cd  /home/ec2-user/raisetech-live8-sample-app  
>  bin/dev  
####  ALBを経由してアプリケーション（第3回課題で利用したもの）に接続確認  
---------------    
![ロードバランサ0608-1_2](/ロードバランサ0608-1_2.PNG)  
---------------    
![ロードバランサ0608-1_1](/ロードバランサ0608-1_1.PNG)  
---------------    

