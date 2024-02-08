 # Нормализация данных 
 # Структура базы данных

Данные исходных таблиц transaction и customer исследовала на предмет соответствия условиям первой (1НФ), второй (2НФ), третьей (3НФ) нормальных форм.


**Условия для 1НФ:**

1. В каждой ячейке таблицы хранится строго атомарное значение. Значение, не имеющее признаков составного и не являющееся массивом или списком в любом виде.
2. В рамках одного столбца таблицы хранятся данные одного типа.
3. В таблице нет дублирующихся строк, нарушающих реляционные принципы хранения данных.
   
В таблицах transaction и customer все атрибуты  атомарные, кроме вызвавшего подозрения поля адреса у customer, так как на примере "12 335-avenu" видно, что номер дома и наименование улицы не хранятся раздельно. Однако, в некоторых случаях бизнесу не требуется приведение хранимых данных в идеальный теоретический вид.
В рамкках одного столбца хранятся данные одного типа. В некоторых строках отсутствует информация об исходном товаре, но есть цена. 


**Выводы по 1НФ:** Обе исходные таблицы находятся в первой нормальной форме, так как удовлетворяют требованиям, предъявляемым к структуре таблиц в теории реляционных баз данных.


**Условия для 2НФ:**

1. Таблица должна находиться в 1 НФ (условие выполняется, с учетом результатов предыдущего параграфа)
2. Таблица должна иметь ключ, - столбец или набор столбцов, по которым гарантированно можно отличить строки друг от друга. По ключу мы можем обратиться к конкретной строке данных в таблице.
3. В случае потенциального составного ключа, все неключевые столбцы должны зависеть от полного ключа и не зависеть от его части.

Таблица должна иметь ключ. Выбираю наиболее подходящие кючевые атрибуты, таким оказался transaction_id. Данные этого столбца уникальны. Проверить это можно, если сгруппировать исходные данные по всем атрибутам кроме ключевого transaction_id и посчитать количество дубликатов, где количество повторений более одного.
В таблице customers имеет наиболее подходящий атрибут для ключа customer_id, который имеет возрастающие значения, а так же не уникален. Другие атрибуты таблицы нам не подходят, таккак имеют дубли.


**Выводы по 2НФ:** Обе исходные таблицы находятся во второй нормальной форме, так как удовлетворяют требованиям, предъявляемым к структуре таблиц в теории реляционных баз данных. Для таблицы transaction ключом является transaction_id, для customers - customer_id.


**Условия для 3НФ:**

1. Таблица должна находиться в 2 НФ (условие выполняется, с учетом результатов предыдущего параграфа)
2. Ни один неключевой атрибут не находится в транзитивной функциональной зависимости от потенциального ключа. Иными словами, в таблице не должно быть неключевых столбцов, которые бы зависели от других неключевых столбцов. Неключевые столбцы не должны пытаться играть роль ключа в таблице.

Правило требует выносить все не ключевые поля, содержимое которых может относиться к нескольким записям таблицы в отдельные таблицы. Вынесем атрибуты brand, product_line, product_class, product_size в отдельную таблицу продуктов с ключом record_id.

После данных преобразований исходная таблица transactions теряет из своего состава атрибут “product_id” и заменяет его на атрибут с внешним ключом “product_stock_id” ссылающийся на таблицу product_stock и ее атрибут stock_id.

Таблица products (ключ record_id) будет содержать таблицы-справочники:  
	
+ brands
+ product_lines
+ product_class
+ product_size
	   
Таким образом мы получили нормализацию по третьей нормальной форме (3НФ).

В результате преобразований таблица transaction с ключом (transaction_id) имеет поля :

+ product_stock_id
+ customer_id
+ transaction_date
+ online_oder
+ order_status

Поле products_stock_id в таблице transactions ссылается на еще одну таблицу products_stock.
	
transaction -> products_stock_id -> products_stock 
	
Поле order_statuses (ключ status_name) ссылается на таблицу - справочник order_statuses 
	    
transaction -> order_statuses - > status_name	


**Выводы по 3НФ** : Исходная таблица transaction подлежит нормализации путем введения двух дополнительных таблиц с продуктами products и их складским запасом product_stock, после чего структура удовлетворяет требованиям 3 НФ. Таблица customer по результату анализа уже находится в 3 НФ и не требует каких либо преобразований.

	

# Структура базы данных 
![Zemskova_diagram](https://github.com/Zemsko/Zemskova_M_V/assets/147048091/42ab7914-10ea-4747-ae24-789bbbc539fd)

Данные в таблицу подгружались из файлов transactions.csv и customers.scv используя возможности инструмента DBeaver. Скриншоты прилагаются.

![Screen1](https://github.com/Zemsko/Zemskova_M_V/assets/147048091/75f41a80-d337-41eb-bc37-030474e18566)
![Screen2](https://github.com/Zemsko/Zemskova_M_V/assets/147048091/b4e78017-dd5a-44d5-8493-a27826bc2f00)
![Screen3](https://github.com/Zemsko/Zemskova_M_V/assets/147048091/a2934c2a-2f91-4d45-b267-d00874d6e7cc)



