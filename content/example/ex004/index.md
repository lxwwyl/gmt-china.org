---
title: 中国省会城市分布图
date: 2016-10-24
tags:
    - 地学数据
authors:
    - 忆尤
images:
    - CN-capitals.png
---

{{% notice info %}}
数据下载：[CN-border-La.dat](/datas/CN-border-La.dat) [CN-capitals.dat](/datas/CN-capitals.dat)
{{% /notice %}}

本文整理并绘制了中国省会城市的分布图，同时展示了如何巧妙地利用 `pstext` 模块的功能来灵活地放置城市名的位置。

绘图脚本如下：
{{< include-code "/example/ex004/CN-capitals.sh" bash >}}

`pstext` 的 `-F` 选项参数为 `-F+f7p,35+j` ，即使用大小为 7p 的 35 号字体写城市名。由于使用了 `+j` 选项，因而输入文件需要有四列，分别是经度、纬度、文本对齐方式以及城市名，具体内容如下（此处为了节省空间，只显示了个别几个城市的数据）：

    # 经度    纬度   对齐方式  城市名
    121.48   31.22    ML    上海
    ...
    112.53   37.87    TC    太原
    ...
    101.74   36.56    MR    西宁
    ...
    117.27   31.86    CB    合肥

`pstext` 默认会将城市名放在城市所在处，因而要使用 `-D<dx>/<dy>` 选项将城市名沿着X和Y方向分别移动 `<dx>` 和 `<dy>`。上面的示例中使用了 `-Dj0.15c/0.15c`，关键在于其中 `j` 的使用，其使得文本会沿着文本对齐方式所定义的方向移动。比如：

1. “上海”的对齐方式是 `ML`（即 **M**iddle **L**eft），`-Dj0.15c/0.15c` 使得“上海”向右移动了 0.15 厘米
2. “西宁”的对齐方式是 `MR`（即 **M**iddle **R**ight），`-Dj0.15c/0.15c` 使得“太原”向左移动了 0.15 厘米
3. “太原”的对齐方式是 `TC`（即 **T**op **C**enter），`-Dj0.15c/0.15c` 使得“太原”向下移动了 0.15 厘米
4. “合肥”的对齐方式是 `BC`（即 **B**ottom **C**enter），`-Dj0.15c/0.15c` 使得“西宁”向上移动了 0.15 厘米

你也可以尝试以下其他对齐方式下 `-Dj` 的具体效果。

最终绘图效果如下图：

{{< figure src="/example/ex004/CN-capitals.png" title="中国省会城市分布图" >}}
