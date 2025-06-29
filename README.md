# Домашнее задание Сартисона Евгения №8
Задание: Развернуть Managed PostgreSQL в Yandex Cloud

**(1) Создать кластер**
В каталоге выбрать Managed Service for PostgreSQL
![image](https://github.com/user-attachments/assets/59172540-c585-48fb-8dd7-2bfc1127cf4f)

Ресурсы: 1 vCPU, 1 ГБ RAM
Минимальные ресурсы, что позволяет выбрать YC 4Gb Ram и 2 СPU, как в задании насторйки по ресурсам выполнить нельзя.
![image](https://github.com/user-attachments/assets/cfb1cac9-9caa-446b-9717-ebba226d618e)

Выбрал следующую конфигурация
![image](https://github.com/user-attachments/assets/3138052b-9367-4559-b0c6-161a73647826)




Разрешить доступ с вашего IP





**(2) Подключиться через psql**
Проверить работоспособность кластера
```

```
Установите сертификат:

mkdir -p ~/.postgresql && \
wget "https://storage.yandexcloud.net/cloud-certs/CA.pem" \
    --output-document ~/.postgresql/root.crt && \
chmod 0600 ~/.postgresql/root.crt

Установите зависимости:

sudo apt update && sudo apt install --yes postgresql-client

Подключитесь к базе данных:

psql "host=rc1a-gtqg0ak1h16m6ois.mdb.yandexcloud.net,rc1d-mihje4safpan7ivv.mdb.yandexcloud.net \
    port=6432 \
    sslmode=verify-full \
    dbname=esartisondb \
    user=esartisonuser \
    target_session_attrs=read-write"

После выполнения команды введите пароль пользователя для завершения процедуры подключения.

Для проверки успешности подключения выполните запрос:

SELECT version();

Подробнее о подключении к базе данных в кластере PostgreSQL см. в документации.



**(3) Задокументировать шаги**

Параметры кластера

Команда подключения

Пример выполненного запроса


# Задание со звездочкой # 

★ Автомасштабирование: Настроить auto-scaling для обработки пиковых нагрузок

★ Коллективный доступ: Добавить IP коллеги в белый список


# Критерии оценки:#

✅ Кластер создан с минимальными параметрами

✅ Успешное подключение через psql

✅ Полная документация в README.md
