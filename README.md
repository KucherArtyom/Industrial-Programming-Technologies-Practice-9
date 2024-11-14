# Industrial-Programming-Technologies-Practice-9 (ЭФМО-02-24 Кучер Артем Сергеевич)
## Таблицы интернет-магазина электронники
### Таблица "Покупатели" (Сustomers)
```
CREATE TABLE customers (
  id SERIAL PRIMARY KEY,
  name varchar(20),
  surname varchar(20),
  patronymic varchar(20),
  telephone text,
  card_number varchar(16),
  mail varchar(100),
  password varchar(100)
);
```
### Таблица "Адреса" (Addresses)
```
CREATE TABLE addresses (
  id SERIAL PRIMARY KEY,
  customer_id integer,
  country varchar(100),
  city varchar(100),
  street varchar(255),
  house integer,
  FOREIGN KEY (customer_id) REFERENCES customers (id)
);
```
### Таблица "Категории" (Сategories)
```
CREATE TABLE сategories (
  id SERIAL PRIMARY KEY,
  name varchar(100)
);
```
### Таблица "Производители" (Manufacturers)
```
CREATE TABLE manufacturers (
  id SERIAL PRIMARY KEY,
  name varchar(100),
  country varchar(100)
);
```
### Таблица "Товары" (Products)
```
CREATE TABLE products (
  id SERIAL PRIMARY KEY,
  manufacturer_id integer,
  category_id integer,
  name varchar(100),
  price integer,
  quantity integer,
  article_number text,
  description text,
  image_url varchar(255),
  FOREIGN KEY (manufacturer_id) REFERENCES manufacturers (id),
  FOREIGN KEY (category_id) REFERENCES сategories (id)
);
```
### Таблица "Заказы" (Orders)
```
CREATE TABLE orders (
  id integer PRIMARY KEY,
  order_date date,
  order_time time,
  customer_id integer,
  FOREIGN KEY (customer_id) REFERENCES customers (id)
);
```
### Таблица "Обзоры" (Reviews)
```
CREATE TABLE reviews (
  id integer PRIMARY KEY,
  customer_id integer,
  product_id integer,
  date_review timestamp,
  review_text text,
  rating integer,
  FOREIGN KEY (customer_id) REFERENCES customers (id),
  FOREIGN KEY (product_id) REFERENCES products (id)
);
```
### Таблица "Любимое" (Favorites)
```
CREATE TABLE favorites (
  id integer PRIMARY KEY,
  product_id integer,
  customer_id integer,
  FOREIGN KEY (product_id) REFERENCES products (id),
  FOREIGN KEY (customer_id) REFERENCES customers (id)
);
```
### Таблица "Поставщики" (Providers)
```
CREATE TABLE providers (
  manufacturer_id integer,
  product_id integer,
  FOREIGN KEY (manufacturer_id) REFERENCES manufacturers (id),
  FOREIGN KEY (product_id) REFERENCES products (id)
);
```
### Таблица "Корзины" (Baskets)
```
CREATE TABLE baskets (
  id integer PRIMARY KEY,
  customer_id integer,
  FOREIGN KEY (customer_id) REFERENCES customers (id)
);
```
### Таблица "Доставки" (Deliveries)
```
CREATE TABLE deliveries (
  id integer PRIMARY KEY,
  order_id integer,
  address_id integer,
  status varchar(50),
  send_date date,
  expected_receive_date date,
  FOREIGN KEY (order_id) REFERENCES orders (id),
  FOREIGN KEY (address_id) REFERENCES addresses (id)
);
```
### Таблица "Продукты-заказы" (Product_Order)
```
CREATE TABLE product_order (
  product_id integer,
  order_id integer,
  FOREIGN KEY (product_id) REFERENCES products (id),
  FOREIGN KEY (order_id) REFERENCES orders (id)
);
```
### Таблица "Продукты-корзины" (Product_Basket)
```
CREATE TABLE product_basket (
  product_id integer,
  basket_id integer,
  FOREIGN KEY (product_id) REFERENCES products (id),
  FOREIGN KEY (basket_id) REFERENCES baskets (id)
);
```
### Заполнение таблиц данными
```
INSERT INTO categories VALUES
("Консоль"),
("Телефон"),
("Ноутбук")

INSERT INTO manufacturers VALUES
("Samsung", "Южная Корея"),
("Xiaomi", "Китай"),
("Asus", "Тайвань")
("Nintendo", "Япония"),
("Apple", "США"),
("Sony", "Япония")
("Microsoft", "США"),
("Realme", "Китай"),
("Lenovo", "Китай")

INSERT INTO products VALUES
(1, 2, "Samsung Galaxy S24", 8000, 10, 8100, "Samsung Galaxy S24 — компактный смартфон из флагманской линейки, получивший мощный фирменный процессор, большой объем оперативной памяти, узнаваемый дизайн и продуманную эргономику. ", "https://ir.ozone.ru/s3/multimedia-m/c1000/6900636406.jpg"),
(1, 2, "Samsung Galaxy S23 FE", 36000, 50, 7100, "Смартфон Samsung Galaxy S23 FE - это новейшее устройство от известного южнокорейского производителя Samsung. Он предлагает пользователям высокую производительность и отличные функциональные возможности.", "https://img.championat.com/i/d/o/168794395937683540.jpg"),
(2, 2, "Смартфон Xiaomi 14 Ultra 16+512", 105000, 12, 5300, "Xiaomi 14 Ultra - это мощный смартфон, который предлагает потрясающие возможности и инновационные функции.", "https://avatars.mds.yandex.net/get-mpic/3927509/2a000001921f74346bd8d44a81de4eb9b55a/optimize"),
(2, 2, "Смартфон Xiaomi 15 16/512 GB", 90000, 20, 1000, "Xiaomi 15 Leica Оптический светосильный объектив Summilux: смартфон оснащен светосильным объективом Summilux, который обеспечивает высокое качество изображения при слабом освещении.", "https://avatars.mds.yandex.net/get-mpic/7979606/2a0000019324bec6606ec12c7afaff1a42db/optimize"),
(3, 3, "Asus TUF Gaming A15", 85000, 10, 1100, "Игровой ноутбук ASUS TUF Gaming A15 FA507NU-LP141 обеспечивает впечатляющую производительность для игр и других задач.", "https://avatars.mds.yandex.net/i?id=a03c8b88bfe7858a4bfea3daa18d8fcf_l-6998621-images-thumbs&n=13"),
(3, 3, "Asus ROG Zephyrus G15", 5000, 5, 19000, "Мощный и портативный, ноутбук ROG Zephyrus G15 представляет собой игровую платформу на базе операционной системы Windows 10, выполненную в ультратонком корпусе весом всего 1,9 кг.", "https://static.onlinetrade.ru/img/items/m/noutbuk_asus_rog_zephyrus_m15_gu502lv_az105t_15.6_fhd_ag_ips_240hz_i7_10750h_16gb_1024gb_ssd_nodvd_rtx_2060_6gb_w10_black_1459559_3.jpg"),
(3, 3, "Asus Vivobook 17", 41500, 12, 900, "ASUS Vivobook 17 X1704ZA-AU341 90NB10F2-M00DD0 — производительный ноутбук в ударопрочном корпусе с активной системой охлаждения.", "https://avatars.mds.yandex.net/i?id=b40b973a43129287ac2cfdb6ff688283_l-6458590-images-thumbs&n=13"),
(8, 2, "Смартфон realme 12 4G 8/128 ГБ", 15000, 25, 3400, "Представляем вашему вниманию смартфон Realme 12 4G. Это устройство, которое сочетает в себе передовые технологии и стильный дизайн.", "https://avatars.mds.yandex.net/get-mpic/11368570/img_id7939120996924950339.jpeg/optimize"),
(9, 1, "Игровая консоль Lenovo Legion Go 512 ГБ", 70000, 50, 9000, "Оцените непревзойденную универсальность Legion Go — мощного игрового инструмента. В режиме портативного устройства ваш любимый карманный гаджет превращается в мощный игровой ПК, отлично подходящий для игры в дороге.", "https://avatars.mds.yandex.net/get-mpic/11483862/2a0000019031f150b00fd4c083d7733d6fb4/optimize"),
(5, 3, "Apple MacBook Air 13 Retina", 65000, 10, 7900, "Самый тонкий и лёгкий ноутбук Apple MacBook Air 13 model: A2337 теперь стал суперсильным благодаря чипу Apple M1.", "https://msk.aura-rent.ru/wp-content/uploads/2020/02/noutbook-air-2.2.jpg"),	
(5, 3, "Apple MacBook Pro 14 2023", 135000, 7, 14100, "Ноутбук Apple Macbook Pro 14 M3 8/512 Silver (MR7J3) – мощный и стильный помощник для работы и развлечений.", "https://mtscdn.ru/upload/iblock/ee8/mbp14_silver_gallery7_202301.jpg"),
(4, 1, "Nintendo Switch OLED", 25500, 20, 16700, "Консоль Nintendo Switch OLED с красочным 7-дюймовым экраном. При практически одинаковых размерах с Nintendo Switch консоль Nintendo Switch OLED отличается более крупным 7-дюймовым OLED-экраном с глубокими цветами и высоким контрастом.", "https://cdn1.ozone.ru/s3/multimedia-s/6080757748.jpg"),
(6, 1, "Sony PlayStation 5 Slim", 47000, 16, 4500, "Игровая приставка Sony PlayStation 5 Slim: улучшенный дизайн и расширенные возможности хранения данных Обновленная версия популярной консоли PlayStation 5", "https://appmistore.ru/upload/iblock/c4e/25bnswfucwuectbrw1s9vlgvr4bkswud.webp"),
(7, 1, "Microsoft Xbox Series S", 34000, 25, 19300, "Игровая консоль Microsoft Xbox Series S рассчитана на использование игр, загружаемых из цифровой библиотеки. ", "https://media.wired.co.uk/photos/606d9dbb20fc96acca6d3a5a/1:1/w_2000,h_2000,c_limit/3.jpg"},
(7, 1, "Microsoft Xbox Series X 1000 ГБ SSD", 57000, 40, 56000, "XBOX Series X – самая мощная консоль от Microsoft девятого поколения игровых платформ, получившая небывалые ранее характеристики и производительность.", "https://avatars.mds.yandex.net/get-mpic/11620615/2a000001923d73058e1cf45e21c0fec54cdf/optimize")
```
