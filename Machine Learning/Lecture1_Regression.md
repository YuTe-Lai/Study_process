# 相關係數

<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/Machine%20Learning/img/ML_Regression_R.png?raw=true" alt="R"  width="500" height="100"><br>
<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/Machine%20Learning/img/ML_Regression_R1.png?raw=true" alt="R1"  width="600" height="400"><br>
## Ｒ值的意義：
<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/Machine%20Learning/img/ML_Regression_R2.png?raw=true" alt="R2"  width="600" height="450"><br>
下圖皆**不存在線性相關**，故 `R = 0` 。<br>
<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/Machine%20Learning/img/ML_Regression_R3.png?raw=true" alt="R3" width="600" height="200"><br>

# 線性模型
線性回歸（Linear regression）是根據多個自變數(independent variable)和依變數(dependent variable)之間的關係建出來的模型。只有一個自變數和一個依變數的情形稱為簡單線性回歸(Simple linear regression)，大於一個自變數的情形稱為多元回歸(multiple regression)。
- 自變數(independent variable)：也稱獨立變數，代表這個變數不會被其他變數影響，可以想像成是因果關係裡的因。
- 依變數(dependent variable)：也稱相依變數，代表這個變數基本上是受其他變數影響，如上，像因果關係裡的果。
<br>

以下圖為例，假設廣告支出和年銷售額可以用直線關係表示，那我們就可以將直線表示成簡單線性迴歸：`y = θ0 + θ1x`，而回歸分析就是要將θ0和θ1找出來。所以要先收集一組資料(xi, yi), i=1, …,n，將每個點都帶到回歸公式內：` ŷi = θ0 + θ1xi ， i = 1,…,n `。<br>
- θ0：截距
- θ1：斜率
- ŷi：為預估出來的銷售額，和真實資料還是會有誤差(error)或稱為殘差(Residual)：εi。
- εi = yi — ŷi
<br>
<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/Machine%20Learning/img/ML_Regression_y=h(x).png?raw=true" alt="y=h(x)"  width="600" height="450"><br>
所以回歸分析的目標函數/損失函數(loss function)就是希望找到的模型最後的殘差越小越好。<br>

## 最小平方法 Least Square Method
