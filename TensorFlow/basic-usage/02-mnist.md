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

相对应的MNIST数据集的**标签**是介于0到9的数字，用来描述给定图片里表示的数字。为了用于这个教程，我们使标签数据是"one-hot vectors"。 一个one-hot向量除了某一位的数字是1以外其余各维度数字都是0。所以在此教程中，数字n将表示成一个只有在第n维度（从0开始）数字为1的**10维向量**(<font color=red>Q:为什么是10维向量？A:因为标签总共有10个</font>)。比如，标签0将表示成([1,0,0,0,0,0,0,0,0,0,0])。因此， mnist.train.labels 是一个 [60000, 10] 的数字矩阵。 
