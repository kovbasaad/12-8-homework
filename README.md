# Домашнее задание к занятию 12.8. «Резервное копирование баз данных» - Ковбаса Анна

### Задание 1. Резервное копирование

### Кейс
Финансовая компания решила увеличить надёжность работы баз данных и их резервного копирования. 

Необходимо описать, какие варианты резервного копирования подходят в случаях: 

1.1. Необходимо восстанавливать данные в полном объёме за предыдущий день.
  
&nbsp;&nbsp;&nbsp;&nbsp;Ежедневное холодное инкрементное резервирование, еженедельное полное

1.2. Необходимо восстанавливать данные за час до предполагаемой поломки.
 
 Горячее инкрементное резервирование каждый час, полное резервирование раз в три дня

1.3.* Возможен ли кейс, когда при поломке базы происходило моментальное переключение на работающую или починенную базу данных.
  
  Да, при использовании репликации master-master


---

### Задание 2. PostgreSQL

2.1. С помощью официальной документации приведите пример команды резервирования данных и восстановления БД (pgdump/pgrestore).
копирование БД dbname:
```
pg_dump dbname > dumpfile
```

копирование таблицы table из БД dbname:
```
pg_dump dbname -t table > dumpfile
```

восстановление БД dbname с остановкой в случае ошибки:
```
psql --set ON_ERROR_STOP=on dbname < dumpfile 
```

---

### Задание 3. MySQL

3.1. С помощью официальной документации приведите пример команды инкрементного резервного копирования базы данных MySQL. 
```
 mysqlbackup --defaults-file=/path/to/dbconf/db.cnf --incremental --backup-dir=/path/to/backups \
 backup
```
3.1.* В каких случаях использование реплики будет давать преимущество по сравнению с обычным резервным копированием?
  В случае отсутсвия времени на восстановление данных, можно мнгвовенно переключиться на рабочую реплику БД

