<center><h1>python tips</h1></center>
### logging模块的使用

```python
import logging
import sys

program = os.path.basename(sys.argv[0])
logger = logging.getLogger(program)

# 设置输出的日志级别
# logging.root.setLevel(level=logging.INFO)
logger.setLevel(level=logging.INFO) 
# 设置日志输出内容：时间%Y-%m-%d %H:%M:%S，日志级别INFO,WARNING,ERROR，日志信息
formatter = logging.Formatter(fmt='%(asctime)s - %(levelname)s - %(name)s - %(message)s',
                   datefmt='%Y-%m-%d %H:%M:%S')
chlr = logging.StreamHandler()
chlr.setFormatter(formatter)
logger.addHandler(chlr)

# 设置日志输出文件
log_file_path = "./run.log"
if os.path.exists(log_file_path): 
    os.remove(log_file_path)
fhlr = logging.FileHandler(log_file_path)
fhlr.setFormatter(formatter)
logger.addHandler(fhlr)

# 输出日志信息内容
logger.info("running %s" % ' '.join(sys.argv))
```

也可以用logging设置

```python
# 设置日志输出内容：时间%Y-%m-%d %H:%M:%S，日志级别INFO,WARNING,ERROR，日志信息
logging.basicConfig(format='%(asctime)s - %(levelname)s - %(name)s - %(message)s',
                   datefmt='%Y-%m-%d %H:%M:%S',
                   level=logging.INFO)
# 设置输出的日志级别
logging.root.setLevel(level=logging.INFO)
```



### format格式化输出字典

```
d = {'world':3.0, 'python':3.6}
print('hello {world:0.3f}'.format(**d))  # 输出value: 在格式化字符串{}中加入字典中的key，字典传入加上**
print('hello {} {}'.format(*d)) # 输出key
```



### 装饰器

1. 不带参数的装饰器等价于wrapper(wrapped)(\*args, \*\*kargs) ，关于functools中的wraps装饰可参考：[wraps](https://segmentfault.com/a/1190000009398663)，主要用于交换装饰函数和被装饰函数之间的\_\_doc\_\_、\_\_name\_\_等属性，不交换则wrapped的这些属性都是wrapper装饰之后的wrapper_func的属性

```python
from functools import wraps

def wrapper(f=None):
    @wraps(f)
    def wrapper_func(*args, **kargs):
        return f(*args, **kargs)
    return wrapper_func

@wrapper
def wrapped(*arg, **kargs):
    pass
```

2. 带参数的装饰器等价于wrapper(start_log="test")(wrapped)(\*args, \*\*kargs)

```python
from functools import wraps, partial

def wrapper(f=None, start_log=None):
    if f is None:
        return partial(wrapper, start_log=start_log)
    @wraps(f)
    def wrapper_func(*args, **kargs):
        if start_log is not None:
            print(start_log)
        return f(*args, **kargs)
    return wrapper_func

@wrapper(start_log="test")
def wrapped(*arg, **kargs):
    pass
```



### 正则表达式re

#### 通配符

* \s是指空白，包括空格、换行、tab缩进等所有的空白，而\S刚好相反。例如，[\s\S]\*表示完全通配

#### 反向引用

单独斜杠的 \1 ， \2 就是反向引用了。

* '\1' 匹配的是 所获取的第1个()匹配的引用。例如，r'(\d)\1' 匹配两个连续数字字符。如33aa 中的33
* '\2' 匹配的是 所获取的第2个()匹配的引用。

例如，r'(\d)(a)\1' 匹配第一是数字第二是字符a,第三\1必须匹配第一个一样的数字重复一次，也就是被引用一次。如9a9 被匹配，但9a8不会被匹配，因为第三位的\1必须是9才可以，

r'(\d)(a)\2' 匹配第一个是一个数字，第二个是a，第三个\2必须是第二组 () 中匹配一样的，如，8aa被匹配，但8ab，7a7不会被匹配，第三位必须是第二组字符的复制版，也是就引用第二组正则的匹配内容。

#### lookaround

Lookaround，具体包括 1) Lookahead 和 2) Lookbehind，分别对应了前向限制和后向限制，不是全部正则表达式（Regex）的引擎实现中都支持一类语法，但是python是支持的

* lookahead具体方式是'str(?=pattern)'表示str后面必须是pattern(注意进行查找时只会返回满足条件的str，不会连同返回pattern)，而'str(?!pattern)'表示str后面必须不是pattern
* lookbehind具体方式是'(?<=pattern)str'表示str前面必须是pattern，而'(?<!pattern)str'表示str前面必须不是pattern

```
x = '(?<=x)hello(?=x)'
p = re.compile(x)
p.findall('dxhelloxs')  # 输出['hello']
```


