<center><h1>python tips</h1></center>

## logging模块的使用

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







