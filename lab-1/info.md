## Функциональные требования

* 1.Авторизация пользователя
* 2.Управление пользователями(CRUD)
* 3.Система ролей
+  User - роль пользователя, которая предоставляет возможность добавлять товары в корзину и удалять их оттуда, оформлять заказ на основании корзины, заказывать доставку товаров
+  Admin - роль администратора, которая предоставляет возможность редактировать информацию о товарах и даёт доступ к административной панели управления пользователями 
* 4.Журналирование действий пользователей(все CRUD действия пользователя) и администратора(все CRUD действия с сущностями бд)

## Список сущностей БД
### User - сущность пользователя
* Поля User:
+ id - идентификатор пользователя (int, PK, FK2, IDENTITY, UNIQUE, NOT NULL)
+ name - имя пользователя (varchar(20), NOT NULL)
+ last_name - фамилия пользователя (varchar(20), NOT NULL)
+ email - почтовый адрес пользователя (varchar(255), FK1, UNIQUE, NOT NULL)
+ password - пароль пользователя (varchar(20), NOT NULL)
+ country - Страна пользователя (varchar(20), NOT NULL)
+ role - роль пользователя (varchar(15), NOT NULL)

### Log - сущность лога действия пользователя
* Поля Order:
+ id - идентификатор лога (int, PK, IDENTITY, UNIQUE, NOT NULL)
+ user - имя пользователя БД, идентичное почтовому адресу пользователя сайта (varchar(255), FK1, UNIQUE, NOT NULL)
+ type - тип лога (varchar(20), NOT NULL)
+ representation - сообщение лога (varchar(128), NOT NULL)

### Product - сущность товара
* Поля Product:
+ id - идентификатор товара (int, PK, FK4, IDENTITY, UNIQUE, NOT NULL)
+ name - наименование товара (varchar(128), UNIQUE, NOT NULL)
+ price - цена товара (int, NOT NULL)
+ description - описание товара (varchar(2048), NULL)
+ image - ссылка на изображение товара (varchar(128), NULL)
+ category - категория товара (varchar(30), NULL)

### Cart - сущность корзины товаров пользователя
* Поля Cart:
+ id - идентификатор корзины (int, PK, FK3, IDENTITY, UNIQUE, NOT NULL)
+ user_id - идентификатор пользователя, которому принадлежит корзина (int FK2, IDENTITY, UNIQUE, NOT NULL)

### Cart_Item - сущность товара в корзине пользователя
* Поля Cart_Item:
+ id - идентификатор товара корзины (int, PK, IDENTITY, UNIQUE, NOT NULL)
+ cart_id - идентификатор корзины, к которой относится товар (int, FK3, IDENTITY, UNIQUE, NOT NULL)
+ product_id - идентификатор товара, который лежит в корзине (int, FK4, IDENTITY, UNIQUE, NOT NULL)
+ quantity - количество единиц товара в корзине (int, NOT NULL)

### Order - сущность заказа пользователя
* Поля Order:
+ id - идентификатор заказа (int, PK, FK5, IDENTITY, UNIQUE, NOT NULL)
+ user_id - идентификатор пользователя, которому принадлежит заказ (int, FK2, IDENTITY, UNIQUE, NOT NULL)
+ date - дата оформления заказа (date, NOT NULL)
+ total_price - итоговая цена заказа (int, NOT NULL)

### Order_Item - сущность товара в заказе пользователя
* Поля Cart_Item:
+ id - идентификатор товара корзины (int, PK, IDENTITY, UNIQUE, NOT NULL)
+ order_id - идентификатор заказа, к которому относится товар (int, FK5, IDENTITY, UNIQUE, NOT NULL)
+ product_id - идентификатор товара, который принадлежит заказу (int, FK4, IDENTITY, UNIQUE, NOT NULL)
+ quantity - количество единиц товара в заказе (int, NOT NULL)

### Delivery - сущность доставки товара
* Поля Delivery:
+ id - идентификатор доставки (int, PK, IDENTITY, UNIQUE, NOT NULL)
+ order_id - идентификатор заказа, к которому будет оформелна доставка (int, FK5, IDENTITY, UNIQUE, NOT NULL)
+ method - способ доставки товара (varchar(20), NOT NULL)
+ address - адрес заказчика (varchar(256), NOT NULL)
+ phone number - номер телефона заказчика (varchar(15), NOT NULL)
+ status - статус доставки (varchar (30), NOT NULL)