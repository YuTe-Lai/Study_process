# 機器學習
機器學習指的是，透過從過往的資料和經驗中學習並找到其運行的規則，最後達到人工智慧的方法。以下圖為例：<br>
未知的目標函式（ f ）：代表該問題最完美的解法，而最佳解法是未知的，我們只能將資料透過演算法去計算出最接近目標函式的方法。<br>
訓練資料（ D ）：`D1（X1,Y1）、D2（X2,Y2）、...、Dn（Xn,Yn）`，其中X為特徵，Y為Label。<br>
假設函式集（ H ）：模型從資料中推導出來的函式為假設函數，其越接近目標函式正確率越高。<br>
輸出函式（ g ）：從Hypothesis set裡選出一個與目標函式誤差最小的當成輸出函示。<br>

<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/img/ML_flowchart.png?raw=true" alt="ML_flowchart"  width="700" height="370"><br>
Target Function（f）代表你想要學習的規則，在沒有noise的情況下，輸入每組變數Xn都可以找到一組精確的輸出Yn，而Target Function（f）能產生多個Data，從中隨機抽取出N組Data來做機器學習，接下來Learning Algorithm會利用這些取出的Data去找出最吻合的Hypothesis，那這組Hypothesis就成了我們學習出來的結果，我們可以利用這個結果來預測新的問題。

