title: 环境搭建
---

快速完成开发、生产的环境搭建，包含 node、mongodb、nginx 等。

## nvm

```bash
$ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.2/install.sh | bash
$ source ~/.bashrc
```

## nodejs

```bash
$ nvm install 7.9.0

# 配置淘宝源
$ npm config set registry https://registry.npm.taobao.org
$ yarn config set registry https://registry.npm.taobao.org
```

## mongodb

详细请参考官网 [install-mongodb-on-red-hat](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-red-hat/)

### Linux

```bash
# 配置 Repo
$ vi /etc/yum.repos.d/mongodb-org-3.6.repo

# repo 内容 -- Start
[mongodb-org-3.6]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.6/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.6.asc
# repo 内容 -- End

# 安装
$ yum install -y mongodb-org

# 启动|关闭|重启
$ service mongod start|stop|restart

# 开机启动
$ chkconfig mongod on

# 连接
$ mongo --host <host>:27017 -u <user> -p <password> <dbname>
```

### Mac

```bash
# 安装
$ brew update
$ brew install mongodb

# 启动
$ mongod

# 连接
$ mongo --host <host>:27017 -u <user> -p <password> <dbname>
```

### 常用命令

```bash
> use <dbname>
> db.createUser({ user: '<username>', pwd: '<password>', roles: [{ role: 'readWrite', db: '<dbname>' }] })
> db.auth('<username>', '<password>')


> help
> db.help()
> show dbs
> show collections
> db.<collectionname>.find()
> db.<collectionname>.remove({})
```

### 备份与恢复

```bash
# 备份
$ mongodump -h <host> -d <dbname> -o <dbdirectory>

# 恢复
$ mongorestore -h <host> -d <dbname> --dir <dbdirectory>
```


## nginx

### Linux

```bash
# 安装
$ yum install nginx

# 启动|关闭|重启
$ service nginx start|stop|restart
```

### Mac

```bash
# 安装
$ brew update
$ brew install nginx

# 启动
$ sudo nginx

# 重新加载配置|重启|停止|退出
$ sudo nginx -s reload|reopen|stop|quit

# 测试配置是否有语法错误
$ sudo nginx -t

# 配置
/usr/local/etc/nginx/nginx.conf
```

### SPA 路由

现在 Web 项目基本上都是单页面应用（SPA），其路由是内部控制，需要在 nginx 做特殊配置支持。

```bash
location / {
  index  index.html index.htm;
  try_files $uri $uri/ /index.html;
}
```

### gzip

默认情况下，nginx 的 gzip 压缩是关闭的。

```shell
## Compression
gzip                on;
gzip_min_length     1024;
gzip_buffers        4 8k;
gzip_comp_level     3;
gzip_http_version   1.0;
gzip_disable        "msie6";
gzip_types          text/plain text/css application/json application/javascript application/x-javascript text/xml application/xml application/xml+rss text/javascript image/x-icon image/jpeg image/bmp image/png image/gif;
gzip_vary           on;
```

具体说明：

- gzip_min_length

  最小压缩的页面，如果页面过于小，可能会越压越大，这里规定大于1K的页面才启用压缩。

- gzip_buffers

  设置系统获取几个单位的缓存用于存储gzip的压缩结果数据流。

- gzip_comp_level

  压缩级别，1压缩比最小处理速度最快，9压缩比最大但处理最慢，同时也最消耗CPU，一般设置为3就可以了。

- gzip_types

  什么类型的页面或文档启用压缩。

### 使用 proxy_pass 反向代理时，cookie 丢失的问题

1. 如果只是host、端口转换，则cookie不会丢失。例如：

```shell
location /project {
  proxy_pass   http://127.0.0.1:8080/project;
}  
```

通过浏览器访问http://127.0.0.1/project时，浏览器的cookie内有jsessionid。再次访问时，浏览器会发送当前的cookie。

2. 如果路径也变化了，则需要设置cookie的路径转换，nginx.conf的配置如下
    location /proxy_path {
        proxy_pass   http://127.0.0.1:8080/project;
    }

通过浏览器访问http://127.0.0.1/proxy_path时，浏览器的cookie内没有jsessionid。再次访问时，后台当然无法获取到cookie了。
详细看了文档：http://nginx.org/en/docs/http/ngx_http_proxy_module.html?&_ga=1.161910972.1696054694.1422417685#proxy_cookie_path

加上路径转换：`proxy_cookie_path  /project /proxy_path`;

则可以将project的cookie输出到proxy_path上。正确的配置是：

```shell
location /proxy_path {
  proxy_pass   http://127.0.0.1:8080/project;
  proxy_cookie_path  /project /proxy_path;
}
```