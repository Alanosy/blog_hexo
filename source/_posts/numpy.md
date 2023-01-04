---
title: Numpy笔记
date: 2023/1/2 21:33:23
tags: [Numpy]
categories: [Numpy]
---
## 常量

### numpy.nan

### 表示空值。
nan = NaN = NAN
【例】两个numpy.nan是不相等的。

import numpy as np

print(np.nan == np.nan)  # False
print(np.nan != np.nan)  # True
numpy.isnan(x, *args, **kwargs) Test element-wise for NaN and return result as a boolean array.
【例】

import numpy as np

x = np.array([1, 1, 8, np.nan, 10])
print(x)
# [ 1.  1.  8. nan 10.]

y = np.isnan(x)
print(y)
# [False False False  True False]

z = np.count_nonzero(y)
print(z)  # 1

### numpy.inf
### 表示正无穷大。
Inf = inf = infty = Infinity = PINF
【例】

### numpy.pi
### 表示圆周率
pi = 3.1415926535897932384626433...

### numpy.e
### 表示自然常数
e = 2.718281828459045235360287471352662497757247093

## 数据类型

### 常见数据类型

Python 原生的数据类型相对较少， bool、int、float、str等。这在不需要关心数据在计算机中表示的所有方式的应用中是方便的。然而，对于科学计算，通常需要更多的控制。为了加以区分 numpy 在这些类型名称末尾都加了“_”。

下表列举了常用 numpy 基本类型。

类型	备注	说明
bool_ = bool8	8位	布尔类型
int8 = byte	8位	整型
int16 = short	16位	整型
int32 = intc	32位	整型
int_ = int64 = long = int0 = intp	64位	整型
uint8 = ubyte	8位	无符号整型
uint16 = ushort	16位	无符号整型
uint32 = uintc	32位	无符号整型
uint64 = uintp = uint0 = uint	64位	无符号整型
float16 = half	16位	浮点型
float32 = single	32位	浮点型
float_ = float64 = double	64位	浮点型
str_ = unicode_ = str0 = unicode	|Unicode 字符串	
datetime64	|日期时间类型	
timedelta64	|表示两个时间之间的间隔	
创建数据类型

numpy 的数值类型实际上是 dtype 对象的实例。

class dtype(object):
    def __init__(self, obj, align=False, copy=False):
        pass
每个内建类型都有一个唯一定义它的字符代码，如下：

字符	对应类型	备注
b	boolean	'b1'
i	signed integer	'i1', 'i2', 'i4', 'i8'
u	unsigned integer	'u1', 'u2' ,'u4' ,'u8'
f	floating-point	'f2', 'f4', 'f8'
c	complex floating-point	
m	timedelta64	表示两个时间之间的间隔
M	datetime64	日期时间类型
O	object	
S	(byte-)string	S3表示长度为3的字符串
U	Unicode	Unicode 字符串
V	void	
【例】

import numpy as np

a = np.dtype('b1')
print(a.type)  # <class 'numpy.bool_'>
print(a.itemsize)  # 1

a = np.dtype('i1')
print(a.type)  # <class 'numpy.int8'>
print(a.itemsize)  # 1
a = np.dtype('i2')
print(a.type)  # <class 'numpy.int16'>
print(a.itemsize)  # 2
a = np.dtype('i4')
print(a.type)  # <class 'numpy.int32'>
print(a.itemsize)  # 4
a = np.dtype('i8')
print(a.type)  # <class 'numpy.int64'>
print(a.itemsize)  # 8

a = np.dtype('u1')
print(a.type)  # <class 'numpy.uint8'>
print(a.itemsize)  # 1
a = np.dtype('u2')
print(a.type)  # <class 'numpy.uint16'>
print(a.itemsize)  # 2
a = np.dtype('u4')
print(a.type)  # <class 'numpy.uint32'>
print(a.itemsize)  # 4
a = np.dtype('u8')
print(a.type)  # <class 'numpy.uint64'>
print(a.itemsize)  # 8

