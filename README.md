# Домашнее задание Сартисона Евгения №8
Задание: Развернуть Managed PostgreSQL в Yandex Cloud

## **(1) Создать кластер**

### В каталоге выбрать Managed Service for PostgreSQL
![image](https://github.com/user-attachments/assets/59172540-c585-48fb-8dd7-2bfc1127cf4f)

### Ресурсы: 1 vCPU, 1 ГБ RAM
Минимальные ресурсы, что позволяет выбрать YC 4Gb Ram и 2 СPU, как в задании насторйки по ресурсам выполнить нельзя.
![image](https://github.com/user-attachments/assets/cfb1cac9-9caa-446b-9717-ebba226d618e)


### Выбрал следующую конфигурация
![image](https://github.com/user-attachments/assets/3138052b-9367-4559-b0c6-161a73647826)

### Создал Postgres cluster со следующими настройками

![image](https://github.com/user-attachments/assets/499da419-5137-4cdf-9d2b-955323a2cbed)




### Разрешить доступ с вашего IP
(a) Создал группу безопасности testgroup
![image](https://github.com/user-attachments/assets/7aefdd50-b3c8-4c11-9d34-191f8a63fcc8)

(б) добавил правило, чтобы мог подключаться со своей машины
![image](https://github.com/user-attachments/assets/8cf72197-963c-4ed3-9550-ee758f6d5483)

Для генерации CIDR использовал сайт https://www.ipaddressguide.com/cidr

(в) Добавление сертификата на локальную машину
```
student:~$ wget "https://storage.yandexcloud.net/cloud-certs/CA.pem" \
    --output-document ~/.postgresql/root.crt && \
chmod 0600 ~/.postgresql/root.crt
--2025-06-29 20:55:14--  https://storage.yandexcloud.net/cloud-certs/CA.pem
Resolving storage.yandexcloud.net (storage.yandexcloud.net)... 213.180.193.243, 2a02:6b8::1d9
Connecting to storage.yandexcloud.net (storage.yandexcloud.net)|213.180.193.243|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 3579 (3,5K) [application/x-x509-ca-cert]
Saving to: ‘/home/student/.postgresql/root.crt’

/home/student/.postgresql/root.crt              100%[=====================================================================================================>]   3,50K  --.-KB/s    in 0s      

2025-06-29 20:55:14 (1,63 GB/s) - ‘/home/student/.postgresql/root.crt’ saved [3579/3579]
```






## **(2) Подключиться через psql**

### С локальной машины подключился под esartisonuser к базе esartisondb
```
student:~$ psql "host=rc1a-jia19cml2a2aqiof.mdb.yandexcloud.net,rc1d-g0u6e98gs55897fe.mdb.yandexcloud.net \
    port=6432 \
    sslmode=verify-full \
    dbname=esartisondb \
    user=esartisonuser \
    target_session_attrs=read-write"
Password for user esartisonuser: 
psql (17.5 (Ubuntu 17.5-1.pgdg22.04+1))
SSL connection (protocol: TLSv1.3, cipher: TLS_AES_256_GCM_SHA384, compression: off, ALPN: none)
Type "help" for help.

esartisondb=> 
```

### Проверить работоспособность кластера
(a) создал таблицу на мастере
![image](https://github.com/user-attachments/assets/7eb4d7e0-2c21-4902-ba33-03aa41121b9b)
![image](https://github.com/user-attachments/assets/353a3b02-f7f6-4195-a753-a1d4f0310ac2)

(б) проверить таблицу на реплике
![image](https://github.com/user-attachments/assets/4ba09501-6c6a-4c06-9442-60ef6aae55d4)
Данные на реплике есть

(в) проверка графиков
![image](https://github.com/user-attachments/assets/d74b6059-8e8b-4037-a326-0a14bc64d2ee)

Все в рабочем состоянии.



## **(3) Задокументировать шаги**

### Параметры кластера
![image](https://github.com/user-attachments/assets/499da419-5137-4cdf-9d2b-955323a2cbed)

### Команда подключения

### Пример выполненного запроса


# Задание со звездочкой # 

★ Автомасштабирование: Настроить auto-scaling для обработки пиковых нагрузок

★ Коллективный доступ: Добавить IP коллеги в белый список


# Критерии оценки:#

✅ Кластер создан с минимальными параметрами

✅ Успешное подключение через psql

✅ Полная документация в README.md
