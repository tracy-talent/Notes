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

* tf.keras.losses.SparseCategoricalCrossentropy(from_logits=False, reduction=tf.keras.losses.Reduction.AUTO)，默认from_logits为False即认为y_pred是经过softmax或者sigmoid等激活函数处理过的0\~1概率值(通过查看源码得知这种情况tensorflow内部会对y_pred的值两极化处理，设置阈值epsilon=1e-7，小于epsilon的等于epsilon，而大于1-epsilon的等于1-epsilon，然后取log，个人猜测这么做是为了使log数值计算更平滑，避免log(x->0.)的情况)，如果不是需要修改参数from_logits=True。而reduction参数默认是AUTO，即根据具体使用情况选择是NONE还是SUM_OVER_BATCH_SIZE.

* batch normalization(BN)是针对batch的每个特征列求均值方差的normalization，而layer normalization(LN)是针对一个样本内所有特征求均值方差然后normalize所有的特，与batch无关，实践表明LN比BN更适用于RNN，而BN比LN更适用于CNN 。由于深度网络参数训练时内部存在**协方差偏移（Internal Covariate Shift）**现象：深度网络内部数据分布在训练过程中发生变化的现象。使得神经网络难以学到数据真正的分布，使用normalization可以加速参数训练使得模型收敛，并且可以避免梯度消失和梯度爆炸。

* tf.shape获取动态维度(返回结果为tensor，graph mode下可以使用tf.print打印)，tf.get_shape获取静态维度

* tf.function转换graph mode时，转换代码内部不能直接使用v = tf.Variable创建变量，而要判断if v is None再创建，否则tensorflow的Autograph转换成图模式的代码时会报tried to create variables on non-first call，因为会重复创建同名variable

* [tf.compat.v1.train.Supervisor](https://www.tensorflow.org/api_docs/python/tf/compat/v1/train/Supervisor)方法介绍：sv = Supervisor(logdir='/tmp/mydir')，Within the `with sv.managed_session()` block all variables in the graph have been initialized. In addition, a few services have been started to checkpoint the model and add summaries to the event log. If the program crashes and is restarted, the managed session automatically reinitialize variables from the most recent checkpoint.提示：This class is deprecated. Please use [`tf.compat.v1.train.MonitoredTrainingSession`](https://www.tensorflow.org/api_docs/python/tf/compat/v1/train/MonitoredTrainingSession) instead.