a = np.dtype('f2')
print(a.type)  # <class 'numpy.float16'>
print(a.itemsize)  # 2
a = np.dtype('f4')
print(a.type)  # <class 'numpy.float32'>
print(a.itemsize)  # 4
a = np.dtype('f8')
print(a.type)  # <class 'numpy.float64'>
print(a.itemsize)  # 8

a = np.dtype('S')
print(a.type)  # <class 'numpy.bytes_'>
print(a.itemsize)  # 0
a = np.dtype('S3')
print(a.type)  # <class 'numpy.bytes_'>
print(a.itemsize)  # 3

a = np.dtype('U3')
print(a.type)  # <class 'numpy.str_'>
print(a.itemsize)  # 12
数据类型信息

Python 的浮点数通常是64位浮点数，几乎等同于 np.float64。

NumPy和Python整数类型的行为在整数溢出方面存在显着差异，与 NumPy 不同，Python 的int 是灵活的。这意味着Python整数可以扩展以容纳任何整数并且不会溢出。

Machine limits for integer types.

class iinfo(object):
    def __init__(self, int_type):
        pass
    def min(self):
        pass
    def max(self):
        pass
【例】

import numpy as np

ii16 = np.iinfo(np.int16)
print(ii16.min)  # -32768
print(ii16.max)  # 32767

ii32 = np.iinfo(np.int32)
print(ii32.min)  # -2147483648
print(ii32.max)  # 2147483647
Machine limits for floating point types.

class finfo(object):
    def _init(self, dtype):
【例】

import numpy as np

ff16 = np.finfo(np.float16)
print(ff16.bits)  # 16
print(ff16.min)  # -65500.0
print(ff16.max)  # 65500.0
print(ff16.eps)  # 0.000977

ff32 = np.finfo(np.float32)
print(ff32.bits)  # 32
print(ff32.min)  # -3.4028235e+38
print(ff32.max)  # 3.4028235e+38
print(ff32.eps)  # 1.1920929e-07

时间日期和时间增量

datetime64 基础

在 numpy 中，我们很方便的将字符串转换成时间日期类型 datetime64（datetime 已被 python 包含的日期时间库所占用）。

datatime64是带单位的日期时间类型，其单位如下：

日期单位	代码含义	时间单位	代码含义
Y	年	h	小时
M	月	m	分钟
W	周	s	秒
D	天	ms	毫秒
-	-	us	微秒
-	-	ns	纳秒
-	-	ps	皮秒
-	-	fs	飞秒
-	-	as	阿托秒
注意：

1秒 = 1000 毫秒（milliseconds）
1毫秒 = 1000 微秒（microseconds）
【例】从字符串创建 datetime64 类型时，默认情况下，numpy 会根据字符串自动选择对应的单位。

import numpy as np

a = np.datetime64('2020-03-01')
print(a, a.dtype)  # 2020-03-01 datetime64[D]

a = np.datetime64('2020-03')
print(a, a.dtype)  # 2020-03 datetime64[M]

a = np.datetime64('2020-03-08 20:00:05')
print(a, a.dtype)  # 2020-03-08T20:00:05 datetime64[s]

a = np.datetime64('2020-03-08 20:00')
print(a, a.dtype)  # 2020-03-08T20:00 datetime64[m]

a = np.datetime64('2020-03-08 20')
print(a, a.dtype)  # 2020-03-08T20 datetime64[h]
【例】从字符串创建 datetime64 类型时，可以强制指定使用的单位。

import numpy as np

a = np.datetime64('2020-03', 'D')
print(a, a.dtype)  # 2020-03-01 datetime64[D]

a = np.datetime64('2020-03', 'Y')
print(a, a.dtype)  # 2020 datetime64[Y]

print(np.datetime64('2020-03') == np.datetime64('2020-03-01'))  # True
print(np.datetime64('2020-03') == np.datetime64('2020-03-02'))  #False
由上例可以看出，2019-03 和 2019-03-01 所表示的其实是同一个时间。 事实上，如果两个 datetime64 对象具有不同的单位，它们可能仍然代表相同的时刻。并且从较大的单位（如月份）转换为较小的单位（如天数）是安全的。

【例】从字符串创建 datetime64 数组时，如果单位不统一，则一律转化成其中最小的单位。

