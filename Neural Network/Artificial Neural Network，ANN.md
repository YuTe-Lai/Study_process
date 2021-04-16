# 類神經網路路 Artificial Neural Network，ANN
類神經網路是透過電腦來模擬⼤腦神經運作的⼀種機器學習方式。大腦內的神經網路是由神經元及突觸所組成，由其他神經元經節點輸入訊號，這時節點會決定要抑制或刺激，決定好後再
把這個訊號傳到下⼀個神經元。其中，神經元具有階層性，階層之間的神經元有著不同強度的鍵結，⽽類神經網路就是依這個概念發展而成的。<br>
 <img src="https://raw.githubusercontent.com/YuTe-Lai/Study_process/master/img/NN_ANN2.png"  width="800" height="280"><br><br>

## 多層神經網路架構
多層神經網路(multi-layer neural networks)可分為輸入層、隱藏層(多層)和輸出層。只要超過⼀層隱藏層的神經網路，通常會被泛稱為深度神經網路(Deep Neural Network，DNN)。

 <img src="https://raw.githubusercontent.com/YuTe-Lai/Study_process/master/img/NN_ANN_3.png"  width="655" height="280"><br>
 以下圖為例，其中黑色線條代表權重（共12個權重），綠色方格為偏移值，他們指向 Activation function。<br>
 多層神經網路的算式：（ 輸入層 x 權重 ）＋ 偏移值，接著傳給 Activation function 運算。<br>
  <img src="https://raw.githubusercontent.com/YuTe-Lai/Study_process/master/img/NN_ANN4.png"  width="733" height="284"><br>
  
## 神經元
神經元為 Neural Network的最小單元。如果希望結果更好，則必須加入多個神經元，建構多層神經網路。<br>
其包含：輸入值、權重、偏移值、激活函數。
 <img src="https://raw.githubusercontent.com/YuTe-Lai/Study_process/master/img/NN_ANN1.png"  width="933" height="322"><br>
- 權重：
表示某個輸入值的重要性。
- 偏移值：
誤差。
- 激活函數：
非線性轉換函數，以增加模型對於非線性規則的學習能力。將輸入值、權重、偏移值運算後的值做非線性的轉換，成為神經元的最終輸出。例如：大於某個值就輸出1，否則輸出-1。
<br>

## 激活函數
負責處理 xW + b，成為neuron 的最終輸出。
- Step function
- Sigmoid function
- Tanh (hyperbolic tangent) function
- ReLU(rectified linear unit) function
- Leaky function•Identity function
- Softmaxfunction


### Step function
```python
import numpy as np
import matplotlib.pyplot as plt
def step_function(x):
  return np.where(x<=0, 0, 1)
x=np.linspace(-5,5)
y=step_function(x)
plt.plot(x,y)
plt.show()
```
<img src="https://raw.githubusercontent.com/YuTe-Lai/Study_process/master/img/NN_ANN_StepFunction.png"  width="400" height="300"><br>


### Sigmoid function
```python
import numpy as np
import matplotlib.pyplot as plt
def sigmoid_function(x):
  return 1/(1+np.exp(-x))
x=np.linspace(-5,5)
y=sigmoid_function(x)
plt.plot(x,y)
plt.show()
```
<img src="https://raw.githubusercontent.com/YuTe-Lai/Study_process/master/img/NN_ANN_SigmoidFunction.png"  width="400" height="300"><br>


### Tanh function
```python
import numpy as np
import matplotlib.pyplot as plt
def tanh_function(x):
  return (np.exp(x)-np.exp(-x))/(np.exp(x)+np.exp(-x))
x=np.linspace(-5,5)
y=tanh_function(x)
plt.plot(x,y)
plt.show()
```
<img src="https://raw.githubusercontent.com/YuTe-Lai/Study_process/master/img/NN_ANN_TanhFunction.png"  width="400" height="300"><br>


### ReLU function
```python
import numpy as np
import matplotlib.pyplot as plt
def step_function(x):
  return np.where(x<=0, 0, x)
x=np.linspace(-5,5)
y=step_function(x)
plt.plot(x,y)
plt.show()
```
<img src="https://raw.githubusercontent.com/YuTe-Lai/Study_process/master/img/NN_ANN_ReluFunction.png"  width="400" height="300"><br>


### Leaky ReLU function
```python
import numpy as np
import matplotlib.pyplot as plt
def step_function(x):
  return np.where(x<=0, 0.01*x, x)
x=np.linspace(-5,5)
y=step_function(x)
plt.plot(x,y)
plt.show()
```
<img src="https://raw.githubusercontent.com/YuTe-Lai/Study_process/master/img/NN_ANN_LeakyReLufunction.png"  width="400" height="300"><br>


### Identity function
```python
import numpy as np
import matplotlib.pyplot as plt
x = np.linspace(-5,5)
y = x
plt.plot(x,y)
plt.show()
```
<img src="https://raw.githubusercontent.com/YuTe-Lai/Study_process/master/img/NN_ANN_IdentityFunction.png"  width="400" height="300"><br>
