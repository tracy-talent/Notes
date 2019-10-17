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
  
* glorot_uniform_initializer(Xaiver初始化器，权重为0，方差为2/(n_in+n_out)的均匀分布或者高斯分布)是variable的默认initilizer

* tf.Tensor没有重载'=='运算符，使用tf.equal替代

* tf.metrics.accuracy()会返回2个常量acc和acc_update_op，并且自动创建两个局部变量total(正确的数目)和count(总数目)，acc直接返回total/count而acc_update_op会更新total和count再返回acc=total/count，注意使用前先初始化局部变量sess.run(tf.local_variables())

* 设置程序可用的cuda设备: `os.environ['CUDA_VISIBLE_DEVICES']='0,1,2,3'`或者命令行下`CUDA_VISIBLE_DEVICES=1 python example.py`

* tf.pad的"CONSTANT"模式paddings长度没有限制，"SYMMETRIC"模式paddings每一维度长度不超过原tensor的每一维大小，"REFLECT"模式paddings每一维度长度不超过原tensor每一维大小-1

* Last-layer activation and loss function combinations

  | **Problem type**                         | **Last-layer activation** | **Loss function**          |
  | ---------------------------------------- | ------------------------- | -------------------------- |
  | Binary classification                    | sigmoid                   | binary_crossentropy        |
  | Multi-class, single-label classification | softmax                   | categorical_crossentropy   |
  | Multi-class, multi-label classification  | sigmoid                   | binary_crossentropy        |
  | Regression to arbitrary values           | None                      | mse                        |
  | Regression to values between 0 and 1     | sigmoid                   | mse or binary_crossentropy |

* tf.keras.model中的verbose参数用于指定输出样式，verbose = 0 为不在标准输出流输出日志信息，verbose = 1 为输出进度条记录，verbose = 2 为每个epoch输出一行记录，例：model.fit(train_data, train_labels, epochs=10, batch=128, validation_data=(val_data, val_labels), verbose=1)

* underfit原因：1. 训练集小，数据不全面；2. 模型太简单不够强大，过正则化over-regularized；3. 训练轮数太少

* overfit原因：1. 训练轮数太多；2. 模型太复杂学习到的非泛化的细节太多。解决overfit：1. 在更大的数据集上训练; 2. 减少训练轮数；3.  正则化(weight regularization and dropout)，place constaints on the quantity and type of information the model can store, focus on the most prominent patterns to have a better chance of generalizing well；4. reduce the size of the model(reduce the capacity of network), i.e. the number of learnable parameters in the model (which is determined by the number of layers and the number of units per layer).
