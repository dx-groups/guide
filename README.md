# Team Guidelines

Guidelines For Front-End Developers.

团队指引，包括学习指南、规范文档等。

## Getting started

Install dependencies:

``` bash
$ git clone https://github.com/elephant-fe/guide
$ cd guide
$ npm install
```

Generate:

``` bash
$ hexo g
```

Run server:

``` bash
$ hexo s --watch
```

## 添加文件

1. `source/docs` 目录下添加相应 markdown 文件
2. `source/_data/sidebar.yml` 文件中关联文件 
3. `themes/navy/languages/zh-cn.yml` 文件中添加文章名


## Deployment

1. Generate and optimize assets

  ```bash
  gulp
  ```

2. Deploy to the gh-pages branch

  ```bash
  hexo d -g
  ```

## License

[CC BY 4.0](http://creativecommons.org/licenses/by/4.0/)
