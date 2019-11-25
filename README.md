# [SAS Data Hack Platypus. Онлайн-этап](https://sascompetitions.ru/competitions/sas-data-hack-platypus-online)

## Данные

**Date** - плановая дата доставки до клиента <br>
**DateOrder** - дата оформления заказа <br>
**ClientID** - ID клиента <br>
**ChannelID** - канал сбыта <br>
**OrderID** - номер заказа, присваевымый сайтом <br>
**MaterialID** - ID материала <br>
**GroupID** - группа Закупок ID <br>
**DeliveryType** - тип доставки <br>
**Cluster** - кластер доставки <br>
**Interval** - временной интервал доставки (с n-часов по n-часов) <br>
**CancelFlag** - метка отмены заказов - целевая переменная первого этапа <br>
**OrderCnt** - заказано, шт <br>
**Prepay** - признак предоплаты <br>
**Count_edit** - число редактирований заказа клиентом, 1 (первоначальный ввод) и больше <br>
**Delta** - число часов от отказа до времени доставки, целевая переменная второго этапа <br>

Метрика - **ROC AUC**.

## 6th place

Что сработало:
- Агрегации по дням недели и месяцам года
- Подсчет количеств уникальных и общего числа елементов заказа
- [One hot encoding](https://en.wikipedia.org/wiki/One-hot) категориальных переменных

Что не сработало:
- Target encoding (не сумел завести нормально)
- Обычная [`KFold`](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.KFold.html) валидация давала хуже прогноз чем [`StratifiedKFold`](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.StratifiedKFold.html)
- Бленд [**XGBoost**](https://xgboost.readthedocs.io/en/latest/) и [**LightGBM**](https://lightgbm.readthedocs.io/en/latest/) не дал прироста целевой метрики

Что не успел попробовать:
- Подобрать параметры для **LightGBM** и **XGBoost**
- Настроить вес позитивного класса (соотношение позитивного к негативному класса в тестовом датасете составляет приблизительно 1 к 16)
- Завести CatBoost
