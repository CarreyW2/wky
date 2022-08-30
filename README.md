# matplotlib基础

[toc]


要画一副图最基础的几个要素：导入模块；x，y轴数据；画什么图；显示图

```python
from matplotlib import pyplot as plt  # 导入pyplot

x = range(2, 26, 2)
y = [15,13,14.5,17,20,25,26,24,23,22,18,15]

plt.plot(x,y)  # 绘制折线图
plt.show()  #展示图形
```

---

还可以做：

1. 设置**图片大小**（想要一个高清无码大图）
2. **保存到本地**
3. **描述信息**，比如x、y轴标签，图主题
4. 调整x、y轴**刻度间距**
5. **线条样式**（颜色、透明度等）
6. **标记特殊点**
7. 添加**水印**

---

## 一、基础设置

### 1. 大部分函数中通用属性 

```python
# 颜色
color='red'
# 形状
linestyle='-'
# 宽度
linewidth=5
# 字体大小
fontsize=12
# 透明度
alpha=0.3
```

---

### 2. 颜色和形状

| 颜色 | 字符     |      | 形状   | 字符 |
| ---- | -------- | ---- | ------ | ---- |
| 红色 | red; r   |      | 点     | .    |
| 蓝色 | blue;b   |      | 像素点 | ,    |
| 绿色 | green;g  |      | 圆形   | o    |
| 黑色 | black;k  |      | 实线   | -    |
| 白色 | white;w  |      | 虚线   | --   |
| 黄色 | yellow;y |      | 点划线 | -.   |
| 灰色 | gray     |      | 点虚线 | :    |
| 紫色 | purple   |      | 正方形 | s    |
| 粉色 | pink     |      | 星型   | *    |

#### 2.1 基础颜色表

