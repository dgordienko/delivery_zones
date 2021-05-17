# Караван-Сарай

## Зоны доставки

| Каталог  | Зоны доставки   |  Ссылка |
| ------------ | ------------ | ------------ |
| Зоны доставки 001 | Авдеевка Ямполь Часов.Яр Украинск Угледар Торецк Торецк села Соледар Славянск Слав. Черевковка  | [link](https://www.google.com/maps/d/viewer?mid=11PwZAdIqZBCF6J3svIo3EyXGpKb4ptV0&ll=48.7763943405649%2C37.865120024530775&z=11 "link")  |
|  Зоны доставки 002 |  Слав. Курорт Слав. ЖД Слав. Былбасовка Слав. Артема Селидово Селидово Северск Святогорск Светлодарск Родинское Покровские села |  [link](https://www.google.com/maps/d/edit?mid=1GCiqyZb-G__tnXK8RfscEjM0ppWYDISh&usp=sharing "link") |
|  Зоны доставки 003   | Покровск Покровск Динас Очеретино Ольгинка и Новотроицкое Новогродовка Николаевка Мирноград Мирноград Новатор Марьинские села дальние Марьинские села ближние  |  [link](https://www.google.com/maps/d/edit?mid=12V-0539VGohyWIgBFqKbHYSAnH6vkQsC&usp=sharing "link") |
| Зоны доставки 004|  Марьинка Лиман Курахово Красногоровка Крам. Ясногоровка Крам. Старый город Крам. Новый свет Крам. Старый город Крам. Низ Крам. Лазурный Крам. Веселый | [link](https://www.google.com/maps/d/edit?mid=1F1RgOep9G0_ZGSc9FHNdpD9M9nvYXFBO&usp=sharing "link")  |
|  Зоны доставки 005 |  Крам. Верх Конст. Село Конст. Низ Конст. Верх Изюм Дружковские села Доброполье Горняк Волновахские села низ Волновахские села дальние |  [link](https://www.google.com/maps/d/edit?mid=1bQtlMnecQgXcV5jvXwL1U7OLpJnozrtP&usp=sharing "link") |
|Зоны доставки 006|  Волновахские села ближние Волноваха Великоновоселовские села Великоновоселовские села трасса Великоновоселовские села низ Великоновоселовские села верх Великая Новоселовка Белозерское Белицкое Бахмут | [link](https://www.google.com/maps/d/edit?mid=1vfPeCx9V5NvSWU_qgQd7s_uSDVtPMWJ8&usp=sharing "link")  |
| Зоны доставки 007  | Бах. запад Алексеево-Дружковка Алексан-ка Авдеевка  | [link](https://www.google.com/maps/d/edit?mid=1DcQIcQZ7RVSjD8Z9poz3GwaEyXCaoUxM&usp=sharing "link")  |

~~~python

import pandas as pd
points = pd.read_csv('distributor_delivery_points.csv')
zones = pd.read_csv('distributor_delivery_zones.csv')
points = points.drop(columns=['TERRITORY2_ID', 'TERRITORY1_ID', 'TERRITORY3_ID', 'COORDINATES_FILLING', 'CREATED_BY', 'CREATED_LOGIN', 'CREATED_DATE', 'BRANCH_ID', 'BRANCH_NAME', 'TRADE_NETWORKS_NAME'])
zones = zones.drop(columns=['STATUS_ID', 'STATUS_NAME', 'ENTITYTYPE_ID', 'MIN_SUM_SHOP', 'MIN_SUM_CAR', 'REMOVAL_RATE', 'ROWID'])
result = list()
for item in zones.iterrows():
    zid = item[1]['ID']
    fname = item[1]['NAME']
    zpoint = points[points['DELIVERY_ZONE_ID'] == zid]
    zpoint = zpoint.drop(columns = ['ID','STATUS_ID','STATUS_NAME','DELIVERY_ZONE_ID','TERRITORY_LEVEL','TERRITORY_TYPE_ID'])
    zpoint = zpoint.rename(columns={'CODE':'Код', 'NAME': 'Наименование', 'TERRITORY2_NAME': 'Район', 'TERRITORY3_NAME': 'Нас. пункт', 'DELIVERY_ZONE_NAME':'Зона доставки', 'ADDITIONAL_SHOP_ADDRESS':'Адрес','ACTIVE_WC_QTY': 'Кол-во УР','LATITUDE':'Широта','LONGTITUDE':'Долгота','DISTRIBUTOR_MARKET_TYPE_NAME':'Тип','TERRITORY1_NAME':'Область'})
    zpoint.to_csv('{}.csv'.format(fname))
