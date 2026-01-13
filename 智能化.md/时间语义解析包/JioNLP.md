
# JioNLP

## 一、什么是JioNLP

- JioNLP是一个基于Python的时间语义解析库。

- 官方地址为：

https://github.com/dongrixinyu/JioNLP

## 二、安装

```shell
pip install jionlp
```

## 三、使用

### （一）在线测试地址

http://182.92.160.94:16666/#/extract_time

### （二）Python

- 例1：

```python
import time
import jionlp as jio

res = jio.parse_time('今年9月', time_base={'year': 2021})
print(res)
res = jio.parse_time('零三年元宵节晚上8点半', time_base=time.time())
print(res)
res = jio.parse_time('一万个小时')
print(res)
res = jio.parse_time('100天之后', time.time())
print(res)
res = jio.parse_time('每周五下午4点', time.time())
print(res)
```

返回的类型：

- 时间点(time_point)
- 时间范围(time_span)
- 时间长度(time_delta)
- 时间周期(time_period)
- 虚拟时间(time_virtual)
- 时间问词(time_query)


- 例2：时间语义解析

```python
import time
import jionlp as jio
text = '【新华社报2021-9-9】南方都市报今天发布了2021年8月份全国CPI（居民消费价格指数）和PPI（工业生产者出厂价格指数）数据。'
res = jio.ner.extract_time(text, time_base={'year': 2021})
print(res)
```























