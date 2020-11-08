# 機器學習
機器學習指的是，透過從過往的資料和經驗中學習並找到其運行的規則，最後達到人工智慧的方法。其架構如下圖：<br>
<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/img/ML_flowchart.png?raw=true" alt="ML_flowchart"  width="700" height="370"><br>
目標函式（Target Function）代表你想要學習的規則，在沒有雜訊（noise）的情況下，輸入每組變數Xn都可以找到一組精確的輸出Yn，而Target Function能產生多個Data，從中隨機抽取出N組Data來做機器學習，接下來Learning Algorithm會利用這些取出的Data去找出最吻合的假設函式（Hypothesis），那這組Hypothesis就成了我們學習出來的結果，我們可以利用這個結果來預測新的問題。<br>
註：<br>
目標函式（ f ）：代表該問題最完美的解法，而最佳解法是未知的，我們只能將資料透過演算法去計算出最接近目標函式的方法。<br>
訓練資料（ D ）：`D1（X1,Y1）、D2（X2,Y2）、...、Dn（Xn,Yn）`，其中X為特徵，Y為Label。<br>
假設函式集（ H ）：模型從資料中推導出來的函式為假設函數，其越接近目標函式正確率越高。<br>
輸出函式（ g ）：從Hypothesis set裡選出一個與目標函式誤差最小的當成輸出函示。<br>
## 機器學習的種類
#### 根據輸出值y的Label情況可以分為：
| Type            | Label       | Method   |
| --------------------- |----------------| -------------|
| 監督式 Supervised       | 全部標記        |將所有已標注Label的資料餵給機器，機器會從中找出與目標函示誤差最小的結果。 |
| 非監督式 Unsupervised   | 沒有標記        |讓機器從完全沒有Label的資料中找出有相同特徵的資料群。|
| 半監督式 Semi-Supervised| 少量標記        |大量標記Label需要極高的成本，故只標記少數的資料。成本比監督式還低，但準確率容易比非監督高。|
| 增強式 Reinforcement    | 沒有標記        |可能手上沒有任何資料，直接讓模型執行，再將執行結果反饋回去做訓練。|
#### 根據Data的給予方式可以分為：
| Type          |Method       |
|------------   |------------ |
|Batch Learning |一次將全部Data餵給機器。|
|Online Learning|將Data分別以序列的方式一個一個餵給機器，這樣的方式讓Model可以隨時更新。|
|Active Learning|機器不僅是被動的接受 Data，而是會主動對使用者提出問題。|

#### 輸入值x（特徵）可以分為：
| Type          |Notice                         |Example            |
|------------   |--------------------           |-------------------|
|Concrete Features（具體） |當輸入變數是建立在人類知識預處理過的情況下。|
|Abstract Features（抽象）|當輸入變數對人類來說不具有意義時。|
|Raw Features（原始）|直接採用不加以處理的原始數據。|

#### 輸出值y可以分為：
從輸出值y的種類上可以分為二元分類、多元分類、線性（Regression）和結構化預測（Structured Learning ）問題。
| Situation         |Output Type    |
|--------------------|----------------|
|分類 Classification  |一種類別     |
|線性 Regression      |純量scalar   |
|結構化 Structured    |序列、句子、圖、樹等|


## 機器學習的方法
  在機器學習的過程中，我們真正希望的是能讓機器去預測新的問題，所以真正的目標是能將「沒有看過的Data」預測好，而不只是將取樣的Data預測好就夠了。因此，我們要建立一個Learning Model可以確保
Ein≈Eout，所以在Learning Algorithm選出最小Ein的Hypothesis的同時，這組Hypothesis也可以很好的預測Out-sample，我們才可以說機器已經會學習了。<br>
註：<br>
In-Sample-Data：抽樣的Data（Train-Data）。<br>
In-sample Error(Ein)：Hypothesis預測In-sample Data的誤差。<br>
Out-Sample-Data：未被抽樣的Data（Test-Data）。<br>
Out-of-sample Error（Eout）：Hypothesis預測Out-of-sample Data的誤差。<br>
#### 證明
而下面是根據Hoeffding不等式，來解釋Ein≈Eout這個條件：<br>
<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/img/ML_EinEout.png?raw=true" alt="ML_EinEout"  width="600" height="320"><br>
假設今天有個桶子裡面包含綠色跟橘色兩種顏色的球，如果今天桶子內橘色球佔的比例為μ，而今天我們從中隨機抽樣出N顆小球，並且計算出這N顆小球中橘色佔的比例為ν，這個時候μ=ν不一定會成立，但可以想像得到μ跟ν也不至於差太多，所以Hoeffding不等式就告訴我們|μ−ν|會被限制在一個範圍內，表示為：`ℙ[|ν−μ|>ε]≤2exp(−2ε^2N)`，當ε（threshold）越大，出現的機率就越低。<br>
<br>
而我們再用每一個Hypothesis預測Data結果的好壞代替橘球跟綠球，預測正確是綠球，預測失敗是橘球，所以對於In-Sample-Data來說：`ν = Ein(h)`，對於Out-Sample來說：`μ = Eout(h)`。套入剛剛的不等式，得`ℙ[|Ein(h)−Eout(h)|>ε]≤2exp(−2ε^2N)`，我們這邊將超過ε的Data定義為Bad Data，那就可以確定Ein和Eout差距超過ε的可能性是被限制住的，當ε越大，出現的機率就越低。<br>
<br>
而事實上我們不會只有一個Hypothesis，所以當我們考慮有M個Hypothses時，有可能每個Hypothsis出現Bad Data的地方都不盡相同，因此會減少能使用的Data。而最慘的情況就是在M個Hypotheses裡的每份Bad Data彼此都沒有重複，所以把這些出現Bad Data的機率取聯集得到以下式子：`ℙ[∃h∈ℍ s.t. |Ein(h)−Eout(h)|>ε]≤2Mexp(−2ε^2N)`。<br>
<br>
目前為止可以得到一個結論：當資料量N夠大時，且Hypothesis的數量不是無限大的時候，基本上Ein≈Eout就成立。然而當Hypothesis的數量是無限的情況呢？<br>
我們剛剛採用的假設是每組Hypotheses的Bad Data彼此間都沒有重疊，所以在M是無限大的情況下，當然會有一個無限大的上限值，但如果考慮了Bad Data重疊的情形，縱使M是無限大，還是有機會把Bad Data的出現機率壓在一個有限的值之下。<br>
<br>
然而讓我們回到二元分類問題，如果今天在二維平面上做二元分類：<br>
- 當資料量n=1時，就算你的Hypotheses有無窮多種，但對於一組Data來說就只有兩種Hypotheses而已：`H{o,x}`。
- 當資料量n=2時，一樣是無限多組切法但Hypotheses也只能歸類成4類：`H{oo,ox,xo,xx}`。
- 當資料量n=3時，在一樣的邏輯下，Hypotheses只能歸類成8類：`H{ooo,oox,oxo,xoo,oxx,xox,xxo,xxx}`。<br>
不過在某些情況下，比如說當資料共線的時候，當資料量n=3時，在一樣的邏輯下，Hypotheses變成只能歸類成6類（如下圖，右圖第三行為線性不可分割，故不考慮）：<br>
<img src="https://github.com/YuTe-Lai/yute-lai.github.io/blob/master/img/ML_Effective_Number_of_Lines.png?raw=true" alt="Effective_Number_of_Lines"  width="946" height="273"><br>
因此我們擔心的「當Data數量增加而造成Hypotheses的種類暴增」的情形被排除了，有一些狀況是不會出現的，故Hypotheses是有重疊的。<br>


  
  
