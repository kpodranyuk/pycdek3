##PyCDEK
Библиотека для работы с API транспортной компании [СДЭК](http://cdek.ru/).

База городов, список тарифов и докуентация API доступна по ссылке: http://www.edostavka.ru/website/edostavka/upload/custom/files/CDEK_integrator.zip

Для получения логина и пароля необходимо [заключить договор](http://www.edostavka.ru/reglament.html) с транспортной компанией.

####Установка:

    pip install git+https://github.com/onrik/pycdek.git#egg=pycdek


#### Методы не требующие логина и пароля:

```python
from pycdek.client import Client

# получение пунктов самовывоза в Москве
for point in Client.get_delivery_points(44).xpath('Pvz'):
    print point.attrib['Code'], point.attrib['Address']
    
# расчет доставки Москва - Санкт-Петербург одной посылки весом 1кг и габаритами 50x10x20
tariffs = [5, 10, 15, 62, 63, 136] #  тарифы склад-склад (самовывоз)
print Client.get_shipping_cost(44, 137, tariffs, goods=[{'weight': 1, 'length': 50, 'width': 10, 'height': 20}])

# расчет доставки Санкт-Петербург - Москва одной посылки весом 2кг и габаритами 100x10x20
tariffs = [11, 16, 137]  # тарифы склад-дверь (доставка курьером)
print Client.get_shipping_cost(137, 44, tariffs, goods=[{'weight': 2, 'length': 100, 'width': 10, 'height': 20}])
    
```
