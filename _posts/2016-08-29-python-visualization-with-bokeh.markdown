---
layout:	    post
title:      "[译|转]Python: 利用 Bokeh 进行可视化"
subtitle:   "Bokeh 的极简教程"
date:       2016-08-29
author:     "kissg"
header-img: "img/2016-08-29-python-visualization-with-bokeh/covery.jpg"
comments:    true
tags:
    - 菜鸟成长日记
    - python
    - 译
    - 转
---

> 原文作者: Mike Driscoll\\
原文连接: [Python: Visualization with Bokeh](http://www.blog.pythonlibrary.org/2016/07/27/python-visualization-with-bokeh/)\\
译者：kissg(赵喧典)\\
本文最先发表于微信公众号"编程派"，是本人在 PythonTG 翻译组的译文，相当于自我转载。编程派地址，如需转载，请联系微信公众号"编程派"获得授权。转载时注明来源，作者及原文链接。

[Bokeh 包](http://bokeh.pydata.org/en/latest/)是一个交互式的可视化库。其利用 web 浏览器进行展示，目标是以 D3.js 的风格绘制图案，这样图会看起来很优美，而且很容易构造。Bokeh 支持大量的流式的数据集。你可以用这个库创建各种图表/图形。它的一个主要竞争对手可能要属 [Plotly](https://plot.ly/) 了。

> 译注：D3.js 是一个可用于创建“数据驱动文档”（Data Driven Documents） JavaScript 库。[详情看这里](https://d3js.org/)

*注意：这不是一篇关于 Bokeh 库的深度教程，因为它所能绘制的不同图表和可视化图形实在太多了。因此，本文的目的是带读者领略一下 Bokeh 库的丰姿，看看它能做哪些有趣的事情。*

让我们花一点时间安装 Bokeh。最简单的方式是使用 pip 或 conda，比如使用 pip：

```shell
pip install bokeh
```

这条命令会安装 Bokeh 以及它所有的依赖包。因为这个原因，你可能想要在一个虚拟环境下安装 Bokeh，但这完全取决于你。现在，让我们通过一个简单的例子，检查是否安装成功。将下面的代码保存到文件，文件名按你喜欢的来就好。

```python
from bokeh.plotting import figure, output_file, show

output_file("/path/to/test.html")

x = range(1, 6)
y = [10, 5, 7, 1, 6]
plot = figure(title='Line example', x_axis_label='x', y_axis_label='y')
plot.line(x, y, legend='Test', line_width=4)
show(plot)
```

这里，我们仅仅从 Bokeh 库导入了一些条目，也仅仅说明了将输出保存到哪里。你会注意到，输出是 HTML 文档 。然后我们为 x 轴和 y 轴生成了一些值，用于创建图表。再然后，我们创建了一个 figure 对象，设置了标题和两个坐标轴的标签。最后，我们画出这条折线，给出了图例，设置了线宽，并显示。命令 show 会自动打开你的默认浏览器，并在其中显示图表。最终你看到的将是这样的：

![Line example](/img/2016-08-29-python-visualization-with-bokeh/bokeh_line.png)

Bokeh 还支持 Jupyter Notebook，唯一需要修改的就是用 **output_notebook** 代替 **output_file**。

> 译注：output_notebook()，不再需要参数。

Bokeh 的[快速入门指南](http://bokeh.pydata.org/en/latest/docs/user_guide/quickstart.html#userguide-quickstart)已经提供了一个在网格线上绘制一系列正弦波的简明例子。我稍微削减了代码，只留下一个正弦波。注意了，要让下面的例子能正常执行，你需要先安装好 NumPy。

```python
import numpy as np

from bokeh.layouts import gridplot
from bokeh.plotting import figure, output_file, show

N = 100
x = np.linspace(0, 4*np.pi, N)
y0 = np.sin(x)

output_file('sinewave.html')

sine = figure(width=500, plot_height=500, title='Sine')
sine.circle(x, y0, size=10, color="navy", alpha=0.5)

p = gridplot([[sine]], toolbar_location=None)

show(p)
```

这个例子与前一个的主要不同是，我们用 NumPy 来生成数据点，以及我们将图形放在了**网格线**内部，而不是画出图形本身。当你运行这段代码，最终看到的图表应该是这样的：

![Sine](/img/2016-08-29-python-visualization-with-bokeh/bokeh_sine_wave.png)

如果你不喜欢圆形，Bokeh 还支持其他的形状，总有你喜欢的，比如正方形，三角形，以及其他多种图形。

## 小结

Bokeh 项目确实很有趣，它提供了简单易用的 API，用于创建图案、图表和其他数据可视化形式。Bokeh 的文档梳理得相当好，它包含了大量的例子，以展示你都能用它做什么。你值得浏览一遍它的文档，这样你会见识到，其他的一些图表是长什么样的，以及生成如此美丽结果的代码是多么简短。

我唯一抱怨的一点是，Bokeh 并没有提供一种通过编程就能保存图片的方法。两年来，这一直是他们致力于修改的 [bug](https://github.com/bokeh/bokeh/issues/538)。好消息是，他们找到了一种方式，也许不久就会支持这一功能。除此之外，我觉得它简直酷毙了。

> 译注, 结语: 我承认这篇译文确实很水, 但原文就是这样的. 当时在学习数据可视化, 就认领了这篇有关 Bokeh 的, 没注意这么水...
