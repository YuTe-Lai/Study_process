# Logistic Regression VS Classification
Classification預測的值是不連續的項目種類(例如：是否回購、是否續租...等)，其輸出結果為：是或否、1或0。但是在生活中更常見的應用會像是：根據今天的溫度、濕度、風向來預測明天的天氣，
通常我們會需要知道明天是晴天的機率或是雨天的機率，來決定是否帶傘具出門。而Logistic Regression便是這種分類模型，其輸出值會介在0,1之間。

# Sigmoid Function
Sigmoid Function 的 y 值介於 0 ~ 1，這樣的分布也符合機率是在 0 ~ 1 的範圍中。如下圖所示，當 Z = 0 時判斷成 1 的機率為 0.5，因此只要 z > 0 判斷成 1 的機率就會 > 0.5 ，
反之如果 z ≤ 0 判斷成 1 的機率就 ≤ 0.5 ，因此我們就把他判斷成 0。Logistic Regreesion 跟 Classification 的不同在於他多了機率的資訊。 

<img src="https://github.com/YuTe-Lai/Study_process/blob/master/Machine%20Learning/img/Lecture3_LogisticRegression_Sigmoid.png?raw=true" width="660" height="320"><br>

# Logistic Regression : Cost Function
以條件機率來看的話：
- 當 y = 1 時，希望 P ( y = 1 | x ) 越大越好。
- 當 y = 0 時，希望 P ( y = 0 | x ) 越大越好。

因為機率越乘越小，所以目標改為最大化： Cost Function = 最大化（ P ( y = 1 | x ) ＊ P ( y = 0 | x ) ）<br>
<img src="https://github.com/YuTe-Lai/Study_process/blob/master/Machine%20Learning/img/Lecture3_LogisticRegression_CostFunction.png?raw=true" width="200" height="80"><br>