import numpy as np

a = np.array(['2020-03', '2020-03-08', '2020-03-08 20:00'], dtype='datetime64')
print(a, a.dtype)
# ['2020-03-01T00:00' '2020-03-08T00:00' '2020-03-08T20:00'] datetime64[m]
【例】使用arange()创建 datetime64 数组，用于生成日期范围。

import numpy as np

a = np.arange('2020-08-01', '2020-08-10', dtype=np.datetime64)
print(a)
# ['2020-08-01' '2020-08-02' '2020-08-03' '2020-08-04' '2020-08-05'
#  '2020-08-06' '2020-08-07' '2020-08-08' '2020-08-09']
print(a.dtype)  # datetime64[D]

a = np.arange('2020-08-01 20:00', '2020-08-10', dtype=np.datetime64)
print(a)
# ['2020-08-01T20:00' '2020-08-01T20:01' '2020-08-01T20:02' ...
#  '2020-08-09T23:57' '2020-08-09T23:58' '2020-08-09T23:59']
print(a.dtype)  # datetime64[m]

a = np.arange('2020-05', '2020-12', dtype=np.datetime64)
print(a)
# ['2020-05' '2020-06' '2020-07' '2020-08' '2020-09' '2020-10' '2020-11']
print(a.dtype)  # datetime64[M]
datetime64 和 timedelta64 运算

【例】timedelta64 表示两个 datetime64 之间的差。timedelta64 也是带单位的，并且和相减运算中的两个 datetime64 中的较小的单位保持一致。

import numpy as np

a = np.datetime64('2020-03-08') - np.datetime64('2020-03-07')
b = np.datetime64('2020-03-08') - np.datetime64('202-03-07 08:00')
c = np.datetime64('2020-03-08') - np.datetime64('2020-03-07 23:00', 'D')

print(a, a.dtype)  # 1 days timedelta64[D]
print(b, b.dtype)  # 956178240 minutes timedelta64[m]
print(c, c.dtype)  # 1 days timedelta64[D]

a = np.datetime64('2020-03') + np.timedelta64(20, 'D')
b = np.datetime64('2020-06-15 00:00') + np.timedelta64(12, 'h')
print(a, a.dtype)  # 2020-03-21 datetime64[D]
print(b, b.dtype)  # 2020-06-15T12:00 datetime64[m]
【例】生成 timedelta64时，要注意年（'Y'）和月（'M'）这两个单位无法和其它单位进行运算（一年有几天？一个月有几个小时？这些都是不确定的）。

import numpy as np

a = np.timedelta64(1, 'Y')
b = np.timedelta64(a, 'M')
print(a)  # 1 years
print(b)  # 12 months

c = np.timedelta64(1, 'h')
d = np.timedelta64(c, 'm')
print(c)  # 1 hours
print(d)  # 60 minutes

print(np.timedelta64(a, 'D'))
# TypeError: Cannot cast NumPy timedelta64 scalar from metadata [Y] to [D] according to the rule 'same_kind'

print(np.timedelta64(b, 'D'))
# TypeError: Cannot cast NumPy timedelta64 scalar from metadata [M] to [D] according to the rule 'same_kind'
【例】timedelta64 的运算。

import numpy as np

a = np.timedelta64(1, 'Y')
b = np.timedelta64(6, 'M')
c = np.timedelta64(1, 'W')
d = np.timedelta64(1, 'D')
e = np.timedelta64(10, 'D')

print(a)  # 1 years
print(b)  # 6 months
print(a + b)  # 18 months
print(a - b)  # 6 months
print(2 * a)  # 2 years
print(a / b)  # 2.0
print(c / d)  # 7.0
print(c % e)  # 7 days
【例】numpy.datetime64 与 datetime.datetime 相互转换

import numpy as np
import datetime

dt = datetime.datetime(year=2020, month=6, day=1, hour=20, minute=5, second=30)
dt64 = np.datetime64(dt, 's')
print(dt64, dt64.dtype)
# 2020-06-01T20:05:30 datetime64[s]

dt2 = dt64.astype(datetime.datetime)
print(dt2, type(dt2))
# 2020-06-01 20:05:30 <class 'datetime.datetime'>
datetime64 的应用

