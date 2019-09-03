<center><h1>Python2  diffs Python3</h1></center>

## 字典

* python2里面dict.keys()返回静态列表，而python3里面dict.keys()返回键值的动态视图dict_keys(keys)，同样都可以读，但是涉及到修改的操作比如调用sort则需要将动态视图转换成静态列表(可以使用sorted排序而不需要转换)。

```python
uniq = {"1":"liu","2":"jian"}
print(uniq.keys())

output>dict_keys(['1', '2'])
#python3的排序
keys = list(uniq.keys())
keys.sort()
#or
keys = sorted(uniq.keys())
```

* sort by key ==OR== sort by value

```python
#sort by key
keys = sorted(uniq.items(), key=lambda d:d[0], reverse=False)
#sort by value
values = sorted(uniq.items(), key=lambda d:d[1], reverse=False)
```



## 版本判别(six模块)

```python
if six.PY3:
    pass
elif six.PY2:
    pass
```



## 生成python doc

* 使用pydoc命令

```
# 生成指定模块的pydoc,并将doc写到module.html中(module不必加.py)
python -m pydoc -w module
# 为python所有模块建一个可查询doc的server,使用-p指定一个端口号在浏览器中打开即可查看
python -m pydoc -p portno
```

