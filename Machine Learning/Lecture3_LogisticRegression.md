# Logistic Regression VS Classification
Classification 預測的值是不連續的項目種類 ( 例如：是否回購、是否續租...等 )，其輸出結果為：是或否、1 或 0 。但是在生活中更常見的應用會像是：根據今天的溫度、濕度、風向來預測明天的天氣，
通常我們會需要知道明天是晴天的機率或是雨天的機率，來決定是否帶傘具出門。而 Logistic Regression 便是這種分類模型，其輸出值會介在 0 , 1 之間。

# Sigmoid Function
Sigmoid Function 的 y 值介於 0 ~ 1，這樣的分布也符合機率是在 0 ~ 1 的範圍中。如下圖所示，當 Z = 0 時判斷成 1 的機率為 0.5，因此只要 z > 0 判斷成 1 的機率就會 > 0.5 ，
反之如果 z ≤ 0 判斷成 1 的機率就 ≤ 0.5 ，因此我們就把他判斷成 0。Logistic Regreesion 跟 Classification 的不同在於他多了機率的資訊。 

<img src="https://github.com/YuTe-Lai/Study_process/blob/master/Machine%20Learning/img/Lecture3_LogisticRegression_Sigmoid.png?raw=true" width="660" height="320"><br>

# Logistic Regression : Cost Function
以條件機率來看的話：
- 當 y = 1 時，希望 P ( y = 1 | x ) 越大越好。若 y(i) = 1 : P(y(i) = 1|x(i))^y(i) * P(y(i) = 0|x(i))^(1−y(i)) = P ( y(i) = 1|x(i) )
- 當 y = 0 時，希望 P ( y = 0 | x ) 越大越好。若 y(i) = 0 : P(y(i) = 1|x(i))^y(i) * P(y(i) = 0|x(i))^(1−y(i)) = P ( y(i) = 0|x(i) )

因為機率越乘越小，所以目標改為最大化： Cost Function = 最大化（ P ( y(i) = 1 | x(i) ) ＊ P ( y(i) = 0 | x(i) ) ）<br>
<img src="https://github.com/YuTe-Lai/Study_process/blob/master/Machine%20Learning/img/Lecture3_LogisticRegression_CostFunction.png?raw=true" width="180" height="70"><br>
將函式取 log：<br>
<img src="https://github.com/YuTe-Lai/Study_process/blob/master/Machine%20Learning/img/Lecture3_LogisticRegression_CostFunction1.png?raw=true" width="500" height="180"><br>
接下來將函式加個負號，讓最大化問題變成最小化問題，便可以利用梯度下降法求出：<br>
<img src="https://github.com/YuTe-Lai/Study_process/blob/master/Machine%20Learning/img/Lecture3_LogisticRegression_CostFunction2.png?raw=true" width="400" height="215"><br>

加入正規化參數：<br>
<img src="https://github.com/YuTe-Lai/Study_process/blob/master/Machine%20Learning/img/Lecture3_LogisticRegression_CostFunction3.png?raw=true" width="440" height="160"><br>

# 模型實作
### 使用資料集------鳶尾花卉數據集
```python
import pandas as pd 
import numpy as np
from sklearn import datasets
iris = datasets.load_iris()
features = pd.DataFrame(iris['data'], columns = iris['feature_names'])
targets = pd.DataFrame(iris['target'], columns = ['class'])
df = pd.concat([features, targets], axis=1)
df = df[df['class'] !=2 ] #只使用類別1跟2的資料

```
### 畫出散佈圖
```python
import matplotlib.pyplot as plt
import seaborn as sns

plt.style.use('ggplot')
g = sns.FacetGrid(df, hue='class', size = 5)
g.map(plt.scatter,'sepal length (cm)','sepal width (cm)')
g.add_legend()
```
<img src="https://github.com/YuTe-Lai/Study_process/blob/master/Machine%20Learning/img/Lecture3_LogisticRegression_scatter.png?raw=true" width="440" height="400"><br>

### 資料預處理
```python
#標準化
from sklearn.preprocessing import StandardScaler
x = df.iloc[:,:2].values #使用前兩項特徵
y = df.iloc[:,4].values

sc = StandardScaler()
sc.fit(x)
x_std = sc.transform(x)
```
### 訓練Logistic Regression
```python
from sklearn.linear_model import LogisticRegression
from matplotlib.colors import ListedColormap

lr = LogisticRegression(C = 100.0, random_state= 1)   # C = 1/λ
lr.fit(x_std, y)
print(lr.coef_)
print(lr.intercept_)
```
[[ 9.97519721 -6.71009506]]<br>
[1.81731713]<br>

### 繪出決策區域圖
```python
from matplotlib.colors import ListedColormap
#定義決策區域
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
            
plot_decision_region_ver2(x_std, y , classifier = lr)
plt.xlabel('sepal length [standardized]')
plt.ylabel('sepal width [standardized]')
plt.legend(loc = 'upper left')
plt.tight_layout()

plt.show()
```
<img src="https://github.com/YuTe-Lai/Study_process/blob/master/Machine%20Learning/img/Lecture3_LogisticRegression_decision.png?raw=true" width="440" height="400"><br>






