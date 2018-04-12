title: 交互规范 
---

## 原则

根据费茨法则（Fitts's Law）所描述的，如果用户鼠标移动距离越少、对象相对目标越大，那么用户越容易操作。通过运用上下文工具（即：放在内容中的操作工具），使内容和操作融合，从而简化交互。

能在这个页面解决的问题，就不要去其它页面解决，因为任何页面刷新和跳转都会引起变化盲视（Change Blindness），导致用户心流（Flow）被打断。频繁的页面刷新和跳转，就像在看戏时，演员说完一行台词就安排一次谢幕一样。


## 字体

```javascript
font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
             "Helvetica Neue", Helvetica, "PingFang SC", "Hiragino Sans GB", "Microsoft YaHei",
             SimSun, sans-serif;
```


## 字阶与行高

字阶和行高决定着一套字体系统的动态与秩序之美。字阶是指一系列有规律的不同尺寸的字体。行高可以理解为一个包裹在字体外面的无形的盒子。

![font](./font.png)

## Loading 动画

### 覆盖式

这种 loading 方式适用各种场景，近乎可以作为加载的 “银弹”

{% raw %}
<iframe src="https://elephant-fe.github.io/examples/#/demo/spin" style="width: 100%; height: 80px;"></iframe>
{% endraw %}

### 内容式

当内容还在加载中时，可以用类似内容的方式展示一个占位，数据加载后过渡更为自然

{% raw %}
<iframe src="https://elephant-fe.github.io/examples/#/demo/card" style="width: 100%; height: 180px;"></iframe>
{% endraw %}

如果是数据块的场景，尽量使用内容式的 loading


## 分页

分页组件统一如下：

- 显示数据总量
- 指定每页可以显示多少条
- 快速跳转至某页

![page](./page.png)

参考 javascript 代码如下

```javascript
const pagination = {
  // total: parseInt(page.totalCount),
  // pageSize: this.state.pageSize,
  showSizeChanger: true,
  showQuickJumper: true,
  showTotal: total => `共 ${total} 项`,
  pageSizeOptions: ['5', '10', '20', '50'],
}
```

## 选择框

- 状态类这种确定的字典项，不可输可选
- 数据类的下拉框，需要和后台交互的，可输可选

## 表格

表格尽量不设置列宽和行高，利用 table 的自适应布局，一般都能获得不错的效果。

## 最小权限

对于操作类页面，遵循最小权限原则，有以下场景：

- 列表页，选择行的情况，只有当按钮对应功能可用时，按钮才可点击，其他情况均 disable
- 表单页，提交后及时将功能按钮置灰，避免重复提交
- 若有些功能按钮无法及时 disable，要用 throttle 或 debounce 进行限流