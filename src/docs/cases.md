### Наиболее популярные кейсы

Для понимания алгоритма выполнения основных задач ознакомьтесь с доступными SDK в [разделе](https://russianinvestments.github.io/investAPI/faq_python/) "Языки программирования".   

Рекомендуется также прочитать [статью о создании торгового робота](https://habr.com/ru/companies/tinkoff/articles/709166/).

В статье описаны популярные сценарии для пользователей Tinkoff Invest API.

#### Как создать заявку на покупку или продажу инструмента

В случае, когда стратегия дает команду продавать или покупать, необходимо создать заявку:

1. Проверьте существует ли позиция по бумаге с помощью метода [FindInstrument](/investAPI/instruments/#findinstrument).
2. Проверьте статус торгового инструмента с помощью метода [GetTradingStatus](/investAPI/marketdata/#gettradingstatus).
3. Получите последние цены на инструмент с помощью метода [GetLastPrice](/investAPI/marketdata#getlastprices).
4. Получите параметр `min_price_increment` для расчета цены, которую возможно выставить, с помощью метода [GetInstrumentBy](/src/docs/instruments.md/#getinstrumentby).
5. Проверьте свой счет на аккаунте.
6. Выставите заявку с помощью метода [PostOrder](/investAPI/orders#postorder) и сохраните полученный параметр `order_id`.
7. Получите список активных заявок с помощью метода [GetOrders](/investAPI/orders#getorders) и проверьте есть ли заявка в списке активных по параметру `order_id`.

Информацию об исполненной заявке возможно получить с помощью метода [GetOrderState](/investAPI/orders#getorderstate) по параметру `order_id`.


### Начало работы и получение информации об аккаунте

Для получения информации об аккаунте:

1. Вызовите метод [GetAccounts](/investAPI/users#getaccounts) для получения списка счетов, их статусов и типов.
2. Вызовите метод [GetInfo](/investAPI/users#getinfo), который позволяет:
    * определить наличие у пользователя статуса квалифицированного инвестора, премиального клиента;
    * получить список типов инструментов, к которым пользователь имеет доступ по итогам тестирования. 
   
   Эта информация помогает определить ограничения в торговле.
3. Получите доступные лимиты с помощью метода [GetInfo](/investAPI/users#getaccounts).
4. Периодически обновляйте информацию о маржинальных показателях счета с помощью метода [GetMarginAttributes](/investAPI/users#getmarginattributes) по параметру `accountId` для торговли на срочном рынке.

### Как найти базовый актив фьючерса

Для поиска базового актива фьючерса:

1. Вызовите один из методов: [GetFutureBy](/investAPI/instruments/#futureby) или [GetFutures](/investAPI/instruments/#futures). 
2. Сохраните значение параметра `basic_asset_position_uid` (уникальный идентификатор позиции основного инструмента).

>**Примечание**
> Для поиска базового актива фьючерса можно также использовать метод [FindInstrument](/investAPI/instruments/#findinstrument). Для этого достаточно передать в query значение параметра `basic_asset_position_uid`, возвращаемое методами GetFutureBy и GetFutures.
