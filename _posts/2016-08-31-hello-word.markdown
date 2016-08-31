---
published: true
title: 聊聊神经网络——神经网络模型、训练、实现
layout: post
---
## 模型定义

假设输入层为N维向量，输出层为分别属于M个类别的概率，则模型图为：

<p align="center">
<img src="https://github.com/ybbaigo/seven-blue/blob/master/deep-learning/nn/resoures/nn_summary.png?raw=true"/>
</p>

具体模型公式为：

<p align="left">
<img src="https://github.com/ybbaigo/seven-blue/blob/master/deep-learning/nn/resoures/model_1.png?raw=true"/>
</p>

<p align="left">
<img src="https://github.com/ybbaigo/seven-blue/blob/master/deep-learning/nn/resoures/model_2.png?raw=true"/>
</p>

<p align="left">
<img src="https://github.com/ybbaigo/seven-blue/blob/master/deep-learning/nn/resoures/model_3.png?raw=true"/>
</p>

<p align="left">
<img src="https://github.com/ybbaigo/seven-blue/blob/master/deep-learning/nn/resoures/model_4.png?raw=true"/>
</p>

Loss函数为：

<p align="left">
<img src="https://github.com/ybbaigo/seven-blue/blob/master/deep-learning/nn/resoures/loss_1.png?raw=true"/>
</p>


## 模型训练

模型训练采用**Backpropagation**算法，其中**Backwards**过程采用**Mini-batch gradient descent**算法：

``` python
# Vanilla Minibatch Gradient Descent

while True:
    data_batch = sample_training_data(data, 256) # sample 256 examples
    weights_grad = evaluate_gradient(loss_fun, data_batch, weights)
    weights += - step_size * weights_grad # perform parameter update
```

训练过程中涉及到的偏导计算结果如下：

<p align="left">
<img src="https://github.com/ybbaigo/seven-blue/blob/master/deep-learning/nn/resoures/dev_1.png?raw=true"/>
</p>

<p align="left">
<img src="https://github.com/ybbaigo/seven-blue/blob/master/deep-learning/nn/resoures/dev_2.png?raw=true"/>
</p>

<p align="left">
<img src="https://github.com/ybbaigo/seven-blue/blob/master/deep-learning/nn/resoures/dev_3.png?raw=true"/>
</p>

<p align="left">
<img src="https://github.com/ybbaigo/seven-blue/blob/master/deep-learning/nn/resoures/dev_4.png?raw=true"/>
</p>

<p align="left">
<img src="https://github.com/ybbaigo/seven-blue/blob/master/deep-learning/nn/resoures/dev_5.png?raw=true"/>
</p>

## 代码实现

<pre>
<a href="https://github.com/ybbaigo/seven-blue/blob/master/deep-learning/nn/nn.ipynb">https://github.com/ybbaigo/seven-blue/blob/master/deep-learning/nn/nn.ipynb</a>
</pre>

## 参考资料

* https://mattmazur.com/2015/03/17/a-step-by-step-backpropagation-example/
* http://www.wildml.com/2015/09/implementing-a-neural-network-from-scratch/
* http://math.stackexchange.com/questions/945871/derivative-of-softmax-loss-function
* http://cs231n.github.io/optimization-1/
* http://neuralnetworksanddeeplearning.com/chap2.html