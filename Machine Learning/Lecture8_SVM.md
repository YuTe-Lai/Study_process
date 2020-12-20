# 支撐向量機 SVM
 SVM是一種監督式學習的模型，其用於分類與迴歸分析中分析資料的演算法。想找到線性分類器中的最佳分界線，必須先找出離另一組資料最近的邊緣資料點，因為最佳分類線就是由這些邊緣資料點所支撐，所以他們被稱為支撐向量。<br>
  <img src="https://github.com/YuTe-Lai/Study_process/blob/master/Machine%20Learning/img/Lecture8_SVM_margin.png?raw=true" alt="R"  width="777" height="363"><br>
- 邊界較大的推論錯誤率小於邊界較小者，因為邊界小的話，那任意微小的變動都會影起顯著的影響。
<br>

## 非線性問題 Kernel method
在原始空間不好區分的資料（無法線性區分），可以用一個非線性的映射函式，將這些資料轉換到另一個空間（特徵空間），或許會比較好區分（可以線性區分）。<br>
  <img src="https://github.com/YuTe-Lai/Study_process/blob/master/Machine%20Learning/img/Lecture8_SVM_unlinear.png?raw=true" alt="R"  width="888" height="263"><br>
- 特徵空間不一定是更高維度，但通常越高維度資料可以分得越開。
<br>


## 常見的Kernel（ Linear、rbf、poly ）
#### 使用的模組
```python
from matplotlib.colors import ListedColormap
import pandas as pd 
import numpy as np
import matplotlib.pyplot as plt
import time

from sklearn import datasets
from sklearn.preprocessing import StandardScaler
from sklearn.svm import SVC
from sklearn.svm import LinearSVC
from sklearn.model_selection import train_test_split
```

#### 使用的資料集
```python
wine = datasets.load_wine()
x = wine.data
y = wine.target

#資料預處理
#使用兩特徵 ['alcohol','malic_acid']
x = x[:,:2]
#標準化
standardScaler = StandardScaler()
standardScaler.fit(x)
x_standard = standardScaler.transform(x)
x_train, x_test, y_train, y_test = train_test_split(x_standard, y,test_size=0.2,random_state=0)
```
#### 定義決策區域
```python
def plot_decision_region(x, y, classifier,test_idx = None, resolution = 0.02):
    # setup marker generator & color map 
    markers = ('s', 'x', 'o','^','v')
    colors = ('red','blue','lightgreen','gray','cyan')
    cmap = ListedColormap(colors[:len(np.unique(y))])
    plt.figure(figsize=(10, 10))
    plt.rcParams['font.size'] = 16
    
    #plot the decision surface
    x1_min, x1_max = x[:, 0].min() -1, x[:, 0].max()+1
    x2_min, x2_max = x[:, 1].min() -1, x[:, 1].max()+1
    xx1, xx2 = np.meshgrid(np.arange(x1_min, x1_max, resolution),
                           np.arange(x2_min, x2_max, resolution))
    
    z = classifier.predict(np.array([xx1.ravel(), xx2.ravel()]).T)
    z = z.reshape(xx1.shape)
    #plt.xlim(xx1.min(), xx2.max())
    #plt.ylim(xx2.min(), xx2.max())
    
    custom_cmap = ListedColormap(['#EF9A9A','#FFF59D','#90CAF9'])
    plt.contourf(xx1, xx2, z, cmap=custom_cmap, alpha = 0.3)
    
    for idx, cl in enumerate(np.unique(y)):
        plt.scatter(x = x[y == cl,0],
                    y = x[y == cl, 1],
                    alpha = 0.8,
                    c = colors[idx],
                    marker = markers[idx],
                    label = cl,
                    edgecolor = 'black')
        
        #highlight test samples
        if test_idx:
            #plot all samples
            x_test, y_test, = x[test_idx, :], y[test_idx]
            
            plt.scatter(x_test[:, 0],
                        x_test[:, 1],
                        c = '',
                        edgecolor = 'black',
                        alpha = 1.0,
                        linewidth = 1,
                        marker = 'o',
                        s = 100,
                        label = 'test set')

```
#### 訓練模型並繪出決策區域
```python
def SVM_(model,x_train,y_train,x_test,y_test,gamma = 5,degree = 3):
    if model == 'linear':
        svm = SVC(kernel = model)
        svm.fit(x_train,y_train)
        train_score = svm.score(x_train,y_train)*100
        test_score = svm.score(x_test,y_test)*100
    elif model == 'rbf':
        svm = SVC(kernel = model , gamma = gamma)
        svm.fit(x_train,y_train)
        train_score = svm.score(x_train,y_train)*100
        test_score = svm.score(x_test,y_test)*100
    else:
        svm = SVC(kernel = model , degree = degree)
        svm.fit(x_train,y_train)
        train_score = svm.score(x_train,y_train)*100
        test_score = svm.score(x_test,y_test)*100
    
    plot_decision_region(x_train, y_train , classifier = svm)
    plt.title(f'SVC(kernel={model}) (train accuracy={train_score:.1f}%, ' + \
              f'test accuracy={test_score:.1f}%)')
    plt.xlabel('alcohol [standardized]')
    plt.ylabel('malic_acid [standardized]')
    plt.legend(loc = 'upper left')
    plt.tight_layout()

    plt.show()
    
```
## Kernel = Linear
在研究線性分類器中發現 SVM 在處理線性問題時有兩種版本，一種是使用 SVC 呼叫線性核函式如下左圖，而下右圖則是用 LinearSVC 的方法。而測試結果發現專門處理線性問題的LinearSVC（右） 在 test data 上的正確率僅有 69.4% ，跟使用線性核函式（左）比較起來結果更不理想，時間效率上也多了整整一倍的時間成本。在樣本數量少的時候使用 SVC 呼叫線性核函式的效果比使用LinearSVC好。但線性核函式的正確率也僅有77.8%，在處理線性不可分的效益不高。
  <img src="https://github.com/YuTe-Lai/Study_process/blob/master/Machine%20Learning/img/Lecture8_SVM_linearkernel.png?raw=true"  width="820" height="550"><br>

