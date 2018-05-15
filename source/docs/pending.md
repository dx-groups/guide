title: 待办
---

此处维护当前团队的 issues，可自行认领，但必须有产出，以周为单位对外输出，输出方式有：**文章** + **代码（产品）**，对于阶段性的成果，适时在团队内部进行布道分享。


## 基础框架

- Arthur 框架 - 徐宝石

- cli 工具

- 构建工具

  - postcss 插件，postcss-plugin-px2rem 添加 dpx，rpx 单位支持 - 孙小海

    `dpx` (dpr px) 这个单位, 按照 dpr 来放大 1*px, 2*px, 3*px 大小的字体，再按照屏幕dpr缩小, 这样就达到了字体不缩放, 各种屏幕的字体看起来都差不多,也与屏幕宽度无关。

    `rpx` (real px), 来表示物理像素

    ```css
    css
      .cls {
            width: 75px;
            font-size: 12dpx
            border: 1rpx
      }

    ===> 转换为

    css
      .cls {
          width: 2rem;
          border: 1px;
      }
      [data-dpr="1"] .cls { font-size: 12px }
      [data-dpr="2"] .cls { font-size: 24px }
      [data-dpr="3"] .cls { font-size: 36px }
    ```

- workspace 参考 Iceworks

## 解决方案

- PWA, service worker, app shell, LAVAS - 王玉龙

- 菜单的优化，现有的菜单配置方式过于固化，是否有更为灵活的方案？

- 测试方案

- 浏览器路由，vue-router 替换

- 移动端适配方案
