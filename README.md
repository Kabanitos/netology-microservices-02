# Домашнее задание к занятию «Микросервисы: принципы»

Вы работаете в крупной компании, которая строит систему на основе микросервисной архитектуры.
Вам как DevOps-специалисту необходимо выдвинуть предложение по организации инфраструктуры для разработки и эксплуатации.

## Задача 1: API Gateway 

Предложите решение для обеспечения реализации API Gateway. Составьте сравнительную таблицу возможностей различных программных решений. На основе таблицы сделайте выбор решения.

Решение должно соответствовать следующим требованиям:
- маршрутизация запросов к нужному сервису на основе конфигурации,
- возможность проверки аутентификационной информации в запросах,
- обеспечение терминации HTTPS.

Обоснуйте свой выбор.
## Ответ
| Характеристика/Решение | Kong | Nginx | Traefik |
|:-----------------------|:------------:|:--------:|:----:|
| Маршрутизация запросов на основе конфигурации | Да, с поддержкой плагинов | Да, конфигурируется через NGINX config | Да, динамическая маршрутизация |
| Возможность проверки аутентификационной информации | Да, через плагины (например, OAuth2, JWT) | Да, с использованием модулей (например, JWT, Basic Auth) | Да, с использованием middleware (например, JWT, Basic Auth) |
| обеспечение терминации HTTPS | Да, поддержка SSL/TLS | Да, конфигурация SSL/TLS в настройках | Да, автоматическая поддержка SSL | 

На основе выше перечисленных требований, мой выбор пал на  Kong. 
- **Маршрутизация запросов:** Kong поддерживает динамическую маршрутизацию и управление API, что позволяет легко настраивать маршруты на основе конфигурации;
- **Аутентификация:** Kong  предоставляет множество плагинов для аутентификации;
- **Простота настрйкии**  Kong имеет хорошую документацию;
- **Терминация HTTPS:**  Kong имеет встроенную поддержку SSL/TLS для терминации HTTPS, что позволяет безопасно обрабатывать HTTPS-запросы.

## Задача 2: Брокер сообщений

Составьте таблицу возможностей различных брокеров сообщений. На основе таблицы сделайте обоснованный выбор решения.

Решение должно соответствовать следующим требованиям:
- поддержка кластеризации для обеспечения надёжности,
- хранение сообщений на диске в процессе доставки,
- высокая скорость работы,
- поддержка различных форматов сообщений,
- разделение прав доступа к различным потокам сообщений,
- простота эксплуатации.

Обоснуйте свой выбор.

## Ответ

| Характеристика/Решение | Apache Kafka | RabbitMQ | NATS |
|:-----------------------|:------------:|:--------:|:----:|
| Кластеризация          |  Есть | Есть | Есть |
| Хранение сообщений на диске | Хранение сообщений на диске по умолчанию с возможностью конфигурации. | Хранение сообщений на диске по умолчанию, возможность настройки сроков хранения. | Сообщения хранятся в памяти, но поддержка журналирования в случае необходимости. |
| Высокая скорость работы | Очень высокая  производительность для обратботки больших объемов данных | Высокая производительность для небольших и средних нагрузок, есть  поддержка очередей. | Очень высокая скорость для обработки небольших сообщений с минимальными задержками. |
| Поддержка различных форматов сообщений | Поддерживает произвольные форматы сообщений через сериализацию (например, Avro, JSON, Protobuf). | Поддержка JSON, XML, и любых текстовых форматов через каналы и очереди. |  Поддержка JSON, строки и бинарных сообщений. |
| Разделение прав доступа | Поддержка ACL и интеграции с внешними системами безопасности. | Поддержка механизмов аутентификации и авторизации, с возможностью настройки ролей. | Основная система безопасности ограничена, поддержка аутентификации через токены и механизмы шифрования. |
| Простота эксплуатации | Сложная настройка и эксплуатация, требуется опыт для настройки | Простая настройка, имеется WEb-консоль управления, поддержка гибких настроек | Легкая настройка и управление, ориентирован на низкую задержку и простоту.| 

Мой выбор: RabbitMQ
- **Поддержка кластеризации:** RabbitMQ поддерживает кластеризацию и отказоустойчивость, что позволяет обеспечить надежную работу системы в случае сбоев.
- **Хранение сообщений на диске:** Сообщения могут храниться на диске, что гарантирует надежность и возможность восстановления данных в случае сбоев.
- **Высокая скорость работы:** Несмотря на то, что RabbitMQ уступает Kafka в скорости обработки больших данных, для большинства приложений с нормальной нагрузкой он работает достаточно быстро.
- **Поддержка различных форматов сообщений:** RabbitMQ поддерживает множество форматов сообщений, что дает гибкость при интеграции с различными системами.
- **Разделение прав доступа:** RabbitMQ поддерживает механизм аутентификации и авторизации с использованием ролей, что позволяет гибко разделять права доступа к различным потокам сообщений.
- **Простота эксплуатации:** RabbitMQ имеет удобную веб-консоль для настройки и мониторинга, что упрощает эксплуатацию и уменьшает время на настройку системы.

