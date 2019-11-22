<center><h1>latex tips</h1></center>
## 公式

* 多行公式居中

  ```latex
  \begin{gather*}
  \end{gather*}
  ```

* 多行公式共用一个标签

  ```latex
  \begin{equation}
  \begin{split}
  \end{split}\tag{1.1}
  \end{equation}
  ```

* 多行公式

  ```latex
  % 等号前加&可用于对齐公式
  \begin{align*}
  \end{align*} 
  % 普通多行
  \begin(equation*|eqnarray)
  \end{equation*|eqnarray}
  ```

  



