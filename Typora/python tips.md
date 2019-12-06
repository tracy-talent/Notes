<center><h1>python tips</h1></center>
### logging模块的使用

```python
import logging
import sys

program = os.path.basename(sys.argv[0])
logger = logging.getLogger(program)

# 设置日志输出内容：时间%Y-%m-%d %H:%M:%S，日志级别INFO,WARNING,ERROR，日志信息
logging.basicConfig(format='%(asctime)s: %(levelname)s: %(message)s')
# 设置输出的日志级别
logging.root.setLevel(level=logging.INFO)
# 输出日志信息内容
logger.info("running %s" % ' '.join(sys.argv))
```

### format格式化输出字典

```
d = {'world':3.0, 'python':3.6}
print('hello {world:0.3f}'.format(**d))  # 输出value: 在格式化字符串{}中加入字典中的key，字典传入加上**
print('hello {} {}'.format(*d)) # 输出key
```

### 正则表达式re

#### 通配符

* \s是指空白，包括空格、换行、tab缩进等所有的空白，而\S刚好相反。例如，[\s\S]\*表示完全通配

#### lookaround

Lookaround，具体包括 1) Lookahead 和 2) Lookbehind，分别对应了前向限制和后向限制，不是全部正则表达式（Regex）的引擎实现中都支持一类语法，但是python是支持的

* lookahead具体方式是'str(?=pattern)'表示str后面必须是pattern(注意进行查找时只会返回满足条件的str，不会连同返回pattern)，而'str(?!pattern)'表示str后面必须不是pattern
* lookbehind具体方式是'(?<=pattern)str'表示str前面必须是pattern，而'(?<!pattern)str'表示str前面必须不是pattern

```
x = '(?<=x)hello(?=x)'
p = re.compile(x)
p.findall('dxhelloxs')  # 输出['hello']
```









