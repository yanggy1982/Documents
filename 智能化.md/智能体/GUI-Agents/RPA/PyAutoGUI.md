
# PyAutoGUI

## 1、PyAutoGUI简介

### 1.1、什么是PyAutoGUI

&nbsp;&nbsp;&nbsp;&nbsp;PyAutoGUI是一个纯Python的GUI自动化工具，通过它可以让程序自动控制鼠标和键盘的一系列操作来达到自动化测试的目的。

### 1.2、主要功能

PyAutoGUI主要包括:
- **通用功能**
- **鼠标控制**
- **键盘控制**
- **屏幕窗口**
- **消息窗**


## 2、安装

```shell
pip install pyautogui
```

## 3、使用

### 3.1、屏幕图像处理

#### 一、获取屏幕尺寸

代码如下：

```python
import pyautogui
print(pyautogui.size())
```

说明：

&nbsp;&nbsp;&nbsp;&nbsp;pyautogui.size()函数返回两个整数的元组， 包含屏幕的宽度和高度的像素数。 返回的是屏幕的实际尺寸，和缩放比率没有关系。

> **获取缩放比例**
> ```python
> import ctypes
> 
> scale_factor = ctypes.windll.shcore.GetScaleFactorForDevice(0)
>```

#### 二、获取屏幕快照

- **全屏截图**

代码如下：

```python
import pyautogui

# 全屏截图
im = pyautogui.screenshot()  
# 保存截图
im.save("hello.jpg")
```

- **区域截图**

代码如下：

```python
import pyautogui

# 区域截图，并保存到im.png
im = pyautogui.screenshot('im.png', region=(0, 0, 830, 300))
```

#### 三、像素及匹配

##### （一）、获取像素

代码如下：

```python
import pyautogui

pix = pyautogui.pixel(0, 0)
print(pix)
```

##### （二）、像素匹配

代码如下：

```python
import pyautogui

isMatch = pyautogui.pixelMatchesColor(0, 0, (24, 24, 24))
print(isMatch)  # True

isMatch = pyautogui.pixelMatchesColor(0, 0, (25, 24, 24))
print(isMatch)  # False

# tolerance 容错 
isMatch = pyautogui.pixelMatchesColor(0, 0, (25, 25, 23), tolerance=1) # 允许差值为1
print(isMatch)  # True
```

#### 四、图像定位

##### （一）locateOnScreen

- **返回**：屏幕上首次发现该图像时左边的x坐标、 顶边的y坐标、 宽度以及高度。

- **示例**：

```python
import pyautogui

region = pyautogui.locateOnScreen('submit.png')
print(region)                     # Box(left=0, top=2080, width=96, height=80)
print(pyautogui.center(region))   # Point(x=48, y=2120)
```

- **注意事项**：

&nbsp;&nbsp;&nbsp;&nbsp;要成功识别， 屏幕上的图像必须与提供的图像完全匹配。 即使只差一个像素， locateOnScreen() 函数也会引发ImageNotFoundException异常。

- **增加容错率，指定查找范围以及可信度**：

```python
import pyautogui

region = pyautogui.locateOnScreen('submit.png', grayscale=True, region=(0, 1000, 100, 2080), confidence=0.9)
```

##### （二）locateCenterOnScreen

- **返回**：定位并求中间点的位置。
- **示例**：
```python
import pyautogui

center = pyautogui.locateCenterOnScreen('submit.png')
print(center)   # Point(x=48, y=2120)
```

##### （三）locateAllOnScreen

- **返回**：屏幕上首次发现该图像时左边的x坐标、 顶边的y坐标、 宽度以及高度。
- **示例**：



### 3.2、鼠标控制


### 3.3、键盘控制


### 3.4、通用功能


## 4、参考资料

https://blog.csdn.net/hitzsf/article/details/136723699













