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
<iframe src="http://10.100.246.27:91/#/demo/spin" style="width: 100%; height: 80px;"></iframe>
{% endraw %}

### 内容式

当内容还在加载中时，可以用类似内容的方式展示一个占位，数据加载后过渡更为自然

{% raw %}
<iframe src="http://10.100.246.27:91/#/demo/card" style="width: 100%; height: 180px;"></iframe>
{% endraw %}

如果是数据块的场景，尽量使用内容式的 loading
