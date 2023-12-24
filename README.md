# Database_Administration_for_DevOps_Engineers_HW_4

*PostgreSQL - Горбунов Д.Н.*

Задание 1.

```
version: '3.7'

services:
  postgres_new:
    image: postgres:12
    environment:
      - POSTGRES_PASSWORD=postgres
      - POSTGRES_PASSWORD=admin
    volumes:
      - /home/gorbunov/hw_postgres/db:/var/lib/postgres/data
      - /home/gorbunov/hw_postgres/backup:/var/postgres_backup
    ports:
      - 5432:5432
```
- Вывод список бд : ```\l```                
- Подключени к бд : ```\c```                    
- Вывод списка таблиц : ```\dt```                      
- Вывод описания содержимого таблиц : ```\dS+```                      
- выход из psql : ```\q```                         

Задание 2.

```create database test_databases;```                 
```psql -U postgres test_databases < test_dump.sql```            
```select attname, avg_width from pg_stats where tablename = 'orders' order by avg_width desc limit 1;```                
![вывод команды]()

Задание 3.

```begin;```              
```create table orders_expensive as select * from orders where price > 499;```             
```commit;```                   
![]()              
- Если при создание изначально таблицы - разибить ей на несколько используя функцию партиционирования и разбить данные по таблицам по нужным критериям               

Задание 4.

```pg_dump -U postgres test_databases > backup.sql```        
Добавим атрибут UNIQUE
```
CREATE TABLE public.orders (
    id integer NOT NULL,
    title character varying(80) UNIQUE NOT NULL,
    price integer DEFAULT 0
);
```
