# Создание БД. Установка и настройка PostGis

**Заходим под пользователем postgres**

`sudo -u postgres psql`


**Создаем новую БД**

`CREATE DATABASE myproject;`

------------------------------------------------------------------------------------------------------------

**Создаем нового пользователя**

`CREATE USER myprojectuser WITH PASSWORD 'difficultpassword';`

------------------------------------------------------------------------------------------------------------

**Прописываем ролли**

`ALTER ROLE myprojectuser SET client_encoding TO 'utf8';`

`ALTER ROLE myprojectuser SET default_transaction_isolation TO 'read committed';`

`ALTER ROLE myprojectuser SET timezone TO 'UTC';`

`GRANT ALL PRIVILEGES ON DATABASE myproject TO myprojectuser;`

`\q`

------------------------------------------------------------------------------------------------------------

**Устанавливаем в базу расширение postgis**

`sudo -u postgres psql -c 'CREATE EXTENSION postgis;' myproject`

------------------------------------------------------------------------------------------------------------

**Проверяем установку PostGIS**

`psql -d myproject -U myprojectuser -c "SELECT PostGIS_Full_Version();"`


------------------------------------------------------------------------------------------------------------


**Прописываем в файл /etc/postgresql/9.5/main/pg_hba.conf права доступа к базе данных с удаленных хостов**

`host all myprojectuser somehost/32 md5`

------------------------------------------------------------------------------------------------------------

**Перезагружаем postgres**

`sudo systemctl restart postgresql`
