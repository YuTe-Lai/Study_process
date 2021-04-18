# 實作 MLP Classifier

### Data
```python
from keras.datasets import fashion_mnist
(x_train, y_train), (x_test, y_test) = fashion_mnist.load_data()
```
```python
print(x_train.shape,y_train.shape)
```
-> (60000, 28, 28) (60000,)<br><br>
X 訓練資料集中有 60000 個 28x28 的資料，對應 Y 資料集中的 60000 個標籤。

### Preprocessing
```python
# Normalization
x_train_normalized = x_train / 255
x_test_normalized = x_test / 255
```
對於電腦來說，若兩張相同圖片的曝光、對比等不同，會導致像素值不一樣，經過卷積層運算後容易導致他們的特徵不同。且運算彩色圖片時會分成RGB三種分量，權值會朝著分量大的方向前進，然而實際訓練模型時通常每張圖都會由不同顏色主導，讓權值更新的主導權不斷變化，導致模型Gradient更新無序、收斂慢，故CNN 還是要做標準化。

```python
# Add image noise
x_train_noise = x_train_normalized + np.random.normal(0, 0.1, (60000, 28, 28))
x_test_noise = x_test_normalized + np.random.normal(0, 0.1, (10000, 28, 28))
```
帶有雜訊的圖片會干擾模型的判斷，故在訓練之前先將圖片去噪便能排除或降低這些干擾，但實務上，模型的其他部份也須同步去噪才能達到效果。另一種方法則是主動在訓練資料中加入對抗樣本（有雜訊的圖片），稱之為「對抗訓練」（Adversarial training）。<br>
