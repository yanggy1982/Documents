
# Time-NLP

## 一、什么是Time-NLP

Time-NLP是一个时间语义解析库。

主要有Java和Python两个版本

- Java版本：https://github.com/shinyke/Time-NLP/
- Python版本：https://github.com/Ryaninf/Time-NLPY

## 二、安装

### （一）Python

安装方法：

1、下载源码包

2、解压，并进入目录

3、安装

```shell
python setup.py install
```

4、安装regex包

```shell
pip install arrow
pip install regex
```


## 三、使用

### （一）Python

```python
from TimeNormalizer import TimeNormalizer # 引入包
import json

tn = TimeNormalizer()

res = tn.parse(target='下周三下午两点30分五秒') # target为待分析语句，timeBase为基准时间默认是当前时间
print(res)
res = tn.parse(target='2013年二月二十八日下午四点三十分二十九秒', timeBase='2013-02-28 16:30:29') # target为待分析语句，timeBase为基准时间默认是当前时间
print(res)
res = tn.parse(target='我需要大概33天2分钟', timeBase='2013-02-28 16:30:29') # target为待分析语句，timeBase为基准时间默认是当前时间
print(res)
res = tn.parse(target='1月末') # target为待分析语句，timeBase为基准时间默认是当前时间
print(res)

res = tn.parse(target='明天')
js = json.loads(res)
print(js)

```