![基础颜色表](https://img-blog.csdnimg.cn/b7e60478cad7465ea5b121df5a43eaf5.png)

#### 2.2 渐变色表

![渐变色表](https://img-blog.csdnimg.cn/78ba18f5ddee40399a9f6df46d9a0db5.png#pic_center#)

#### 2.3 形状表

![形状表](https://img-blog.csdnimg.cn/20191017095713664.png?…1RoZV9UaW1lX1J1bm5lcg==,size_16,color_FFFFFF,t_70)

---

### 3. 显示中文字体和负号

```python
# 方式一
plt.rcParams['font.sans-serif'] = ["SimHei"]  # 黑体显示中文
plt.rcParams['axes.unicode_minus'] = False  # 显示负号

# 方式二
font = {'family': 'SimHei',
        'weight': 'bold',
        'size': '20'}
plt.rc('font', **font)  # 可以给字体设置更多属性
plt.rc('axes', unicode_minus=False) # 显示负号

# 方式三
from matplotlib.font_manager impot FontProperties
# 可以传入自定义字体，在fname那里传入路径('./SimHei.ttf')即可
font = FontProperties(fname='SimHei.ttf', size=14)
# 这种方式是哪里需要就在哪里设置
plt.xlabel("你是什么东西", fontsize=14, fontproperties=font)
```

---

### 4. 隐藏边框

```python
# 一次性去掉所有边框
plt.axis('off')

# 去掉上、右边框
ax = plt.gca()  # get current axis
ax.spine['right'].set_visible(False)
ax.spine['top'].set_visible(False)
```

---

## 二、细节设置

### 1. 数轴刻度、图片尺寸、保存图片

```python
# 导入pyplot
from matplotlib import pyplot as plt  

# figsize修改图片尺寸；修改dpi，让图片更清晰；(facecolor背景色，		edgecolor边缘色，clear是否清楚原来的画布，默认False，即建新图)
fig = plt.figure(figsize=(20,8),dpi=100)  
x = range(2, 26, 2)
y = [15,13,14.5,17,20,25,26,24,23,22,18,15]

# 设置x、y轴刻度
plt.xticks(x)
# plt.xticks(x[::2]) 让刻度不太密集
plt.yticks(min(y),max(y)+1)

# 绘制折线图
plt.plot(x,y) 

# 保存图片 png是矢量图，不会失真
plt.savefig("./name.png")  # 也可以在这里设置dpi=100

# 展示图形
plt.show()  
```

---

### 2. x轴显示字符串（刻度竖直）

```python
_x = list(x)[::10]  # 取步长是为了显示时不至于过密集
_xtick_labels = ["hello,{}".format(i) for i in _x]

# 表示在_x的位置上添加_xtick_labels的数据
# 如果只传入_x，那么_x位置上就是_x的数据
plt.xticks(_x,_xtick_labels,rotation=90)  # 让刻度竖直显示 
```

---

### 3. 数轴标签、图片标题

```python
# 标签
plt.xlabel("时间")  # x轴标签
plt.ylabel('温度')  # y轴标签

# 图片标题
plt.title("时间-温度图")
```

---

### 4. 显示网格

```python
# 显示网格
plt.grid()

# 设置透明度
plt.grid(alpha=0.4)

# 只显示x(y)轴网格线
plt.grid(axis='x') # 或者y

# 颜色、形状、粗细
plt.gird(color='red', linestyle='-', linewidth=5)
```

---

### 5. 显示图例

```python
# 显示图例
plt.legend(prop=font, loc='best') # prop显示中文字体，loc设置位置,"upper right"等
```

---

### 6. 添加注释

```python
# 带箭头的
plt.annotate(s='注释内容', fontsize=12,
             xy=(x,y),  # 标记点坐标
             xytext=(+30,-30),  # 注释偏移位置
             arrowprops=dict(facecolor='black',
                             width=2, # 箭头宽度
                             headwidth=10, # 箭头头部宽度
                             headlength=10, # 箭头头部长度
                             shrink=0.1)) # 箭头两端收缩比

# 不带箭头的
plt.text(x,y,'注释内容',fontsize=12)
```

---

### 7. 添加水印

```python
# 图片水印
img = plt.imread('./图片地址.png')  # 导入图
plt.figimage(img,
             x, y,  # 图片位置
             origin='upper', # 图片朝向
             alpha=0.6)

# 背景水印
plt.imshow(img, extent=[x_begin, x_end, y_begin, y_end], alpha=0.3)

# 文本水印
plt.text(x=x, y=y,  # 文本坐标
         s="水印内容", alpha=0.5,
         rotation=15,  # 旋转角度
         ha='left',  # 左端对齐
         va='top',  # 顶端对齐
         fontdict=dict(fontsize=12, color='gray',
                       family='monospace',  # 字体 "serif"
                       weight='light')) # 磅 "normal""bold"
```

---

## 三、基本图表

### 1. 折线图

```python
import matplotlib.pyplot as plt
import numpy as np
 
T = np.array([6, 7, 8, 9, 10, 11, 12])
power = np.array([1.53E+03, 5.92E+02, 2.04E+02, 7.24E+01, 2.72E+01, 1.10E+01, 4.70E+00])
 
plt.plot(T,power)
plt.show()
```

![](https://img-blog.csdn.net/20170412155842304?waterm…/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

---

### 2. 平滑曲线图

```python
import matplotlib.pyplot as plt
import numpy as np
from scipy.interpolate import spline
 
T = np.array([6, 7, 8, 9, 10, 11, 12])
power = np.array([1.53E+03, 5.92E+02, 2.04E+02, 7.24E+01, 2.72E+01, 1.10E+01, 4.70E+00])
xnew = np.linspace(T.min(),T.max(),300) #300 represents number of points to make between T.min and T.max
 
power_smooth = spline(T,power,xnew)
 
plt.plot(xnew,power_smooth)
plt.show()
```

![](https://img-blog.csdn.net/20170412160135212?waterm…/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

---

### 3. 散点图

```python
import matplotlib.pyplot as plt
import numpy as np
 
# 第一组散点
x = np.array([1, 2, 3, 4, 5, 6, 7, 8])
y = np.array([1, 4, 9, 16, 7, 11, 23, 18])
colors = np.array([0, 10, 20, 30, 40, 45, 50, 55])
plt.scatter(x, y,s=100,c=colors,alpha=0.5,cmap='viridis')      # s 点的大小  c 点的颜色 alpha 透明度 cmap 颜色条(color需要设置为数组)
plt.colorbar()  # 显示颜色条
plt.show()
```

<img src='data:img/jpg;base64,iVBORw0KGgoAAAANSUhEUgAAAg0AAAGmCAYAAAD/K7ckAAAgAElEQVR4AezBf3CdhX3v+ff3OY90
JEs6R5Z/SBaWwfw0AUwSksVqSArExfHt0FD7dgqTbknLTGYyDlPwZNKhk580HWfyR0kzY2inw0Dy
B+WGu4UMuQnZ1F3MZmOz4NQQIPW1icFyZMlgWzq2bB1J5/nsqne065uBw/GJBdLx5/UK/b8wMzMz
ewcJZmZmZjVIMDMzM6tBgpmZmVkNEszMzMxqkGBmZmZWgwQzMzOzGiSYmZmZ1SDBzMzMrAYJZmZm
ZjVIMDMzM6tBgpmZmVkNEszMzMxqkGBmZmZWgwQzMzOzGiSYmZmZ1SDBzMzMrAYJZmZmZjVIMDMz
M6tBgpmZmVkNUuaQLMsYHByko6ODiMDMzOztSOL48eP09vaSJAmzZXx8nImJCX5bzc3NtLS0MJ+l
zCGDg4P09fVhZmZWq4GBAZYvX85sGB8fZ+UF3QwNl/ht9fT0sH//flpaWpivUuaQjo4Opg0MDFAo
FDAzM3s7pVKJvr4+Ojo6mC0TExMMDZd47ZdfpdDRQr1Kx8e54PKvMjExQUtLC/NVyhwSEUwrFAoU
CgXMzMzeSUQw2zo68nQU8tRLiEaQYGZmZlaDFDMzM6tKgKifaAwpZmZmVpUQQtRLiEaQYGZmZlaD
FDMzM6sqk8gk6pVJNIIUMzObsyrZOJWshJgiiVbSpJOIwN5dAkT9RGNIMTOzOUUS5cohjo+/QKn8
HFPZcYRIookFTRdRbPkwbc2rSCKP2bspxczM5gwp4+jJ/4MjJ3/CVFYiTQqkSSdBQqYJSuUXOF5+
gbbmy+jpuJXm3GJs9gkhRL2EaAQpZmY2J0jiyMltvDH2A9KknQVNlxIRzMixgKZcJ5nKnJh4hcHR
73Be8c9oynVhs0uAqJ9oDAlmZjYnnJp8lSMn/3fSpIPm3FIigreSRJ7W9CJOTu7jjbEfYvZuSTAz
szmhVP45lewkzbklvJMkUppz3Zwov0R5ahibXRkiQ2SIDJEhMkSGyBAZIkNkiAyRITJEhsgQGaIR
JJiZ2XtusnKUUvkFmnKLqFWadDKpUY6XX8RmlwABAgQIECBAgAABAgQIECBAgGgMCWZm9p6bqBxm
KivRlHRSq4ggR57xqQFsdgkQIECAAAECBAgQIECAAAECBIjGkGBmZu+5TFOgDEg4MzkylTF7N6SY
mdl7LolmInKIKYImaiUmySULsNmVCTJRt0w0hAQzM3vP5dNemnJdTFaOUCupgphiQdNF2OwSIECA
AAECBAgQIECAAAECBAgQjSHBzMzec2nSTjH/YaayESRRi8nsCE25xbQ3X4XZuyHBzMzmhELLB2jK
LWZ8agBJVFPJTjGZHaWY/xBNuSI2+wQIECBAgAABAgQIECBAgADROBLMzGxOyKe9dLdvIIkmTlVe
I9MEv0kSk5VjjE+9TiH/YRYtuAmbfQIECBAgQIAAAQIECBAgQIAAAaIxpJiZ2ZxRaPkASTRxeOxJ
Tk0dIAhy0U5EQqYyFY2Riw66FlzPkrY/IJe0YPZuSTEzszmlPX8lrU0XMzbxCqPlXZSnDoEqNOWW
0JVfSyG/muZcDxGBvTsygoygXhlBI0gxM7M5J5e0UGj5IIWWDyIJyIjIYe8NAaJ+ojGkmJnZnBYR
QA6z91qKmZmZVSUFUlAvKWgEKWZmZlZVBmTUL6MxpJiZmVlVIhBBvUTQCBLMzMxsTvnqV79KRBAR
RAQRwapVq5gxPj7Opk2bWLRoEe3t7WzcuJHh4WFmW4KZmZlVJQIRiEAEIhCBCEQgAhGIQAQiEIEI
RCCCM3XFFVdw6NAhDh06xKFDh/jpT3/KjLvvvpsnn3ySxx57jO3btzM4OMiGDRuYbSlmZmZWVQZk
1C/jzKVpSk9PD79pdHSUBx98kEceeYQbb7yRaQ899BCXX345O3fuZM2aNcyWBDMzM3tXlEolSqUS
pVKJUqlEuVzm7ezdu5fe3l4uvPBCPvWpT3HgwAGm7dq1i8nJSdauXcuMVatWsWLFCnbs2MFsSjAz
M7OqpEAKpEAKpEAKpEAKpEAKpEAKpEAKpEAKpGBaX18fxWKRYrFIsVhky5YtvJVrr72Whx9+mKee
eooHHniA/fv389GPfpTjx48zNDREc3MznZ2dnK67u5uhoSFmU4qZmZlVJQIR1EsE0wYGBigUCszI
5/O8lfXr1zNj9erVXHvttZx//vl873vfo7W1lfdKgpmZmb0rCoUChUKBQqFAoVAgn89Ti87OTi69
9FL27dtHT08PExMTjIyMcLrh4WF6enqYTQlmZmZWVQZkBBlBRpARZAQZQUaQEWQEGUFGkBFkBBlB
RpDx2zlx4gSvvvoqy5Yt45prrqGpqYlt27YxY8+ePRw4cID+/n5mU4qZmZlVJQIR1EsEZ+Lzn/88
N998M+effz6Dg4N85StfIZfLcdttt1EsFrnjjjvYvHkzXV1dFAoF7rzzTvr7+1mzZg2zKcXMzMzm
lIMHD3Lbbbdx5MgRlixZwnXXXcfOnTtZsmQJ0+677z6SJGHjxo2Uy2XWrVvH/fffz2xLMTMzs6oE
iPqJM/Poo49STUtLC1u3bmXr1q28m1LMzMysKhFkBPUSQSNIMTMzs6qkQArqJQWNIMHMzMysBilm
ZmZWlQhEUC8RNIIUMzMzqyojyAjqlRE0ggQzMzOzGqSYmZlZVSIQQb1E0AhSzMzMrCoRSEG9RNAI
EszMzMxqkGJmZmZVZQQZQb0ygkaQYmZmZlUJEPUTjSHBzMzMrAYpZmZmVpUIRFAvETSCFDMzM6sq
U5ApqFemoBGkmJmZWVUiEEG9RNAIEszMzMxqkGJmZmZViUAE9RJBI0gxMzOzqjKCjKBeGUEjSKjR
li1b+PCHP0xHRwdLly7llltuYc+ePZxufHycTZs2sWjRItrb29m4cSPDw8OYmZnZ/JdQo+3bt7Np
0yZ27tzJT37yEyYnJ7npppsYGxtjxt13382TTz7JY489xvbt2xkcHGTDhg2YmZnNawIJJJBAAgkk
kEACCSSQQAIJJJAA0RBSavTUU09xuocffpilS5eya9cuPvaxjzE6OsqDDz7II488wo033si0hx56
iMsvv5ydO3eyZs0azMzM5iMRiKBeImgECXUaHR1lWldXF9N27drF5OQka9euZcaqVatYsWIFO3bs
4K2Uy2VKpRKlUolSqUSpVMLMzMzmpoQ6ZFnGXXfdxUc+8hGuvPJKpg0NDdHc3ExnZyen6+7uZmho
iLeyZcsWisUixWKRYrFIX18fZmZmc40IRCACEYhABCIQgQhEIAIRiEAEIhCBCBpBQh02bdrESy+9
xKOPPspv45577mF0dJTR0VFGR0cZGBjAzMxsrskIMoKMICPICDKCjCAjyAgygowgI8gIMoKMICPI
CBpByhn63Oc+xw9+8AOeeeYZli9fzoyenh4mJiYYGRmhs7OTGcPDw/T09PBW8vk8+XweMzMzm/sS
aiSJz33uczz++OP867/+KytXruR011xzDU1NTWzbto0Ze/bs4cCBA/T392NmZjZfSYEUSIEUSIEU
SIEUSIEUSIEUSIEUSIEUSEEjSKnRpk2beOSRR/j+979PR0cHQ0NDTCsWi7S2tlIsFrnjjjvYvHkz
XV1dFAoF7rzzTvr7+1mzZg1mZmbzlQBRP9EYUmr0wAMPMO3666/ndA899BCf/vSnmXbfffeRJAkb
N26kXC6zbt067r//fszMzOYzASKol2gMKTWSxDtpaWlh69atbN26FTMzM2ssKWZmZlZVpiBTUK9M
QSNIMTMzs6pEIIJ6iaARJJiZmZnVIMXMzMyqEoEI6iWCRpBiZmZmVUkgUTeJhpBgZmZmVoMUMzMz
qyojyAjqlRE0ghQzMzOrSgQiqJcIGkGCmZmZWQ1SzMzMrCoRiKBeImgEKWZmZlaVBBJ1k2gIKWZm
ZvYOAhHUL2gECWZmZmY1SDEzM7OqpEAK6iUFjSDFzMzMqsqAjPplNIYEMzMzsxqkmJmZzTJlYzD1
CprcAzoOpJDrIZpWQ24FEcFcJgIR1EsEjSDFzMxslkgVVH4GJn4KlcMQCdAEEkzuRuVnIL0EWv4T
kS5nrpICKaiXFDSCFDMzs1kgVdCpJ6C8HWIB5FZCpPx/JNAJmHwRZcOw4E+IdCU2dyWYmZnNApWf
gfJ2SJZCrhci5X8SAUkH5C6Gypvo5H9B2VHmIgECBAgQIECAAAECBAgQIECAANEYEszMzM4yZWMw
8VOIBZAUqCoSyF0AlQGYeIG5SAQiEIEIRCACEYhABCIQgQhEIAIRiEAEjSDBzMzsbJt6BSqHIVlK
TSIH0YYm/m+kCWxuSjEzMzvLNLkHIoFIqVmyGCpDUBmA9CLmEimQgnpJQSNIMTMzO9t0HGjizOSB
CVCZuUaAqJ9oDClmZmZnXQoSZyYDEiBhrhGBCOolgkaQYGZmdrbleoBxkKiZjkO0QbIQm5sSzMzM
zrJoWg2xAHSCmmVvQtPlkCxlrpFAAgkkkEACCSSQQAIJJJBAAgkkkGgICWZmZmdbbgWkl0B2CJTx
jrISRI5ovoaIYK4RgQhEIAIRiEAEIhCBCEQgAhGIQAQiEEG9vvGNbxAR3HXXXcwYHx9n06ZNLFq0
iPb2djZu3Mjw8DCzLcHMzOwsiwii5T9Brhsq+0EV3lZWgmwImj8C6Srs//fcc8/xD//wD6xevZrT
3X333Tz55JM89thjbN++ncHBQTZs2MBsSzAzM5sFkS4nFvwJ5JZBZR9UDoLGQQJVIBuBqX2go5C/
nmj9AyJyzEVSIAVSIAVSIAVSIAVSIAVSIAVSIAVSIAVScKZOnDjBpz71Kf7xH/+RhQsXMmN0dJQH
H3yQv/3bv+XGG2/kmmuu4aGHHuJnP/sZO3fuZDYlmJmZzZJIVxLtnyFa/zMki6AyBJW9UNkPOgXN
HyLa7iBa/5CIZuYqAQIECBAgQIAAAQIECBAgQIAA8T+USiVKpRKlUolSqUS5XObtbNq0id///d9n
7dq1nG7Xrl1MTk6ydu1aZqxatYoVK1awY8cOZlOKmZnZLIqkC1pugPxHoDIAKgMJJAshWUpEcK7o
6+vjdF/5ylf46le/ym969NFH+fnPf85zzz3HbxoaGqK5uZnOzk5O193dzdDQELMpxczM7F0Q0Qzp
RcxHIhBBvUQwbWBggEKhwIx8Ps9vGhgY4C/+4i/4yU9+QktLC3NJgpmZmVUlgQQSSCCBBBJIIIEE
EkgggQQSSCDxHwqFAoVCgUKhQKFQIJ/P85t27drF4cOH+eAHP0iapqRpyvbt2/n2t79NmqZ0d3cz
MTHByMgIpxseHqanp4fZlGJmZmZzxsc//nF+8YtfcLo/+7M/Y9WqVfzlX/4lfX19NDU1sW3bNjZu
3Mi0PXv2cODAAfr7+5lNKWZmZlaVCERQLxHUqqOjgyuvvJLTtbW1sWjRIq688kqm3XHHHWzevJmu
ri4KhQJ33nkn/f39rFmzhtmUYmZmZlVJIFE3ibPqvvvuI0kSNm7cSLlcZt26ddx///3MthQzMzN7
B4EI6hf8Np5++mlO19LSwtatW9m6dSvvpgQzMzOzGqSYmZlZVQJE/URjSDEzM7OqJJCCekk0hAQz
MzOzGqSYmZlZVQJE/URjSDEzM7OqpEAK6iUFjSDBzMzMrAYpZmZmVpUAUT/RGFLM7IxNVCoMnTxO
eapCU5KwuLWN9uZmzKwxiUAE9RJBI0gxs5odGz/F7jcOsfPQAMNjx5lSRhIJxXwLH1raywe6e1nR
0YmZWSNKMbOa7Dn6Bo/u+QWDJ0osaGpiSWsbTUmOisRI+RT/bf8efjr4Or+/chW/u/wCIgIzawwS
SNRNoiGkmNk7enXkKN995d8YLZe5dOFikghmNAE9aQfdC9oZPnmC/23vS0y7vm8lZtYoAgjqFzSC
BDOrajKr8M/7XuZo+RQXFheSRPBWIoKetg5a0yZ+uH8PgydKmFljkEACCSSQQAIJJJBAAgkkkEAC
CSSQaAgJZlbVnqNv8npphBXtRSKCd9KzoJ2R8jgvvHEIM7NGkmBmVf3b4UEqWUZL2kQtIoJic55n
Dx3k1NQkZjb/iUAEIhCBCEQgAhGIQAQiEIEIRCACEYigEaSYWVWvHx+hvTnPmSjmWzgyfpKR8jit
aRNmNr8JkKibaAwJZva2JDFZqZCL4EzkIsgkJrMKZmaNIsHM3lZE0NbUzESlwpmYyCqkSUI+l2Jm
1igSzKyqqxb3cGKyjCRq9eapk5xfWMiS1jbMbP4TgQhEIAIRiEAEIhCBCEQgAhGIQAQiEEEjSDCz
qt6/dBmF5hZGyuPUYiqrMJlVuLZnOUkEZmaNIsHMqupZ0M4HlvZy6ORxxqemqCaTeHX0KBcWu7hy
cTdm1hgkkEACCSSQQAIJJJBAAgkkkEACCSQaQoqZVRUR3HLx5ZQmxvn54UG6W9vpamklIpghibHJ
CQ6OlVjeXuC2VVfT1tSMmTUGEYigXiJoBClm9o7ampq5/X0fYGFLKz8fHuTfj71Ja5rSnOSoSIxN
TtCaNrF6cQ8bLrmCZW0dmJk1mhQzq8mCpmZuvWw1N/ZdyItvDPHK0TcYm5wgn0u5oNDJ+5cu44LC
QpIIzKzBCBD1Ew0hxczOyNIF7aw9/2LWnn8xZnZuECDqJxpDipmZmVWnAAV1U9AIEszMzMxqkFCj
Z555hptvvpne3l4igieeeILTffrTnyYiiAgigojgE5/4BGZmZvOdAAECBAgQIECAAAECBAgQIECA
aAwJNRobG+Pqq69m69atvJ1PfOITHDp0iEOHDnHo0CH+6Z/+CTMzs/lOAgkkkEACCSSQQAIJJJBA
AgkkkECiIaTUaP369axfv55q8vk8PT09mJmZWeNJOIuefvppli5dymWXXcZnP/tZjhw5gpmZ2fwX
QAABBBBAAAEEEEAAAQQQQAABBBA0gpSz5BOf+AQbNmxg5cqVvPrqq/zVX/0V69evZ8eOHeRyOd5K
uVymXC4zo1QqYWZmNtdIIFE3iYaQcpbceuutzLjqqqtYvXo1F110EU8//TQf//jHeStbtmzha1/7
GmZmZjb3JcySCy+8kMWLF7Nv3z7ezj333MPo6Cijo6OMjo4yMDCAmZmZzU0ps+TgwYMcOXKEZcuW
8Xby+Tz5fB4zM7O5LRBB/YJGkFKjEydOsG/fPmbs37+f3bt309XVRVdXF1/72tfYuHEjPT09vPrq
q3zhC1/g4osvZt26dZiZmdn8l1Kj559/nhtuuIEZmzdvZtrtt9/OAw88wIsvvsh3vvMdRkZG6O3t
5aabbuKv//qvyefzmJmZzWsCRP1EQ0ip0fXXX48k3s6Pf/xjzMzMrHGlmJmZWVUSSNRNoiEkmJmZ
mdUgxczMzN5BAEH9gkaQYmZmZtUJEPUTDSHBzMzMrAYpZmZmVpUAUT/RGFLMzMysOgGifqIhJJiZ
mZnVIMXMzMzeQQBB/YJGkGJmZmbVCRD1Ew0hwczMzKwGKWZmZlaVAFE/0RhSzMzMrDoBon6iIaSY
mZnZOwggqF/QCBLMzMzMapBgZmZmVoMUMzMzq06AqJ9oCAlmZmZmNUgwMzOzOeWBBx5g9erVFAoF
CoUC/f39/OhHP2LG+Pg4mzZtYtGiRbS3t7Nx40aGh4eZbQlmZmZWnQABAgQIECBAgAABAgQIECBA
gDgjy5cv5xvf+Aa7du3i+eef58Ybb+STn/wkL7/8MtPuvvtunnzySR577DG2b9/O4OAgGzZsYLal
mJmZ2Zxy8803c7q/+Zu/4YEHHmDnzp0sX76cBx98kEceeYQbb7yRaQ899BCXX345O3fuZM2aNcyW
BDMzM5uzKpUKjz76KGNjY/T397Nr1y4mJydZu3YtM1atWsWKFSvYsWMHsynFzMzMqlOAgropmFYq
lThdPp8nn8/zVn7xi1/Q39/P+Pg47e3tPP7447zvfe9j9+7dNDc309nZyem6u7sZGhpiNiWYmZnZ
u6Kvr49isUixWKRYLLJlyxbezmWXXcbu3bt59tln+exnP8vtt9/OK6+8wnspxczMzN4VAwMDFAoF
ZuTzed5Oc3MzF198MdOuueYannvuOf7u7/6OP/7jP2ZiYoKRkRE6OzuZMTw8TE9PD7MpwczMzKoT
IECAAAECBAgQIECAAAECBAgQ/6FQKFAoFCgUChQKBfL5PLXKsoxyucw111xDU1MT27ZtY8aePXs4
cOAA/f39zKYUMzMzm1Puuece1q9fz4oVKzh+/DiPPPIITz/9ND/+8Y8pFovccccdbN68ma6uLgqF
AnfeeSf9/f2sWbOG2ZRiZmZmc8rhw4f50z/9Uw4dOkSxWGT16tX8+Mc/5vd+7/eYdt9995EkCRs3
bqRcLrNu3Truv/9+ZluKmZmZVSdA1E+ckQcffJBqWlpa2Lp1K1u3buXdlGBmZmZWgwQzMzOzGqSY
mZlZdQJE/URDSDEzM7N3EEBQv6ARJJiZmZnVIMXMzMyqCiBE3YLGkGBmZmZWgwQzMzOzGiSYmZmZ
1SDFzMzMqhMg6icaQoKZmZlZDRLMzMzMapBiZmZm1QkQ9RMNIcHMzMysBglmZmZmNUgxMzOzqkIQ
om4hGkKCmZmZWQ0SzMzMzGqQYmbWIMamjjF46r8zNL6PicopctFEZ1M35y1YxaJ8H0nkMKuLAFE/
0RBSzMzmucmszC9LzzAw9jLj2XGaooVcpAhxdOIgr518gUXNy7mi8wa6mnsxs/qkmJnNY5NZmZ8f
+28cHHuZtnQhS5rPJyLhdBPZOG+UX+O5I0/woa6bWZTvw8zOXIKZ2Tz276WfcnDsZRY2L6Mt7SQi
4Tc1Jy0sbl7Bycoo/3bsR5yqHMfsjChAAQpQgAIUoAAFKEABClCAAhSgAAUoaAQJZmbz1NjUCAMn
X6ItXUhT0kI1EUFX03mMTh7m0Kn/jpmduQQzs3nq0Km9nKocZ0GuQC2SSGiOFl4fe5GKpjCrVQhC
EIIQhCAEIQhBCEIQghCEIAQhCEGIhpBgZjZPHR7/FWk0E5FQqwVpJ8cn3+T45JuY2ZlJMDObpyay
U+Qi5UzkIiXTFFOawMzOTIqZ2TyVixRJnAkpIyIhIYdZzQSI+omGkGBmNk91Ni9jQqc4E+PZCfK5
NhaknZjZmUkwM5unelsvoynylCsnqYUkTlZKLG99Hy25NszszCSYmc1TXc29LMr3UZp6AynjnYxV
RsgnC+hdsAqzMyJAgAABAgQIECBAgAABAgQIECAaQoKZ2TwVkXBl8QY60sW8OTFApgpvRRInpo5S
zk5waUc/C5uWYWZnLsXMbB4rNnfzoUV/wL8d+xFvTgyQRjNtuU5y0YTIGK+c4FTlOPncAt5XuIFL
Ov4XIgKzMxVYipnZPLeweRm/s/iPGTq1lwMnX2R08jAVVQiCfG4Bl7V9hPMWrKKzqYeIwMzqk2Jm
1gBacm1c0P5+VrRdxYmpo0xmZXKR0porkM8twMx+eylmZg0kiRyFpiWYnVUCRP1EQ0gwMzMzq0FC
jZ555hluvvlment7iQieeOIJTieJL3/5yyxbtozW1lbWrl3L3r17MTMzm/cECBAgQIAAAQIECBAg
QIAAAQJEQ0io0djYGFdffTVbt27lrXzzm9/k29/+Nn//93/Ps88+S1tbG+vWrWN8fBwzMzOb/1Jq
tH79etavX89bkcS3vvUtvvjFL/LJT36Sad/97nfp7u7miSee4NZbb8XMzMzmt4SzYP/+/QwNDbF2
7VpmFItFrr32Wnbs2IGZmdl8FoIQhCAEIQhBCEIQghCEIAQhCEEIQhCiIaScBUNDQ0zr7u7mdN3d
3QwNDfF2yuUy5XKZGaVSCTMzM5ubEt5DW7ZsoVgsUiwWKRaL9PX1YWZmZnNTwlnQ09PDtOHhYU43
PDxMT08Pb+eee+5hdHSU0dFRRkdHGRgYwMzMbM4RIECAAAECBAgQIECAAAECBAgQDSHhLFi5ciU9
PT1s27aNGaVSiWeffZb+/n7eTj6fp1AoUCgUKBQKFAoFzMzMbG5KqdGJEyfYt28fM/bv38/u3bvp
6upixYoV3HXXXXz961/nkksuYeXKlXzpS1+it7eXW265BTMzM5v/Umr0/PPPc8MNNzBj8+bNTLv9
9tt5+OGH+cIXvsDY2Bif+cxnGBkZ4brrruOpp56ipaUFMzOzeU2AqJ9oCCk1uv7665HE24kI7r33
Xu69917MzMwaSQBB/YLGkGBmZmZWgxSzd0GWicGjo5ROlZnWmm9i+aIiTbkcZmZzngBRP9EQUsxm
0cTUFC8dGObnrx7kV8NHGZ+cQkBzLkdvV4EPX9zHVef30NGax8zM5rYUs1ly/FSZx599iRdeO0Qu
gsXFNtryzUwrT04xNHKcx372Aj//1UH+8++spqezAzMzm7sSzGbB+MQU/7zzJXa9+mt6uwpc0N1F
e0ueiCAiaGluom9xJyu7F/Hq8FEe/ekLHDl+EjOzOUmAAAECBAgQIECAAAECBAgQIEA0hASzWbB7
/6954bVBzl/SSWtzE28nzSVc2N3F/uGjPPPKrzAzs7krwewsm6pkPLfvIPmmlJbmJt5JLklYXFjA
i68d4tiJU5iZ2dyUYHaW7T98lIEjIywptFGrhW0LGBkb55cHD2NmNteEIAQhCEEIQhCCEIQgBCEI
QQhCEIIQhGgICWZn2cjYKaYqGS3NTdQqSYJpI2MnMTOzuSnB7CyrZCIiOFORBFOZMDM7123ZsoUP
f/jDdHR0sHTpUm655Rb27NnD6cbHx9m0aROLFi2ivb2djRs3Mjw8zGxKMDvLWptTJFHJMs6EMtHa
3ISZ2ZwjQIAAAQIECBAgQIAAAQIECBAgzsj27dvZtGkTO3fu5Cc/+QmTk5PcdNNNjI2NMePuu+/m
ySef5LHHHmP79u0MDg6yYcMGZlOK2Vl2wZIuOttaOXbiFIsLbdTiZHmCfFOOC7u7MDM71z311FOc
7uGHH2bp0qXs2rWLj33sY4yOjvLggw/yyABC9LQAACAASURBVCOPcOONNzLtoYce4vLLL2fnzp2s
WbOG2ZBgdpYV21q4+oJejp44iSRqcXj0BOcvXcgFSxdiZmb/s9HRUaZ1dXUxbdeuXUxOTrJ27Vpm
rFq1ihUrVrBjxw5mS4LZLPjQxeexuKONA2+OIIlq3iiNkUsSfueyC8glCWZmjapUKlEqlSiVSpRK
JcrlMu8kyzLuuusuPvKRj3DllVcybWhoiObmZjo7Ozldd3c3Q0NDzJYEs1lwXleRDWuuZEFzE78a
PspYeYLfVJ6c4sAbI5wqT7Du/Zey+vwezMzmogBCEIIQhCAEIQhBCEIQghCEIAQhCEHwP/T19VEs
FikWixSLRbZs2cI72bRpEy+99BKPPvoo77UUs1nyvr5u/uR3P8i/vLiX/cPHGJwcpbkpJQgmpqZI
koTzugr87hUX8oGVvUQEZmaNbGBggEKhwIx8Pk81n/vc5/jBD37AM888w/Lly5nR09PDxMQEIyMj
dHZ2MmN4eJienh5mS4rZLLqoZxErl3bx+hvHeHlgmCPHx8gExQUtrDpvCZcsW0xTmsPM7FxQKBQo
FAq8E0nceeedPP744zz99NOsXLmS011zzTU0NTWxbds2Nm7cyLQ9e/Zw4MAB+vv7mS0pZrMsSYKV
3V2s7O7CzGxeEiDqJ87Ipk2beOSRR/j+979PR0cHQ0NDTCsWi7S2tlIsFrnjjjvYvHkzXV1dFAoF
7rzzTvr7+1mzZg2zJcXMzMzmlAceeIBp119/Pad76KGH+PSnP820++67jyRJ2LhxI+VymXXr1nH/
/fczm1LMzMxsTpHEO2lpaWHr1q1s3bqVd0uKmZmZVSdA1E80hBQzMzOrKoCgfkFjSDAzMzOrQYqZ
mZlVJ0DUTzSEBDMzM7MapJiZmVl1AkT9RENIMDMzM6tBgpmZmVkNUszMzKyqEISoW4iGkGBmZmZW
gwQzMzOzGqSYmZlZdRJI1E2iEaSY2TkrU8bgqcO8OvY6R8ujZGS05Rawsn05FyxYTj7XjJnZjBQz
OycNnhrmZ2/+nIOnhpjIJmlOmghgUhVeGt3DonwnH+i8gtWdq0giwcwsxczOOa+NHeTHQ/8npckT
LMkvpDXXwukmsymOTYyy7fAOTlRO8juLPkgSCWbnqhCEqFuIhpBgZueUoxMj/Mvw/8XJykn6Wnto
zbXwm5qSlKUtiyikbTx7ZDcvl/ZiZpZgZueUX5b2cWRihJ78UiKCagpN7aSRY/exV5jMpjCzc1uC
mZ0zTlXG+WXpVTpyC0giqEVXcyeHy0c4cHIQs3OWAAECBAgQIECAAAECBAgQIECAaAgJZnbOOHTq
DY5NlOhsLlCr5qSJijIGTh7CzM5tCWZ2zpjIJgCRixxnIo0cJyunMLNzW4qZnTOSSJgmiYigVkKk
kcPsXBWCEHUL0RASzOycUWhqpzlp5lRlnFpJYkoVFjYXMbNzW4KZnTOW5hfRt2AZxyZL1Or41Bjt
uQVc1L4CMzu3JZjZOSOJhPcVLkaIU5Vx3kmmjKMTo6xs76OruROzc5YAAQIECBAgQIAAAQIECBAg
QIBoCAlmdk65uP0C3le4hOHyEU5Wxnk7FVU4eGqIntYlrFn0fszMUszsnJImOW5c2k9E8PLoXo4y
QmdTgQW5FoJgIpvk2OQo5WyC3tZubur+KF3NnZiZpZjZOSefa2bt0o9wUdsKflnax+snBzk2MYoQ
aZKyJN/FFYVLubTjAtrSBZid60IQom4hGkKKmZ2T0iTHJR0XcHH7+RyZOMaJqZNkEi25ZpbmF5Mm
OczMTpdiZue0iGBxvovF+S7MzKpJMTMzs+oEiPqJhpBiZmZm1QkQ9RMNIcXMzMyqCiCoX9AYEszM
zMxqkGJmZmbVSSBRN4lGkGBmZmZWgwQzMzOzGqSYmZlZdQJE/URDSDEzM7OqAgjqFzSGBDMzM7Ma
pJiZmVl1AkT9RENIMDMzM6tBgpmZmVkNUszMzKw6AaJ+oiGkmJmZWVUBBPULGkOKmZmZVSeBRN0k
GkGCmZmZWQ0SzqKvfvWrRAQRQUQQEaxatQozM7N5T4AAAQIECBAgQIAAAQIECBANI+Usu+KKK/iX
f/kXZqRpipmZmc1/KWdZmqb09PRgZmZmjSXhLNu7dy+9vb1ceOGFfOpTn+LAgQO8nXK5TKlUolQq
USqVKJVKmJmZzTkCBAgQIECAAAECBAgQIECAAAGiISScRddeey0PP/wwTz31FA888AD79+/nox/9
KMePH+etbNmyhWKxSLFYpFgs0tfXh5mZ2VwTQAABBBBAAAEEEEAAAQQQQAABBBA0hoSzaP369fzR
H/0Rq1evZt26dfzwhz9kZGSE733ve7yVe+65h9HRUUZHRxkdHWVgYAAzMzObm1JmUWdnJ5deein7
9u3jreTzefL5PGZmZnOaAFE/0RASZtGJEyd49dVXWbZsGWZmZvOXAAECBAgQIECAAAECBAgQIECA
aAQJZ9HnP/95tm/fzmuvvcbPfvYz/vAP/5BcLsdtt92GmZmZzW8pZ9HBgwe57bbbOHLkCEuWLOG6
665j586dLFmyBDMzs3lLgKifaAgpZ9Gjjz6KmZlZowlBiLqFaAgJNqdJYnKygiTMzOzc8Mwzz3Dz
zTfT29tLRPDEE09wOkl8+ctfZtmyZbS2trJ27Vr27t3LbEuxOadSyTg4cISXX/41+189zNRUhVwu
YXnfIq64cjkrL1xCmuYwM7PGNDY2xtVXX82f//mfs2HDBn7TN7/5Tb797W/zne98h5UrV/KlL32J
devW8corr9DS0sJsSbE55djREzz1wxfZv/8NJiemaOtoIU0TJiameGH367z0iwGWL+/ipvWr6e1d
iJmZvQskkKibxJlYv34969ev561I4lvf+hZf/OIX+eQnP8m07373u3R3d/PEE09w6623MlsSbM44
dvQE//xfn+Pf/32Qrq42LrhwCUuWdLBwYRuLFndwwcolLO0u8PrrR3j8vz7H4K+PYWZm80epVKJU
KlEqlSiVSpTLZc7U/v37GRoaYu3atcwoFotce+217Nixg9mUYHNCpZLx1A9f5MCBI5x/wWJaFzTz
VvL5Jlacv4g33zzOD3+wm1OnJjAzs/mhr6+PYrFIsVikWCyyZcsWztTQ0BDTuru7OV13dzdDQ0PM
phSbEw4OHGH//sMs6+0kl0uoJkmC5X1d/HrgGPv2DnPV6j7MzGwWCRD1E/9hYGCAQqHAjHw+z3yS
YHPCyy//momJCq2tzdQiTXMkueAXLx4gy4SZmc2eEIQgBCEIQQhCEIIQhCAEIQhBCEIQghD/oVAo
UCgUKBQKFAoF8vk8Z6qnp4dpw8PDnG54eJienh5mU4K957JM/GrfMB0dLZyJYucCDg2OcOLEOGZm
dm5YuXIlPT09bNu2jRmlUolnn32W/v5+ZlOKveemJitMTWXk0oQzkaYJp05mTE5WMDOz2SRA1E+c
iRMnTrBv3z5m7N+/n927d9PV1cWKFSu46667+PrXv84ll1zCypUr+dKXvkRvby+33HILsynF3nNp
U44kCaYqGWeiUhFJEqRpgpmZzSIBon7ijDz//PPccMMNzNi8eTPTbr/9dh5++GG+8IUvMDY2xmc+
8xlGRka47rrreOqpp2hpaWE2pdh7LkmC5X1dvPTiQRYtaqdWpdFT9CzrpL2tBTMzaxzXX389kng7
EcG9997Lvffey7spweaEK6/qI5JgojxFLSqVjImJKa5+/wpyaYKZmdlsS7A5YeWFSznvvIUMDh5D
EtVIYujQKIsXd3DpZT2Ymdksk0ACCSSQQAIJJJBAAgkkkEACCSSQaAQJNic0NeVYt341XV3tHHj9
CJWpjLeSZRmDvx6huTnHTZ+4io6OVszMbJYJECBAgAABAgQIECBAgAABAgSIhpBic8Z5y7v4w40f
4oc/2M3AgSOkTTmKnQtIcwmVLKM0eory+CSLlxT4vXVXcellyzAzM3u3pNicsrxvEf/r7R9l794h
Xth9gOGhESqVjCRJWNpd5P3vP///aQ9egKus74SPf//P8+RccsKTBHInCQm3YIjcY+TSNijXUbTb
rewquxux66wrVmtmu10606q7bbXbTnUvDtadFrtr3aqtWGenigtTVPYFQZBIsFwSRJJAEhOSnOTk
cnLO+b0970zeyTCIIeDiOf19Pswoy8N1/SillPrfYQDD+BmSg4P6zPGnepgzt5iKa4voDQ4wPBzF
SbGYkObHdiyUUkr9LxMBEcZNhGTgoD6zLMuQnpGKUkop9VlgoZRSSik1Bg5KKaWUujgBhPETkoKF
UkoppdQYOCillFLq4kRAhHETIRlYKKWUUkqNgYVSSiml1Bg4KKWUUuriRECEcRMhGVgopZRSSo2B
g1JKKaUuTgBh/ISkYKGUUkopNQYOSimllLooI4IRYbyMCMnAQimllFJqDCyUUkoppcbAQSmllFIX
JwIijJsIycBBKaWUUp9M+INnoZRSSik1Bg5KKaWU+gQCCOMnJAMHpZRSSl2cAML4CUnBQimllFJq
DByUUkopdXEiIMK4iZAMHJRSSin1CQQQxk9IBg5KKaWUujgBhPETkoKFUkoppdQYOCillFLq4gQQ
YdyEpGChlFJKKTUGFkoppZRSY+CglFJKqYsTARHGTYRkYKGUUkopNQYOSaa/d4D+YD9x/jQfgfQA
SimllLp8DkkgFovRfPwsv9t7nN+9fYLwQBgRwePzMHPRVMoXl1F8zWRs20YppZS6ZCIgwriJkAwc
Elx4MMzOn79F3a4jDA2ESc9ySc9yiRsMDfHO9jrqdh2hYuksVtZU4w/4UEoppS6JCIgwbiIkA4cE
FhmOsH3rbzmw4z2yCydRkJnGaP40H5m56YSC/RzYcZjhcIR196zC4/OglFJKqUtjkcAOv/U7Dv32
CHlTcpiQmcbHCbipTJ6WR/3uo7y78zBKKaWUunQWCSoaiVK36whOik2q6+eT+AJe/Gk+Du06Qngw
jFJKKTVmIiACIiACIiACIiACIiACIiACIiACIiACIiQDiwR1+nfNtDS0MmnyRMZqUn4m7ac7OPne
hyillFJjJSKICCKCiCAiiAgigoggIogIIoKIICKICCKCiCAiJAOLBNV5tptIOIIv1ctYpXhTiEVj
nDvbjVJKKaUujUOCioQjGGMYj+FwBKWUUmrMBBDGT0gKDgnK40tBYoKIYIxhzAQ8vhSUUkqpsRNA
GD8hGVgkqLzSHHxpXvqDA4zVQGiQFJ9DXmkOSimllLo0Fgkqf2ouJRVFdJ45x1h1tnQxeUYBxddM
RimllBozERABERABERABERABERABERABERABERABEZKBRYIyxjCvugI7xaarrYdPEuzsJSYx5t9Q
gW3bKKWUUmMmgAACCCCAAAIIIIAAAggggAACCCAkBYsENnPRND73x9fT291H++kOotEY54vFYnS0
nKOrrYfF6xZRsWwWSimllLp0DgnMGMOSWyvxpnrZ88p+Tr/fhMfnwZfmI24oNMTgwBAZ2S43bvgc
VTcvwLIslFJKqUsiAiKMmwjJwCHBWZZF5ep5XFM1g+MHTnLk/xylu70HBDKn5jB76SzKFk3DnTQB
pZRSanwEEMZPSAYOSSItI8CCG69lwY3XEovFiLMsC6WUUkpdGQ5JyLIslFJKqStGAGH8hKTgoJRS
SqmLEwERxk2EZGBxhT355JOUlJTg8/moqqpi3759KKWUUolMRBARRAQRQUQQEUQEEUFEEBFEBBFB
RBARRAQRQURIBhZX0PPPP09tbS0PPfQQBw8eZO7cuaxevZr29naUUkopldgsrqAf/ehH3H333Wzc
uJHy8nKeeuopUlNT+elPf4pSSimVuAQQQAABBBBAAAEEEEAAAQQQQAABhPF48sknKSkpwefzUVVV
xb59+7iaLK6QcDjMgQMHWLFiBSMsy2LFihXs2bMHpZRSKmEJIIAAAggggAACCCCAAAIIIIAAAgiX
7Pnnn6e2tpaHHnqIgwcPMnfuXFavXk17eztXi8UV0tHRQTQaJTc3l9Fyc3NpbW3lQoaGhggGgwSD
QYLBIMFgEKWUUkrBj370I+6++242btxIeXk5Tz31FKmpqfz0pz/lanG4ih599FEeeeQRzhcMBlFK
KaUuJhgMEicifNoGhvoBYbwGhgaICwaDjOb1evF6vZwvHA5z4MABNm/ezAjLslixYgV79uzhanG4
QrKysrBtm7a2NkZra2sjLy+PC9m8eTO1tbWMaGlpoby8nKKiIpRSSqmx6O3tJT09nU+Dx+MhLy+P
Bx+/l8uVlpZGUVERoz300EM8/PDDnK+jo4NoNEpubi6j5ebmcvToUa4WhyvE4/GwcOFCdu7cyRe/
+EXiYrEYO3fu5L777uNCvF4vXq+XEWlpaTQ1NTFhwgSMMYxXMBikqKiIpqYmXNcl0QWDQYqKimhq
asJ1XRJZMBikqKiIpqYmXNcl0QWDQYqKimhqasJ1XRJZMBikqKiIpqYmXNcl0QWDQYqKimhqasJ1
XRJZMBikqKiIpqYmXNcl0QWDQYqKimhqasJ1XcZLROjt7aWgoIBPi8/n44MPPiAcDnO5RARjDKN5
vV4SicMVVFtbS01NDYsWLeK6667jiSeeIBQKsXHjRsbCsiwKCwu5UlzXxXVdkoXruriuSzJwXRfX
dUkWruviui7JwHVdXNclWbiui+u6JAPXdXFdl2Thui6u63I50tPT+bT5fD58Ph//m7KysrBtm7a2
NkZra2sjLy+Pq8XiCvqTP/kTfvjDH/Ltb3+befPmcejQIV577TVyc3NRSiml1Nh4PB4WLlzIzp07
GRGLxdi5cyeLFy/manG4wu677z7uu+8+lFJKKTV+tbW11NTUsGjRIq677jqeeOIJQqEQGzdu5Gqx
H/49kpBt21RXV+M4DsnAtm2qq6txHIdEZ9s21dXVOI5DMrBtm+rqahzHIdHZtk11dTWO45AMbNum
uroax3FIdLZtU11djeM4JAPbtqmursZxHNSFVVRUkJGRwXe/+11++MMfEvfzn/+csrIyrhYjv4dS
Siml1CewUEoppdT/JyKMh4hwPhFBRBgrEeGzzEIppZRS/4+IYIyhu7sbEUFEEBFEBBHhk4TDYfr7
+xktEonQ39/PWBhj6Ovr41KJCO3t7XzaHJRSSv3BEhFGGGMQEYwxxIkIxhjOJyLEGWO4GBEhzhjD
+UQEYwyfREQwxhAnIowwxvBpMMbQ1dVFc3Mztm3j8XiIM8YQFwqFSE9Px7Is4kSEaDTKiM7OTkQE
j8fDiM7OTmKxGB6Ph7hwOIzf78cYw2giQjQa5eTJk5SWljJhwgQ+iYhgjKGzs5Ouri4mTZqEbdt8
Woz8Hkoppf6gtLW1ceTIEQYGBsjJyaG7u5vy8nImT55MJBLhvffeo6WlhdTUVHw+H6mpqcyfP5+4
zs5O6uvrMcYQCATIz8/H4/EwceJELMtiRE9PD01NTWRlZZGXl8cIEaGurg7LspgzZw4XIyJ0dnbS
0NBAb28vrusyZcoUUlNTcV2XK0lEOHfuHEeOHGHPnj0YY4jLzc2lqqqKEydOcODAAR588EHS09OJ
6+7u5p//+Z+Jmz9/PnEHDhzAsizirr32Wmzb5uDBgziOQywWI+7+++8nIyMDESEWi/Gf//mfDA0N
ISIMDAyQmppK3JQpU7Btm1AoxM0338xoIoIxhuPHj/PSSy9hWRaO42CM4YYbbqChoYHh4WH+9E//
lCvFIYm8+eab/OAHP+DAgQOcPXuWbdu28cUvfpFE9Oijj/LSSy9x9OhR/H4/S5Ys4fvf/z5lZWUk
oi1btrBlyxZOnTpF3OzZs/n2t7/N2rVrSXSPPfYYmzdv5oEHHuCJJ54g0Tz88MM88sgjjFZWVsbR
o0dJRC0tLXzjG9/g1Vdfpb+/n+nTp7N161YWLVpEoikpKeHDDz/kfPfeey9PPvkk4yEi7N69m9/+
9rfMmzePkpISwuEwHR0dxGIxRITt27dz/Phxli5dis/no62tjXA4zIhQKMQ777zD4sWL6e/vp66u
jsLCQhobG5k7dy4+n4+4rq4uHMfh4MGDrF69mocffphnn32W2tpa6uvrGR4e5ic/+QnGGC4kEonw
q1/9is7OTubOnUtxcTEiwrFjx5g4cSJx1157LZdLRIhGo7z11lvs2bOHNWvW8Ed/9EdMnToV27aJ
a21tpb6+niVLlpCens6IjIwMvvWtbzHi0KFDFBUVMW/ePEY0NzdTWVlJfn4+kUgEx3E4X0tLC1/6
0pcoKCigu7sbESEuNTWVlpYWurq6GCEiGGOIa2pqor6+nj/7sz8jKyuLOGMMlmXR2tpKSUkJV5JD
EgmFQsydO5e77rqLL33pSySyN954g02bNlFZWUkkEuGb3/wmq1at4v333ycQCJBoCgsLeeyxx5gx
YwYiws9+9jNuvfVW3n33XWbPnk2i2r9/Pz/+8Y+ZM2cOiWz27Nns2LGDEY7jkIi6urpYunQpy5cv
59VXXyU7O5sTJ06QmZlJItq/fz/RaJQR9fX1rFy5kttuu43xam9vZ+fOnaxfv57y8nJGLFq0iLhI
JEJ7eztr1qzhmmuu4eMEAgGWLFnCiL6+PlpbW3n99de55ZZbiAuHw3z00UdMnjyZr3/96/z7v/87
P/vZz1i2bBkvvvgiX/3qV5k3bx73338/54vFYjz77LMUFxezfv16jDGICMYYysrK6Ovro6GhgaNH
jzJr1iwuhzGGYDDImTNnuPvuu5k4cSLNzc00NTUxadIkmpub+Z//+R+WL1/O9ddfz/mGh4dpb28n
FouRkZHB8PAwR48epbe3l1AoRG9vL2lpabz66qu0trbywAMPEAgEOF9ubi6O43DmzBkmT55MQUEB
cS0tLaSkpDDCGMPw8DBHjx4lFApRUFDAwMAAzc3NZGRk0N3dTU9PD7FYDL/fT2NjI0NDQ5SXl3O5
HJLI2rVrWbt2LcngtddeY7RnnnmGnJwcDhw4wOc//3kSzbp16xjtu9/9Llu2bGHv3r3Mnj2bRNTX
18eGDRv4t3/7N77zne+QyBzHIS8vj0T3/e9/n6KiIrZu3cqI0tJSElV2djajPfbYY0ybNo0vfOEL
jNfhw4eZOnUq5eXlXIiIsHDhQrxeL5ciEAgwadIk2traCIVCBAIBLMuio6ODqVOn4vV6ufnmm7np
ppsQEUpLS6msrGTfvn1cyJEjR/B4PCxfvpxoNMrevXvp6elhzpw51NfXs3LlSqZPn84LL7zArFmz
EBGMMYyViGCMYURmZiYbNmxARBgYGGBoaIjXXnsNv99PUVERK1asIDs7m2g0im3bnG9wcJD33nsP
y7IoLi4mOzubkydPkpWVRXZ2NlOmTMHn81FdXU0gEODjeDwejDHs27ePW2+9FWMMra2tpKamcr5w
OEwkEqG+vp6CggIcx2H+/Pn88pe/ZMaMGaSkpNDR0cHQ0BAtLS2Ul5dzuRxUQujp6SFu4sSJJLpo
NMqLL75IKBRi8eLFJKpNmzZx0003sWLFCr7zne+QyE6cOEFBQQE+n4/Fixfz6KOPUlxcTKJ55ZVX
WL16NbfddhtvvPEGkydP5t577+Xuu+8m0YXDYZ599llqa2sxxjAeIsLZs2eZPn06H8dxHMLhMNFo
lM7OTjIzM7Esi7Hw+/04jsOZM2eYMWMGxhiGhobIzs5m3bp13HPPPRw/fpwZM2Zw7tw5Dh8+zF/9
1V9xIW+99Ra33norcc8//zzGGFauXInX6+Xtt99m1apVBAIBQqEQ/f39pKamcvLkSUKhEGMxODiI
MYZFixYhIrz33nucOnWKY8eOMTAwwOTJk1m1ahW5ubm0tbVx6NAhWltb8Xq9pKenEwqFWL9+PT6f
D4/HQ35+PkePHmX16tWkpKTQ0NDA6dOnWbNmDZZlEQ6H2blzJ7fddhsXY4yhpKSEc+fO0dLSwttv
v019fT233347o6WkpLBgwQJOnTpFTk4OM2fOJC4SibBw4UI+//nP4/V6EREaGxtpaWnhSnBQn3mx
WIyvfe1rLF26lIqKChLV4cOHWbx4MYODg6SlpbFt2zbKy8tJRL/4xS84ePAg+/fvJ9FVVVXxzDPP
UFZWxtmzZ3nkkUf43Oc+R319PRMmTCCRnDx5ki1btlBbW8s3v/lN9u/fz/3334/H46GmpoZE9vLL
L9Pd3c2dd97JeIkIcWlpaXwcYwxz585l165dHD9+nLKyMlJSUiguLsYYw8cxxmDbNpFIhIGBAUbE
YjE8Hg/Tpk3ja1/7GmVlZTz++OPs27ePL3/5y2zYsIHRRIRYLMa5c+fIz89ncHCQxsZG/vZv/xaf
z8fAwACO42DbNiKC1+slFAqRmppKR0cH3d3djFVWVhZxxhhycnIIBAIsWbKEjIwMUlJSiGtsbKSk
pIRZs2YRFwqF6O7uprW1FZ/Pxwi/3097ezvvvvsulZWVTJ06ldLSUoaGhvD7/ezcuZPCwkLKysq4
kKqqKjweD3FZWVmsWrWKoaEhlixZwooVK0hPT0dEMMYwWjgc5tixY3z00UdYlsWUKVPo6Ohg7969
OI7DxIkT6e7u5kpxUJ95mzZtor6+nt27d5PIysrKOHToED09Pfzyl7+kpqaGN954g/LychJJU1MT
DzzwAP/93/+Nz+cj0a1du5YRc+bMoaqqiilTpvDCCy/wla98hUQSi8VYtGgR3/ve94ibP38+9fX1
PPXUU9TU1JDIfvKTn7B27VoKCgoYL2MMGRkZDA8PczEpKSmsXLmS7u5uGhsbCQQCvPbaa6xdu5aP
IyLEYjG6urrwer2c7+233yY/P59//Md/5I477sDv9/P1r3+dZcuWUVNTwwhjDJFIBL/fj2VZRCIR
MjMz8fl8xMViMTweDyN6enrweDzEXXfddYzXRx99RFx/fz9nz54lLjc3l8bGRs6dO4fX62WEiNDR
0UGciGCMwbIs1q9fT0pKCsYYotEoLKPYuQAAB8hJREFUJSUlpKSkEHf99dcTCAQQEYwxjBaNRmlp
aWHPnj3Yts2FTJs2jbq6OhYtWkROTg4j+vv76evro7i4GMuy8Pv9fPjhh5SWluLz+UhNTWVwcJAr
xUF9pt13333813/9F2+++SaFhYUkMo/Hw/Tp04lbuHAh+/fv55/+6Z/48Y9/TCI5cOAA7e3tLFiw
gBHRaJQ333yTf/3Xf2VoaAjbtklUGRkZzJw5k4aGBhJNfn4+5eXljHbNNdfwq1/9ikT24YcfsmPH
Dl566SUu14wZMzh9+jRjkZGRwYIFC+jq6uKll15i5cqVOI7DhRhj6Orqor+/n7y8PM63adMmnn76
aW688UZs26asrIzbbruNRx99lJqaGkYzxpCSksKIqqoqIpEItm3T2tpKVVUVIkJnZycejwfXdblc
ra2t+Hw+8vPzOX36NNFolNzcXI4dO8a0adMoKSmhtbWVSCRCnOM4xBljePzxxxkcHMQYw4IFC8jK
yiItLY1wOMzLL7/MiRMnGM0Yw9/93d8hIhhjsG2buXPnciHDw8NEIhFSU1NpaGigoqKC0XJzc8nN
zSU/P5+4aDTK6tWrqaiowHEc4oaHh7lSHNRnkojw1a9+lW3btrFr1y5KS0tJNrFYjKGhIRLNjTfe
yOHDhxlt48aNzJo1i2984xvYtk0i6+vro7GxkT//8z8n0SxdupRjx44x2vHjx5kyZQqJbOvWreTk
5HDTTTdxOYwxTJgwgaysLAYHB/H5fJxPRLiQcDhMNBrFcRwsyyItLY04EcEYQzQa5Te/+Q2lpaWk
p6dzvv7+fpqbm5kzZw7d3d1YloVlWcRiMc7nOA4zZsygq6uLzMxMOjo6ePnll7Ftm56eHgoKCvj1
r3/N6dOnWbNmDcYYLtfKlSsxxtDb28vBgwe55ZZb8Pv9WJbF/PnzcV2XjIwM0tPTCQQCjPbXf/3X
xDmOg4iwY8cOMjIyeP3111m2bBmVlZXk5uZyIT09PYgIhYWFXMjAwAAej4f09HSGh4dxHIcRxhiO
Hz/OiRMn8Hq9xMViMUKhEHV1dViWRVwwGCQvL48rwSGJ9PX10dDQwIgPPviAQ4cOMXHiRIqLi0kk
mzZt4rnnnuPXv/41EyZMoLW1lbj09HT8fj+JZvPmzaxdu5bi4mJ6e3t57rnn2LVrF9u3byfRTJgw
gYqKCkYLBAJMmjSJiooKEs3f/M3fsG7dOqZMmcKZM2d46KGHsG2b22+/nUTz4IMPsmTJEr73ve+x
fv169u3bx9NPP83TTz9NoorFYmzdupWamhocx+FyZWRk8MEHH3DmzBlycnLw+XzEYjGamprIz8/H
tm0GBwfx+/1YlsXAwAC/+c1vKCkpwev1Euf1elm6dClDQ0NEIhE6Ojp4/fXX6enp4Stf+QoXsm7d
Oh555BHKy8uZOHEidXV1vPDCC9xzzz2czxjD7NmzOXXqFBkZGaxZs4aTJ08iIkydOpVYLEZDQwPL
li0jKyuLyyUiGGMIBoM8/fTTzJw5E7/fj4gQJyLYts3JkyfJzc3F5/NRVFTECK/XizGG3t5eXnjh
BSzL4oYbbqCvr4+srCwaGxuxLIvMzEzS0tIYYYzhxRdfJBwOczFLly7FdV0GBgbweDyMNm/ePGbO
nMkn8fv9XAkOSeSdd95h+fLljKitrSWupqaGZ555hkSyZcsW4qqrqxlt69at3HnnnSSa9vZ2/uIv
/oKzZ8+Snp7OnDlz2L59OytXrkRdXc3Nzdx+++10dnaSnZ3NsmXL2Lt3L9nZ2SSayspKtm3bxubN
m/n7v/97SktLeeKJJ9iwYQOJaseOHZw+fZq77rqLKyEQCDB79mxef/11Tp8+zfDwMOFwmEAgwF13
3UUsFuMXv/gFAwMDDA0NISJMnz6dL3/5y4yoq6tj9+7dxNm2TXp6OjNnzuT2228nLS2NER988AEj
/uVf/oVvfetb3HHHHbS2thIIBLjlllv4h3/4B85njCEzM5OWlhba29vJzs5m+vTpiAjGGIwxFBYW
MmHCBK4EYwynTp3iueeeo6KignXr1jGir6+POJ/Px7Jly6irq2Pbtm0sX76cyspKRITe3l727NnD
vn37qKysZMWKFYzIyMjg+uuv56233iIuKysLy7K49tprMcbwl3/5l3wcEcEYg4jQ1dVFJBLBdV1E
BBGhv78fx3FwXZexaGlpITs7G4/Hw3gZ+T2UUkr9wYlEIvT39+M4DqmpqYw2MDBAOBwmNTWVlJQU
roauri62b9/O0NAQeXl5WJZFe3s7zc3NrFixgoULF3KltLS0cObMGSorK4k7dOgQe/bs4aOPPqK2
tpa0tDRGvP/++xQWFuK6LnGvvPIKg4ODfOELXyA3NxcRYWhoiB/84Ac8+OCDpKWlEXfmzBl2795N
JBLhjjvuYCyOHDlCfX09J0+eJD8/nzvvvJO4zs5O/uM//oNLtWHDBrKzsxkvI7+HUkop9RnV29tL
W1sb4XAYv99PXl4efr+fT1Nvby+tra1MnDiRSZMmcakikQiHDh1i7ty5pKSkMJqIYIxhLEKhEE1N
Tdi2TWlpKY7jcDUZ+T2UUkoppT6BhVJKKaXUGFgopZRSSo2BhVJKKaXUGFgopZRSSo2BhVJKKaXU
GFgopZRSSo2BhVJKKaXUGFgopZRSSo3B/wW0Rrn50VhooQAAAABJRU5ErkJggg=='/>

---

### 4. 条形图

```python
import matplotlib.pyplot as plt
import numpy as np
plt.style.use('_mpl-gallery')  # 指定绘图风格

# 随机创建数据:
np.random.seed(3)
x = 0.5 + np.arange(8) # [0.5,1.5,2.5,...,7.5]
y = np.random.uniform(2, 7, len(x))  # [2,7]的均匀分布

# 绘图
fig, ax = plt.subplots()

ax.bar(x, y, width=1, edgecolor="white", linewidth=0.7)  # 条形图

ax.set(xlim=(0, 8), xticks=np.arange(1, 8),
       ylim=(0, 8), yticks=np.arange(1, 8))  # 设置数轴范围

plt.show()
```

![](https://matplotlib.org/stable/_images/sphx_glr_bar_001_2_0x.png)

---

### 5. 饼图

```python
import matplotlib.pyplot as plt
import numpy as np

plt.style.use('_mpl-gallery-nogrid')  # 风格


# 创建数据
x = [1, 2, 3, 4]  # 数据，会显示出所占份额
colors = plt.get_cmap('Blues')(np.linspace(0.2, 0.7, len(x)))  # 采用蓝色系的渐变色

# plot
fig, ax = plt.subplots()
ax.pie(x, colors=colors, 
       radius=3,  # 饼图半径
       center=(4, 4),  # 饼图圆心
       wedgeprops={"linewidth": 1, "edgecolor": "white"}, frame=True)

ax.set(xlim=(0, 8), xticks=np.arange(1, 8),
       ylim=(0, 8), yticks=np.arange(1, 8))  # 设置数轴范围

plt.show()
```

![](https://matplotlib.org/stable/_images/sphx_glr_pie_001_2_0x.png)

---

### 6. 直方图

```python
import matplotlib.pyplot as plt
import numpy as np

plt.style.use('_mpl-gallery')

# make data
np.random.seed(1)
x = 4 + np.random.normal(0, 1.5, 200)  # 服从均值为4+0，标准差为1.5的正态分布，输出200个值

# plot:
fig, ax = plt.subplots()

ax.hist(x, 
        bins=8,  # 直方图组数
        linewidth=0.5, edgecolor="white")

ax.set(xlim=(0, 8), xticks=np.arange(1, 8),
       ylim=(0, 56), yticks=np.linspace(0, 56, 9))  # 设置数轴范围

plt.show()
```

![]( https://matplotlib.org/stable/_images/sphx_glr_hist_plot_001_2_0x.png)
