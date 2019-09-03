<center><h1>NLP tips</h1></center>

## WikiExtractor.py用法

> 用与从wik数据集中提取出便于使用数据

1. git clone https://github.com/attardi/wikiextractor.git
2. cd wikiextractor
3. python setup.py install

```shell
WikiExtractor.py -o wiki_zh zhwiki-latest-pages-articles.xml.bz2
# wiki的数据集将会划分到wiki_zh目录下的各个子目录中
```



## opencc命令

>  opencc命令用于中文简繁之间的转换

* 句子简繁转换

```shell
echo '歐幾里得 西元前三世紀的希臘數學家' | opencc -c t2s
echo '欧几里得 西元前三世纪的希腊数学家' | opencc -c s2t
# 其中t2s是繁体转简体，s2t是简体转繁体
```

* 文件简繁转换

```shell
opencc -i wiki.zh.txt -o wiki.zh_simple.txt -c t2s.json
```