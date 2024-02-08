 # Нормализация данных
 # Структура базы данных(https://github.com/Zemsko/Zemskova_M_V/assets/147048091/42ab7914-10ea-4747-ae24-789bbbc539fd)
Данные исходной таблицы transaction находятся в
первой нормальной форме (1НФ) все атрибуты в таблице простые.

Приведем таблицу ко воторой нормальной форме (2 Нф)
 

Отношения будут соответствовать (2НФ), если сама БД находится в (1НФ), а каждый столбец, 
который не является ключом, зависит от первичного ключа.


1) Таблица transaction, ключ (transaction_id) имеет поля :

	+ products_stock_id
	+ customer_id
	+ transaction_date
	+ online_oder
	+ order_status

Все поля таблицы transaction зависят от одного ключа (transaction_id)
Приведена таблица transaction ко 2НФ.
    
Отношение находится в 3НФ, когда находится во 2НФ и каждый не ключевой атрибут 
нетранзитивно зависит от первичного ключа.Правило требует выносить все не ключевые поля,
содержимое которых может относиться к нескольким записям таблицы в отдельные таблицы.
	
	Поле products_stock_id в таблице transactions ссылается на еще одну таблицу products_stock.
	
	Таким образом мы получили нормализацию из (2НФ) к третьей нормальной форме (3НФ).

	transaction -> products_stock_id -> products_stock 
	
2) Поле order_statuses (ключ status_name) ссылается на таблицу - справочник order_statuses 
	
Создала отдельную таблицу order_statuses. Привела к (3НФ)
    
	transaction -> order_statuses - > status_name	


3) Таблица products_stock с ключом (stock_id) приведена ко второй нормальной форме (2НФ) products_stock по ключу stock_id.
Все поля таблицы products_stock зависят от одного ключа (stock_id):
	
 	+ product_record_id
	+ list_price,
	+ standart_cost
				
4) Таблица customers (ключ customer_id ). Приведенаа ко второй нормальной форме (2НФ). Все поля таблицы customers зависят от одного ключа (customer_id):

	+ first_name
	+ last_name
	+ gender 
	+ DOB
	+ job_title
	+ job_industry_category
	+ wealth_segment
	+ deceased_indicator
	+ owns_car
	+ address
	+ postcode
	+ state
	+ country
	+ property_valuation
	
5)Таблица products (ключ record_id),содержит таблицы-справочники:
	  
	   6)brands
	   7)product_lines
	   8)product_classes
	   9)product_size
	   
Таким образом мы получили нормализацию по третьей нормальной форме (3НФ).

	   products -> brands          -> brand_name
	   products -> product_lines   -> product_line
	   products -> product_classes -> product_class
	   products -> product_sizes   -> product_size
# Структура базы данных 
![Zemskova_diagram](https://github.com/Zemsko/Zemskova_M_V/assets/147048091/42ab7914-10ea-4747-ae24-789bbbc539fd)
