## 1. Bir partideki toplam 16 kayıt cihazından 4’ü arızalıdır. Bu partiden rastgele 3 kayıt cihazı seçilirse, seçilen arızalı kayıt cihazı sayısının olasılık dağılımını, beklenen değerini, varyansını ve standart sapmasını hesaplayınız.


```python
from sympy.stats import FiniteRV, density, E, variance, std
finX = FiniteRV('X', {0: 11/28, 1: 33/70, 2: 9/70, 3: 1/140}) 
print(f"Olasılık dağılımı: {density(finX).dict}")
print(f"Beklenen değer: {E(finX).round(2)}")
print(f"Varyans: {variance(finX).round(4)}")
print(f"Standart sapma: {std(finX).round(3)}")
```


```python
from sympy.stats import Hypergeometric, density, E, variance, std
hypX = Hypergeometric('X', 16, 4, 3)
print(f"Olasılık dağılımı: {density(hypX).dict}")
print(f"Beklenen değer: {E(hypX).round(2)}")
print(f"Varyans: {variance(hypX)}")
print(f"Standart sapma: {std(hypX)}")
```


```python
from scipy.stats import hypergeom
print(f"Olasılık dağılımı: {hypergeom.pmf([0, 1, 2, 3], 16, 4, 3)}")
print(f"Beklenen değer: {hypergeom.expect(args=(16, 4, 3)).round(2)}")
print(f"Varyans: {hypergeom.var(16,4,3)}")
print(f"Standart sapma: {hypergeom.std(16,4,3).round(3)}")
```

## 2. Belirli bir kavşakta kırmızı ışıkta duran bir sürücünün ışığın yeşile dönmesi için bekleme süresi (saniye) [0, 30] aralığında düzgün (tekdüze, uniform) dağılıma sahiptir. Sürücünün bekleme süresinin 10 saniyeden az olması olasılığını, 24 saniyeden fazla olması olasılığını, ortalamasını, varyansını ve standart sapmasını hesaplayınız.


```python
from sympy.stats import Uniform, E, variance, std, cdf
uniX = Uniform("X", 0, 30)
print(f"Sürücünün bekleme süresinin 10 saniyeden az olması olasılığı: {cdf(uniX)(10)}")
print(f"Sürücünün bekleme süresinin 24 saniyeden fazla olması olasılığı: {cdf(uniX)(6)}")
print(f"Sürücünün bekleme süresinin ortalaması: {E(uniX)}")
print(f"Sürücünün bekleme süresinin varyansı: {variance(uniX)}")
print(f"Sürücünün bekleme süresinin standart sapması: {std(uniX)}")
```


```python
from scipy.stats import uniform
print(f"Sürücünün bekleme süresinin 10 saniyeden az olması olasılığı: {uniform.cdf(10, 0, 30).round(1)}")
print(f"Sürücünün bekleme süresinin 24 saniyeden fazla olması olasılığı: {uniform.sf(24, 0, 30).round(2)}")
print(f"Sürücünün bekleme süresinin ortalaması: {uniform.mean(0,30)}")
print(f"Sürücünün bekleme süresinin varyansı: {uniform.var(0,30)}")
print(f"Sürücünün bekleme süresinin standart sapması: {uniform.std(0,30).round(2)}")
```

## 5. Kanada’nın Hamilton şehrinde televizyon sahibi olan 500 aileden oluşan bir rastgele örneklemde, 340 ailenin HBO’ya abone olduğu gözlemlenmiştir. Bu şehirde televizyonu olan HBO abonesi ailelerin gerçek oranı için bir %95 güven aralığı elde ediniz. Güven aralığını elde ederken güvenilirlik katsayısı (reliability factor), standart hata (standard error), hata marjini (margin of error), alt güven sınırı (lower confidence limit) ve üst güven sınırını (upper confidence limit) hesaplayınız.


```python
from math import sqrt
x = 340
n = 500
p = x/n

reliability_factor = 1.96
standard_error = sqrt( p * (1 - p) / n )
margin_of_error = reliability_factor * standard_error
lower_conf_limit = p - margin_of_error
upper_conf_limit = p + margin_of_error

print(f"Reliability factor: {reliability_factor}")
print(f"Standard error: {round(standard_error,4)}")
print(f"Margin of error: {round(margin_of_error, 3)}")
print(f"Lower confidence limit: {round(lower_conf_limit, 3)}")
print(f"Upper confidence limit: {round(upper_conf_limit, 3)}")
```
