# Convolutional Neural Network，CNN

### 特徵 feature
CNN 會比較兩張圖片裡的各個局部，這些局部被稱為特徵（feature）。特徵就像是一張更小的圖片，也就是更小的二維矩陣。這些特徵會捕捉圖片中的共通要素。<br>
- Convolved feature 值越高代表越符合特徵。<br>
<img src="https://raw.githubusercontent.com/YuTe-Lai/Study_process/master/img/NN_CNN1.png"  width="400" height="277"><br>

### 卷積 convolution
當CNN 要分辨一張圖片時，CNN 會比對圖片中的任何地方。要計算特徵和圖片局部的相符程度，只要將特徵和圖片局部的各個像素上的值相乘、再總和。如上圖，黃框內紅字為特徵，若兩個像素相符，乘積為`1*1=1`；若兩個像素不相符，乘積為`0*1=0`。也就是說像素相符的乘積為 1，像素相異的乘積為 0。如果兩張圖的每個相素都相符，將這些乘積加總就會得到 9；反之，如果兩者的像素完全相異，就會得到 0。接著只要重複上述過程、歸納出圖片中各種可能的特徵，就能完成卷積。<br>
- 用 𝟑×𝟑 Kernel 將 𝟓×𝟓 的圖片掃過一遍，可以得到 feature map (特徵圖)
- 特徵圖有降階的作用，達到減少特徵量的目的
- 通常會設定多個過濾器來擷取圖片特徵

### 池化 pooling
池化是一個壓縮圖片並保留重要資訊的方法，負責對feature map 做重點挑選。池化會在圖片上選取不同的範圍，並在這個範圍中選擇一個最大值或是取加權平均。實務上，邊長為二或三的正方形範圍，搭配兩像素的間隔（stride）是滿理想的設定。原圖片經過池化以後，其所包含的像素數量會降為原本的四分之一，但池化後的圖片包含了原圖中各個範圍的最大值或加權平均，它還是保留了每個範圍和各個特徵的相符程度。也就是說，池化後的資訊更專注於圖片中是否存在相符的特徵，而非圖片中哪裡存在這些特徵。<br>
- Dimension reduction
- Mean- or Max-pooling

### 填補 padding
Padding是為了不讓輸入圖片被萃取太小張所採取的作法，在原圖片周圍補上 0 (zero-padding) 後進行convolution 計算。
- 不讓輸入圖片被萃取太小張
- 強化邊緣特徵

<img src="https://raw.githubusercontent.com/YuTe-Lai/Study_process/master/img/NN_CNN2.png"  width="823" height="277"><br>


