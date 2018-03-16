[mnist](http://www.tensorfly.cn/tfdoc/tutorials/overview.html)
### mnist 数据下载
下载[input_data.py](https://tensorflow.googlesource.com/tensorflow/+/master/tensorflow/examples/tutorials/mnist/input_data.py)，</br>
[input_data.py的使用](http://blog.csdn.net/lwplwf/article/details/54896959),</br>
新建get_input_data.py跟input_data.py放在同一个目录下，
```
import input_data
mnist = input_data.read_data_sets('data/', one_hot=True)
print "type of mnist is %s" % type(mnist)
print "number of train data is %d" % mnist.train.num_examples
print "number of test data is %d" % mnist.test.num_examples
```
执行python get_input_data.py, 输出：
```
Extracting data/train-images-idx3-ubyte.gz
Extracting data/train-labels-idx1-ubyte.gz
Extracting data/t10k-images-idx3-ubyte.gz
Extracting data/t10k-labels-idx1-ubyte.gz
type of mnist is <class 'input_data.DataSets'>
number of train data is 55000
number of test data is 10000
```
Q:训练数据跟测试数据的区别是什么？
A：在机器学习模型设计时必须有一个单独的**测试数据集**不用于训练而是用来评估这个模型的性能，从而更加容易把设计的模型推广到其他数据集上（泛化）。
### 数据集详情
每一个MNIST数据单元有两部分组成：**一张包含手写数字的图片和一个对应的标签**。我们把这些图片设为“xs”，把这些标签设为“ys，”。
训练数据集和测试数据集都包含xs和ys，比如训练数据集的图片是 mnist.train.images ，训练数据集的标签是 mnist.train.labels。
我们把这个数组展开成一个向量，长度是 **28x28 = 784**。。从这个角度来看，MNIST数据集的图片就是在**784维向量空间里面的点**, 并且拥有比较复杂的结构。

相对应的MNIST数据集的**标签**是介于0到9的数字，用来描述给定图片里表示的数字。为了用于这个教程，我们使标签数据是"one-hot vectors"。 一个one-hot向量除了某一位的数字是1以外其余各维度数字都是0。所以在此教程中，数字n将表示成一个只有在第n维度（从0开始）数字为1的**10维向量**(<font color=#ff0000>Q:为什么是10维向量？A:因为标签总共有10个</font>)。比如，标签0将表示成([1,0,0,0,0,0,0,0,0,0,0])。因此， mnist.train.labels 是一个 [60000, 10] 的数字矩阵。 
### Softmax回归介绍 
softmax模型可以用来给不同的对象分配概率。</br>
softmax回归（softmax regression）分两步：第一步</br>
为了得到一张给定图片属于某个特定数字类的证据（evidence），我们对图片像素值进行加权求和。如果这个像素具有很强的证据说明这张图片不属于该类，那么相应的权值为负数，相反如果这个像素拥有有利的证据支持这张图片属于这个类，那么权值是正数。
我们也需要加入一个额外的偏置量（bias），因为输入往往会带有一些无关的干扰量。因此对于给定的输入图片 x 它代表的是数字 i 的证据可以表示为
![](http://www.tensorfly.cn/tfdoc/images/mnist1.png)</br>
其中![](http://www.tensorfly.cn/tfdoc/images/mnist2.png)代表权重， ![](http://www.tensorfly.cn/tfdoc/images/mnist3.png)代表数字 i 类的偏置量，j 代表给定图片 x 的像素索引用于像素求和。然后用softmax函数可以把这些证据转换成概率 y：</br>
![](http://www.tensorfly.cn/tfdoc/images/mnist4.png)</br>

但是更多的时候把softmax模型函数定义为前一种形式：把输入值当成幂指数求值，再正则化这些结果值。这个幂运算表示，更大的证据对应更大的假设模型（hypothesis）里面的乘数权重值。反之，拥有更少的证据意味着在假设模型里面拥有更小的乘数系数。假设模型里的权值不可以是0值或者负值。Softmax然后会正则化这些权重值，使它们的总和等于1，以此构造一个有效的概率分布。（更多的关于Softmax函数的信息，可以参考Michael Nieslen的书里面的这个部分，其中有关于softmax的可交互式的可视化解释。）</br>
我们也可以用向量表示这个计算过程：用矩阵乘法和向量相加。这有助于提高计算效率。（也是一种更有效的思考方式）</br>
![](http://www.tensorfly.cn/tfdoc/images/softmax-regression-vectorequation.png)</br>
### 实现回归模型 
为了用python实现高效的数值计算，我们通常会使用函数库，比如NumPy，会把类似矩阵乘法这样的复杂运算使用其他外部语言实现。不幸的是，从外部计算切换回Python的每一个操作，仍然是一个很大的开销。如果你用GPU来进行外部计算，这样的开销会更大。用分布式的计算方式，也会花费更多的资源用来传输数据。
TensorFlow也把复杂的计算放在python之外完成，但是为了避免前面说的那些开销，它做了进一步完善。**Tensorflow不单独地运行单一的复杂计算，而是让我们可以先用图描述一系列可交互的计算操作，然后全部一起在Python之外运行**。（这样类似的运行方式，可以在不少的机器学习库中看到。）
```
import tensorflow as tf

#每一张图展平成784维的向量。我们用2维的浮点数张量来表示这些图，这个张量的形状是[None，784 ]。
#（这里的None表示此张量的第一个维度可以是任何长度的。）
x = tf.placeholder("float", [None, 784])

#权重值和偏置量,我们赋予tf.Variable不同的初值来创建不同的Variable：在这里，
#我们都用全为零的张量来初始化W和b。因为我们要学习W和b的值，它们的初值可以随意设置。
W = tf.Variable(tf.zeros([784,10]))
b = tf.Variable(tf.zeros([10]))

# 实现我们的模型
y = tf.nn.softmax(tf.matmul(x,W) + b)
```
### 训练模型 
我们通常定义指标来表示一个模型是坏的，这个指标称为**成本（cost）或损失（loss）**，然后尽量最小化这个指标</br>
一个非常常见的，非常漂亮的成本函数是**“交叉熵”（cross-entropy）**。交叉熵产生于信息论里面的信息压缩编码技术，但是它后来演变成为从博弈论到机器学习等其他领域里的重要技术手段。它的定义如下：</br>
![交叉熵](http://www.tensorfly.cn/tfdoc/images/mnist10.png)</br>
**y 是我们预测的概率分布, y' 是实际的分布（我们输入的one-hot vector)。比较粗糙的理解是，交叉熵是用来衡量我们的预测用于描述真相的低效性。**</br>，关于[交叉熵](http://colah.github.io/posts/2015-09-Visual-Information/).</br>
为了计算交叉熵，我们首先需要添加一个新的占位符用于输入正确值：
```
y_ = tf.placeholder("float", [None,10])
```
然后计算交叉熵:
```
cross_entropy = -tf.reduce_sum(y_*tf.log(y))
```
首先，用 tf.log 计算 y 的每个元素的对数。接下来，我们把 y_ 的每一个元素和 tf.log(y_) 的对应元素相乘。最后，用 tf.reduce_sum 计算张量的所有元素的总和。用TensorFlow来训练它是非常容易的。因为TensorFlow拥有一张描述你各个计算单元的图，它可以自动地使用反向传播算法(backpropagation algorithm)来有效地确定你的变量是如何影响你想要最小化的那个成本值的。然后，TensorFlow会用你选择的优化算法来不断地修改变量以降低成本。
```
train_step = tf.train.GradientDescentOptimizer(0.01).minimize(cross_entropy)
```
在这里，我们要求TensorFlow用梯度下降算法（gradient descent algorithm）以0.01的学习速率最小化交叉熵。梯度下降算法（gradient descent algorithm）是一个简单的学习过程，TensorFlow只需将每个变量一点点地往使成本不断降低的方向移动。当然TensorFlow也提供了其他许多优化算法：只要简单地调整一行代码就可以使用其他的算法。
现在，我们已经设置好了我们的模型。在运行计算之前，我们需要添加一个操作来初始化我们创建的变量：
```
init = tf.initialize_all_variables()
```
现在我们可以在一个Session里面启动我们的模型，并且初始化变量：
```
sess = tf.Session()
sess.run(init)
```
然后开始训练模型，这里我们让模型循环训练1000次！
```
for i in range(1000):
  batch_xs, batch_ys = mnist.train.next_batch(100)
  sess.run(train_step, feed_dict={x: batch_xs, y_: batch_ys})
```
该循环的每个步骤中，我们都会随机抓取训练数据中的100个批处理数据点，然后我们用这些数据点作为参数替换之前的占位符来运行train_step。

使用一小部分的随机数据来进行训练被称为随机训练（stochastic training）- 在这里更确切的说是随机梯度下降训练。在理想情况下，我们希望用我们所有的数据来进行每一步的训练，因为这能给我们更好的训练结果，但显然这需要很大的计算开销。所以，每一次训练我们可以使用不同的数据子集，这样做既可以减少计算开销，又可以最大化地学习到数据集的总体特性。
### 评估我们的模型 
首先让我们找出那些预测正确的标签。**tf.argmax** 是一个非常有用的函数，它能给出某个tensor对象在某一维上的其数据最大值所在的索引值。由于标签向量是由0,1组成，因此最大值1所在的索引位置就是类别标签，比如tf.argmax(y,1)返回的是模型对于任一输入x预测到的标签值，而 tf.argmax(y_,1) 代表正确的标签，我们可以用 tf.equal 来检测我们的预测是否真实标签匹配(索引位置一样表示匹配)。
```
correct_prediction = tf.equal(tf.argmax(y,1), tf.argmax(y_,1))
```
这行代码会给我们一组布尔值。为了确定正确预测项的比例，我们可以把布尔值转换成浮点数，然后取平均值。例如，[True, False, True, True] 会变成 [1,0,1,1] ，取平均值后得到 0.75.
```
accuracy = tf.reduce_mean(tf.cast(correct_prediction, "float"))
```
最后，我们计算所学习到的模型在测试数据集上面的正确率。
```
print sess.run(accuracy, feed_dict={x: mnist.test.images, y_: mnist.test.labels})
```
这个最终结果值应该大约是91%。

这个结果好吗？嗯，并不太好。事实上，这个结果是很差的。这是因为我们仅仅使用了一个非常简单的模型。不过，做一些小小的改进，我们就可以得到97％的正确率。最好的模型甚至可以获得超过99.7％的准确率！（想了解更多信息，可以看看这个关于各种模型的性能对比列表。)

比结果更重要的是，我们从这个模型中学习到的设计思想。不过，如果你仍然对这里的结果有点失望，可以查看下一个教程，在那里你可以学习如何用FensorFlow构建更加复杂的模型以获得更好的性能！
### Q & A
- 