为了允许在只有一周中某些日子有效的上下文中使用日期时间，NumPy包含一组“busday”（工作日）功能。

numpy.busday_offset(dates, offsets, roll='raise', weekmask='1111100', holidays=None, busdaycal=None, out=None) First adjusts the date to fall on a valid day according to the roll rule, then applies offsets to the given dates counted in valid days.
参数roll：{'raise', 'nat', 'forward', 'following', 'backward', 'preceding', 'modifiedfollowing', 'modifiedpreceding'}

'raise' means to raise an exception for an invalid day.
'nat' means to return a NaT (not-a-time) for an invalid day.
'forward' and 'following' mean to take the first valid day later in time.
'backward' and 'preceding' mean to take the first valid day earlier in time.
【例】将指定的偏移量应用于工作日，单位天（'D'）。计算下一个工作日，如果当前日期为非工作日，默认报错。可以指定 forward 或 backward 规则来避免报错。（一个是向前取第一个有效的工作日，一个是向后取第一个有效的工作日）

import numpy as np

# 2020-07-10 星期五
a = np.busday_offset('2020-07-10', offsets=1)
print(a)  # 2020-07-13

a = np.busday_offset('2020-07-11', offsets=1)
print(a)
# ValueError: Non-business day date in busday_offset

a = np.busday_offset('2020-07-11', offsets=0, roll='forward')
b = np.busday_offset('2020-07-11', offsets=0, roll='backward')
print(a)  # 2020-07-13
print(b)  # 2020-07-10

a = np.busday_offset('2020-07-11', offsets=1, roll='forward')
b = np.busday_offset('2020-07-11', offsets=1, roll='backward')
print(a)  # 2020-07-14
print(b)  # 2020-07-13
可以指定偏移量为 0 来获取当前日期向前或向后最近的工作日，当然，如果当前日期本身就是工作日，则直接返回当前日期。

numpy.is_busday(dates, weekmask='1111100', holidays=None, busdaycal=None, out=None) Calculates which of the given dates are valid days, and which are not.
【例】返回指定日期是否是工作日。

import numpy as np

# 2020-07-10 星期五
a = np.is_busday('2020-07-10')
b = np.is_busday('2020-07-11')
print(a)  # True
print(b)  # False
【例】统计一个 datetime64[D] 数组中的工作日天数。

import numpy as np

# 2020-07-10 星期五
begindates = np.datetime64('2020-07-10')
enddates = np.datetime64('2020-07-20')
a = np.arange(begindates, enddates, dtype='datetime64')
b = np.count_nonzero(np.is_busday(a))
print(a)
# ['2020-07-10' '2020-07-11' '2020-07-12' '2020-07-13' '2020-07-14'
#  '2020-07-15' '2020-07-16' '2020-07-17' '2020-07-18' '2020-07-19']
print(b)  # 6
【例】自定义周掩码值，即指定一周中哪些星期是工作日。

import numpy as np

# 2020-07-10 星期五
a = np.is_busday('2020-07-10', weekmask=[1, 1, 1, 1, 1, 0, 0])
b = np.is_busday('2020-07-10', weekmask=[1, 1, 1, 1, 0, 0, 1])
print(a)  # True
print(b)  # False
numpy.busday_count(begindates, enddates, weekmask='1111100', holidays=[], busdaycal=None, out=None)Counts the number of valid days between begindates and enddates, not including the day of enddates.
【例】返回两个日期之间的工作日数量。

import numpy as np

# 2020-07-10 星期五
begindates = np.datetime64('2020-07-10')
enddates = np.datetime64('2020-07-20')
a = np.busday_count(begindates, enddates)
b = np.busday_count(enddates, begindates)
print(a)  # 6
print(b)  # -6
参考图文


https://www.jianshu.com/p/336cd77d9914
https://www.cnblogs.com/gl1573/p/10549547.html#h2datetime64
https://www.numpy.org.cn/reference/arrays/datetime.html#%E6%97%A5%E6%9C%9F%E6%97%B6%E9%97%B4%E5%8D%95%E4%BD%8D