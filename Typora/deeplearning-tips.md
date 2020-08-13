# DeeepLearning Tips

## optimizers

optimizer的详细理解可参考[吴恩达深度学习课程笔记](http://www.ai-start.com/dl2017/html/lesson2-week2.html#header-n245)

* Adam(adaptive moment estimation)适用于解决大噪声和稀疏梯度的问题。Adam会累积历史一阶和二阶梯度的指数加权平均值，所以稀疏梯度的一阶值不会太小，并且因为遇上稀疏梯度时梯度二阶矩很小，意味着梯度更新值的分母很小，所以梯度更新值会更大，所以反而能加大稀疏特征对模型的影响。
* Adam梯度对角缩放具有不变性：我们如果用因子 c 重缩放（rescaling）梯度 g，相当于用因子 c 重缩放$\hat{m_t}$和用因子 $c^2$ 缩放$\hat{v_t}$，那么梯度更新的有效步长$(c \cdot \hat{m_t} )/(\sqrt{c^2 \cdot \hat{v_t}})=\hat{m_t}/\sqrt{\hat{v_t}}$保持不变
* Adagrad和RMSprop(root mean square propogation)也包含梯度二阶矩，因此也能解决稀疏梯度和噪声的非稳态问题。但是Adagrad的梯度二阶矩没有衰减因子，二阶梯度值越来越大，可能导致在未到达最优值之前就停止更新了。
* NAG(Nesterov accelerated gradient)相比momentum梯度更新的方式，NAG在计算参数梯度之前会在历史梯度的方向上往前探一小步，在此基础计算出的梯度更有可能朝着最优解的方向。[参考配图理解Nesterove](https://blog.csdn.net/tsyccnh/article/details/76673073)