## Kernel = rbf
使用 rbf 核函式調整其中 gamma 參數，如下圖，gamma值如果越大決策線就越曲折，花費的時間也越多，每個點影響的範圍就越小，越容易造成 overfitting 。其中比較值得注意的是 gamma = 0.01 時不論是分數還是時間成本都比線性核函式弱，可以推論 SVM_rbf 更適合解決非線性的問題。<br>

  <img src="https://github.com/YuTe-Lai/Study_process/blob/master/Machine%20Learning/img/Lecture8_SVM_rbf_kernel.png?raw=true"  width="910" height="880"><br>

經測試在 gamma = 5  或 gamma = 6 的時候分數是一樣的，但是以時間效率來看，我認為 gamma = 5 時應該會是更好的選擇。
## Kernel = poly
poly核函式的參數degree <1的時候如下圖，模型會直接全猜一樣的label。  <br>
<img src="https://github.com/YuTe-Lai/Study_process/blob/master/Machine%20Learning/img/Lecture8_SVM_poly_kernel0.png?raw=true"  width="300" height="300"><br>

而在degree>1的情況下，degree的決策線跟gamma一樣越大就越曲折。其中奇數與偶數會呈現不同的圖形，偶數時的mergin看起來像是用兩個平面定義出來的空間，degree越大平面就越彎曲，其正確率大約都落在60%，隨著degree值越高準確率越低。其 degree = 3 時有最高的分數。<br>
 <img src="https://github.com/YuTe-Lai/Study_process/blob/master/Machine%20Learning/img/Lecture8_SVM_poly_kernel1.png?raw=true" width="800" height="800"><br>
 <img src="https://github.com/YuTe-Lai/Study_process/blob/master/Machine%20Learning/img/Lecture8_SVM_poly_kernel2.png?raw=true" width="800" height="570"><br>

