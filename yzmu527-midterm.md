```python
import statistics
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
import stemgraphic
dataset = [10,20,20,30,30,30,40,40,40,40,50,50,50,50,50,60,60,60,60,60,60,70,70,70,70,70,70,70,80,80]
```

## 1. Örneklem büyüklüğü 30 olan kendi oluşturduğunuz bir veri kümesi için

## a) Ortalama ve standart sapma değerlerini hesaplayınız.


```python
print(f"Veri kümesinin ortalaması: {statistics.mean(dataset)}\nVeri kümesinin standart sapma değeri: {round(statistics.stdev(dataset),2)}")
```

## b) Ortanca, mod, ve kartil (çeyreklik) değerlerini hesaplayınız.


```python
print(f"Veri kümesinin ortancası: {statistics.median(dataset)}\nVeri kümesinin modu: {statistics.mode(dataset)}\nVeri kümesinin kartilleri: {statistics.quantiles(dataset)} ")

```

## c) Ortalama, ortanca ve mod değerlerini kıyaslayarak veri kümenizin çarpıklığı hakkında yorum yapınız.
Ortalama < medyan < mod olduğu için veri kümesi negatif olarak çarpıktır.
## d) Aralık ve kartiller arası aralık (IQR) değerlerini hesaplayınız.


```python
print(f"Veri kümesinin aralık değeri: {np.ptp(dataset)}\nVeri kümesinin kartiller arası aralık değeri: {statistics.quantiles(dataset)[2] - statistics.quantiles(dataset)[0]}")
```

## e) 6 sınıf içeren bir frekans dağılım tablosu elde ediniz.


```python
temp = pd.Series(dataset).value_counts(bins=6).sort_index()
data = {"Sınıf": temp.index, "Frekans": temp.values,}
df2 = pd.DataFrame(data)
df2["Kümülatif frekans"] = np.cumsum(df2['Frekans'])

df2
```

## f) Frekans tablosunu kullanarak ilgili histogram ve ogive grafiklerini çiziniz.


```python
hist = df2["Frekans"].values
bin_edges = np.histogram(dataset, bins=6)[1]
fig, ax = plt.subplots()
ax.hist(dataset, bin_edges, edgecolor="Black")
plt.title('Histogram')
plt.show()
```


```python
plt.plot(bin_edges[1:], df2['Kümülatif frekans'], marker='o')
plt.title('Ogive')
plt.show()
```

## g) Veri kümenize ait bir gövde-yaprak grafiği elde ediniz.


```python
stemgraphic.stem_graphic(dataset, scale=10, asc=False)
```

## 2. Aşağıdaki soruları yanıtlayınız.

## a) Kovaryans ve korelasyon katsayısı nedir ve ne işe yarar? Detaylıca açıklayınız.
Kovaryans katsayısı, iki değişken arasındaki pozitif ya da negatif ilişkiyi tanımlayan, bu ilişki hakkında yorum yapabilmemizi sağlayan değerdir. Popülasyon kovaryansı ve örneklem kovaryansı olarak ikiye ayrılır. Aralarındaki fark popülasyon kovaryansının tüm veri kümesi(N) üzerinde, örneklem kovaryansının ise örneklem(N-1) üzerinde uygulanıyor olmasıdır.

Korelasyon katsayısı ise kovaryansa benzer olarak iki değişken arasındaki ilişkinin yönünü ve gücünü verir. Fakat kovaryanstan farklı olarak değişkenlerin büyüklüğünden etkilenmeden -1 ve +1 arasında standart bir değer sunar. En bilinen türleri Pearson, Spearman ve Kendall'dır.
## b) Kovaryans ve korelasyon katsayısı değerlerini hesaplayabileceğiniz bir veri kümesi oluşturup bu değerleri elde ediniz.


```python
# "Örneklem" verilerim
x = [15,  28,  32,  46,  59,  65,  77,  81,  93, 100]
y = [300, 243, 236, 195, 186, 154, 138, 128, 84, 60]
```


```python
np.cov(x,y)[0][1].round(2) # Popülasyon kovaryansı hesaplayacak olsak bias'ı True yapmamız gerekirdi.
```


```python
np.corrcoef(x,y)[0][1].round(2)
```

## c) Veri kümenize ait saçılım garifiğini çiziniz.


```python
plt.scatter(range(1,11),x, label="X")
plt.scatter(range(1,11),y, label="Y")
plt.title("Saçılım")
plt.legend()
plt.show()
```

## d) Elde ettiğiniz kovaryans ve korelasyon katsayısı değerleri ve oluşturduğunuz saçılım grafiğini kullanarak veri kümenizi oluşturan değişkenler arasındaki ilişki hakkında yorum yapınız.
İki veri kümesi arasında çok güçlü negatif bir ilişki vardır. X kümesindeki değerler arttıkça Y kümesindeki değerler azalma eğilimi göstermektedir.
