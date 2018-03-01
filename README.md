# Team Guidelines

Guidelines For Front-End Developers.

团队指引，包括学习指南、规范文档等。

## Getting started

Install dependencies:

``` bash
$ git clone https://github.com/elephant-fe/guide
$ cd guide
$ npm install
$ npm start
```

## 添加文件

1. `source/docs` 目录下添加相应 markdown 文件
2. `source/_data/sidebar.yml` 文件中关联文件 
3. `themes/navy/languages/zh-cn.yml` 文件中添加文章名


## Deployment

Generate and upload assets

  ```bash
  npm run deploy
  ```

注意： 部署时直接将文件上传到服务器，需要输入服务器密码。

## License

[CC BY 4.0](http://creativecommons.org/licenses/by/4.0/)
