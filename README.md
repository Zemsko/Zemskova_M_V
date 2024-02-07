 # Нормализация данных
Данные исходной таблицы transaction находились в
первой нормальной форме (1НФ) все атрибуты в таблице простые, но не соответствуют (2НФ) и (3НФ) 

Отношения будут соответствовать 2НФ, если сама БД находится в 1НФ, а каждый столбец, 
который не является ключом, зависит от первичного ключа.


Для приведения данных ко второй и третьей НФ таблицу transaction(ключ transaction_id)разделяю на три: 

	1)products_stock с ключом (stock_id) и полями: (product_record_id),(list_price),(standart_cost),
	где хранится информация о закупочной цене(standart_cost)
	и розничной цене(list_price) товара, поле (product_record_id) отображает значение записи бренда(brands) товара.
	
	2)customers (ключ customer_id )
	
	3)order_statuses (ключ order_name)

	
Исходную таблицу customers связала с таблицей transaction через ключ (customer_id)
А products_stock через ключ (record_id) связала с таблицей products, которая была дополнительно создана
	4)Таблица products (ключ record_id),содержит справочники:
	  
	   5)brands
	   6)product_lines
	   7)product_classes
	   8)product_size

Таким образом мы получили нормализацию по третьей нормальной форме (3НФ).
# Структура базы данных 
![Zemskova_diagram](https://github.com/Zemsko/Zemskova_M_V/assets/147048091/42ab7914-10ea-4747-ae24-789bbbc539fd)
