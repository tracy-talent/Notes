<center><h1>Latex</h1></center>

## 参考文献

* 建一个ref.bib文件，将想要引用的文献的Bibtex添加进去，然后在.tex文件中通过如下方式引用：

```latex
\begin{document}
%设置参考文献类型，标准的为plain
\bibliographystyle{plain}

%引用方式
\cite{文献名}

%放在文末生成参考文献
\bibliography{ref}   
\end{document}
```

