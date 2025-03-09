## Задание 1: Развёртывание PostgreSQL в виртуальной машине

1. Установил виртуальную машину c images:ubuntu 24.04 используя incus:
   ```sh
   incus launch images:ubuntu/24.04 ubuntu-vm --vm
   ```
2. Установлена и настроена PostgreSQL (так как после запуска shell в виртуальной машине мы сразу лоигимся пользователем root, sudo не нужно):
   ```sh
   apt update
   apt install postgresql
   ```
3. Проверена работа сервера командой:
   ```sh
   systemctl status postgresql
   ```

## Задание 2: Заливка базы данных из архива

1. Заходим под пользователем postgres (перед этим установил wget)
   ```sh
   su postgres
   ```
2. Выполнил команду из git репозитория
   ```sh
   wget https://storage.googleapis.com/thaibus/thai_small.tar.gz && tar -xf thai_small.tar.gz && psql < thai.sql
   ```

## Задание 3: Подсчёт количества записей в таблице

1. Подключение к базе данных:
   ```sh
   psql
   ```
2. Выполнение SQL-запроса
   ```sql
   SELECT * FROM book.tickets;
   ```
   привело к падению psql, виртуальной машине не хватило оперативной памяти (1 GB), процесс был убит OOM-killer:
   ```
   [Sun Mar  9 15:02:30 2025] Out of memory: Killed process 3382 (psql) total-vm:780832kB, anon-rss:728320kB, file-rss:128kB, shmem-rss:0kB, UID:103 pgtables:1524kB oom_score_adj:0

   ```
3. Выполнение SQL-запроса:
   ```sql
   SELECT count(*) FROM book.tickets;
   ```
   ```
      count  
   ---------
    5185505
   ```

   
