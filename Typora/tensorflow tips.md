<h1>tensorflow tips</h1>
* 读取tf.Variable的值而不执行任何与该variable相关的操作

  ```python
  tf.reset_default_graph()
  with tf.Session() as sess:
      v = tf.get_variable('v', shape=(), initializer=tf.zeros_initializer())
      tf.global_variables_initializer().run()
      v.assign_add(1).eval()
      print(v.read_value().eval())
  ```

* op.run()默默执行操作返回None，可以使用

  ```python
  tf.reset_default_graph()
  with tf.Session() as sess:
      v = tf.get_variable('v', shape=(), initializer=tf.zeros_initializer())
      sess.run(tf.global_variables_initializer())  # 或者: tf.global_variables_initializer().run()
      assignment = v.assign_add(1)  # 定义加1操作，返回tensor
      print(assignment.eval())  # 输出：1
      print(assignment.op.run()) # 输出: None，加1操作已在背后执行
      print(v.read_value().eval()) # 输出: 2, 读取assignment中的值不执行操作
      print(sess.run(assignment)) # 输出: 3
  ```

* tf隐式地为每个操作添加到默认的tf.get_default_graph中，要在单进程中使用隔离的多个graph，那么tf.Graph必须注册成default graph才可以定义属于自己的operations，否则会报错，不同图中的operations可以同名

  ```python
  with tf.Graph.as_default() as g:
      a = tf.constant(1)
      b = tf.constant(2)
      c = a + b
  print(g, g.get_operations())  
  # 输出：<tensorflow.python.framework.ops.Graph at 0x7f8f78d33b00>
  # [<tf.Operation 'Const' type=Const>, <tf.Operation 'Const_1' type=Const>, <tf.Operation 'add' type=Add>]
  print(tf.get_default_graph(), tf.get_default_graph().get_operations())
  # 输出: <tensorflow.python.framework.ops.Graph at 0x7f8f78a032b0>
  # []
  ```

  由输出可以看出g和tf.get_defalut_graph()显然是不同的两个图

