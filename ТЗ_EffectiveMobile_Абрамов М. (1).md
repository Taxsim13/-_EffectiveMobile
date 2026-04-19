Абрамов Максим  
**Задание 1: Анализ требований**

**Раздел ТЗ: Функционал корзины**  
1\. Пользователь может добавить в корзину от 1 до 10 единиц одного товара.  
2\. Пользователь может изменить количество каждого товара в корзине не менее, чем до 1-го. Для удаления товара из корзины используется отдельная кнопка.  
3\. В корзине может находиться не более 5 различных товаров.	  
4\. Суммарное количество всех товаров в корзине не может превышать 20 штук.  
5\. Товары в корзине могут быть разные.  
6\. При попытке добавить товар, превышающий лимиты, система показывает сообщение: "Лимит корзины превышен".  
7\. Цена на продукт фиксируется на момент добавления в корзину и не меняется.  
8\. На странице корзины отображается список товаров, их количество, цена за единицу и общая стоимость позиции.  
9\. Если пользователь уменьшает количество товара до 0, товар удаляется из корзины.  
10\. В корзине может быть реклама других продуктов.  
11\. Реклама товаров в корзине должна быть каждый будний день по утрам и вечерам.  
12\. Если цена на товар изменилась в каталоге, система должна автоматически обновить ее в корзине у всех пользователей.

1) **Противоречия и недочеты в функционале корзины.**  
1. Пункты **1** и **3**. Сумма всех добавленных товаров должна быть не более 50 штук, что противоречит пункту **4**, которое гласит, что количество всех товаров не может превышать 20 штук.  
2. Пункты **2** и **9**. Ограничение на уменьшение количества товара  до 1 штуки, что противоречит возможности уменьшения количества товара до 0, после чего товар удаляется. Кроме того, во **втором** пункте говорится, что для удаления товара из корзины используется отдельная кнопка.  
3. Пункты **3** и **5**. В пункте **5** отсутствует конкретика, требование двоякое и не тестируемое. Пункт **3** более подробно объясняет, что в корзину можно добавить не более 5 различных товаров.  
4. Пункты **7** и **13**. В пунктах есть разногласия: говорится, что цена товара на момент добавления в корзину не меняется, что противоречит положению о том, что если цена на товар изменилась в каталоге, то система автоматически обновляет цену товаров в корзине.  
5. Пункт **6**. Требование сформулировано неоднозначно: неясно, относится ли оно к количеству одного товара или к различным видам товаров.  
6. Пункты **10** и **11**. В одном требовании говорится, что реклама может размещаться в корзине по желанию, а в другом что реклама обязательна по утрам и вечерам, что противоречит требованиям друг друга.

   

2) **Исправление требований для устранения противоречий.**  
1. Пользователь может добавлять в корзину от 1 до 10 единиц одного вида товара.  
2.  Пользователь может добавлять в корзину не более 5 различных видов товаров.  
3.  Система должна ограничивать общее количество товаров в корзине до 50 штук.  
4. Система показывает сообщение “Лимит корзины превышен”, если пользователь пытается добавить в корзину:  
* более 10 единиц одного товара;  
* общее количество товаров, превышающее 50 шт.  
5. Пользователь может изменять количество каждого товара в корзине в пределах от 1 до 10 единиц.  
6. Система должна позволять пользователю удалять товар из корзины с помощью специальной кнопки.  
7. Система должна автоматически обновлять стоимость товаров в корзинах пользователей, если цена товара в каталоге изменилась.  
8. Система должна отображать список товаров, их количество, цену за единицу и общую стоимость.  
9. Система должна отображать рекламу других товаров в корзине в следующие периоды:  
* с 6:00 до 12:00;  
* с 18:00 до 21:00.

**3\) Уточняющие вопросы по ТЗ:**

1. Что произойдет если пользователь попытается изменить количество товара меньше 1 и более 10 единиц?  
2. Каким образом регулируется товар в корзине?   
3. Как происходит удаление товара из корзины с помощью кнопки?  
4. Как система отреагирует на добавление шести различных товаров?  
5. По какому признаку система будет определять различие между товарами в корзине?   
6. Что отобразиться пользователю при попытке добавить товар, превышающий лимит, помимо отображения сообщения «Лимит корзины превышен»?  
7. Что будет отображать корзина, если она пуста от товаров?  
8. Как часто будет обновляться цена товаров в каталоге?  
9. Как должна располагаться реклама продуктов в корзине?  
10. В какие часы утра и вечера будет отображаться реклама товара в корзине?  
11. Что произойдет, если реклама в корзине не будет отображаться в корзине?

**Задание 2: проектирование API**  
Получение списка магазинов-партнёров.  
**GET/api/v1/partners/shops**  
**Параметры запроса**

| Параметр | Описание | Тип параметра | Тип данных | Обязательность | Комментарий |
| :---- | :---- | :---- | :---- | :---- | :---- |
| page | Номер страницы, которую нужно вернуть | Query | integer | Нет |  |
| size | Количество элементов на странице | Query | integer | Нет |  |

**Пример запроса**  
GET/api/v1/partners/shops?page=0\&size=10  
**Тело запроса**  
Отсутствует  
**Параметры успешного ответа**

| Параметр | Описание | Тип данных | Обязательность | Комментарий |
| :---- | :---- | :---- | :---- | :---- |
| shops\[\] | Список магазинов партнёров | array\[object\] | Да |  |
| shops\[\].name | Название магазина-партнёра | string | Да |  |
| shops\[\].linkImage | Ссылка на иконку изображения магазина | string | Да |  |
| shops\[\].deliveryDateFrom | Дата ближайшей доставки (от) | string (timestamp) | Да |  |
| shops\[\].deliveryDateTo | Дата ближайшей доставки (до) | string (timestamp) | Да |  |
| shops\[\].redirectLink | Ссылка для перехода на внешний ресурс партнёра |  |  |  |
| first | Флаг того, что страница первая | boolean | Да |  |
| last | Флаг того, что страница последняя | boolean | Да |  |
| page | Номер страницы | number | Да |  |
| size | Размер страницы | number | Да |  |

**Пример успешного ответа**  
200 \- OK

{  
  "shops": \[  
    {  
      "name": "METRO",  
      "linkImage": "string",  
      "deliveryDateFrom": "2026-04-10 21:00:00",  
      "deliveryDateTo": "2026-04-10 23:00:00",  
      "redirectLink": "string"  
    }  
  \],  
  "first": true,  
  "last": false,  
  "page": 0,  
  "size": 10  
}

**Задание 3: архитектура**

![][image1]

[image1]: <data:image/png;base64,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>