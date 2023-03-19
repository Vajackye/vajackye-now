## matplotlib
* 可绘制散点图，折线图，曲线图，直方图，饼图

```python
  #导入绘图模块
  import matplotlib.pyplot as plt
  
  #生成在[a,b]内随机数
  '''
  import random
  random.uniform(x, y)
  '''
```
### 图表绘制

```python

import matplotlib.pyplot as plt
import random
from pylab import mpl
mpl.rcParams["font.sans-serif"] = ["SimHei"]#设置显示中文字体
mpl.rcParams["axes.unicode_minus"] = False#设置显示正常符号

x = range(70)

y_shanghai = [random.uniform(15,18) for i in x]#随机数 15-18范围内

y_beijing = [random.uniform(0,3) for i in x]
#plt.plot(x, y_shanghai)#绘图
plt.figure(figsize=(20,8), dpi = 80)
#绘制多个折线于一个图，默认颜色和直线，可手动修改
plt.plot(x, y_shanghai,label = '上海')#标签表明哪条线
plt.plot(x, y_beijing,color = 'g', linestyle = '-.',label = '北京')#线段风格自己查。

x_ticks_label = ["11点{}分".format(i) for i in x]#所有时刻

y_ticks = range(40)

#plt.xticks(x_ticks_label[::5])不可直接使用，因为是字符串（见上x_ticks_label变量），要先转成整数
plt.xticks(x[::5], x_ticks_label[::5])#x轴刻度，内部是刻度范围，5为一个范围，后面的是在原所有时刻以5一个分度显示

plt.yticks(y_ticks[::5])#同理

plt.grid(True, linestyle='--', alpha = 0.5)#grid：网格， alpha：透明度

plt.xlabel("time")#标签
plt.ylabel("temperature")
plt.title("温度变化图", fontsize = 15)#标题

plt.legend(loc = 'best')#给折线的标签放在一起，图例表明哪条线是什么地方的，loc表示当地（本图把？），best表示在画布中最好位置（自动选择）
#图像保存，一定要放在show（）前面，因为show会释放figure资源，最后保存则只保存空图片
#plt.savefig("./test.png")#文件名为test.png

plt.show()

```
```python
import matplotlib.pyplot as plt
import random
from pylab import mpl
#mpl.rcParams["font.sans-serif"] = ["SimHei"]
#mpl.rcParams["axes.unicode_minus"] = False

x = range(60)
y_beijing = [random.uniform(15, 18) for i in x]#应该是列表[]而不是（）
y_shanghai = [random.uniform(2,3) for i in x]
#船舰画布，多画布
fig, axes = plt.subplots(nrows = 1, ncols = 2, figsize = (20, 8), dpi = 200)

#plot画布
axes[0].plot(x, y_shanghai,label = '上海')#标签表明哪条线
axes[1].plot(x, y_beijing,color = 'g', linestyle = '-.',label = '北京')#线段风格自己查。

#刻度
x_ticks_label = ['11点{}分'.format(i) for i in x]
y_ticks = range(60)

#刻度显示
axes[0].set_xticks(x[::5])
axes[0].set_yticks(y_ticks[::5])
axes[0].set_xticklabels(x_ticks_label[::5])
axes[1].set_xticks(x[::5])
axes[1].set_yticks(y_ticks[::5])
axes[1].set_xticklabels(x_ticks_label[::5])

#添加网格
axes[0].grid(True, linestyle = '--', alpha = 1)
axes[1].grid(True, linestyle = '-.', alpha = 1)

#标签
axes[0].set_xlabel("time")
axes[0].set_ylabel("temperature")
axes[0].set_title('noon')
axes[1].set_xlabel("time")
axes[1].set_ylabel("temperature")
axes[1].set_title('noon')

#图例
axes[0].legend(loc = 0)
axes[1].legend(loc = 0)

plt.show()
```
