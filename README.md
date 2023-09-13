# Процедура запуска автотестов

## Предварительные требования
Для запуска приложения на машине должно быть установленно следующее ПО:
* IntelliJ IDEA - Среда разработки и запуска програм написанных на различных языках.
* Docker Desktop - Приложение для скачивания и запуска контейнеров. Необходимо для запуска для установки и использования БД MySQL и PostgeSQL, а также эмулятора банковского сервиса.

## Запуск приложения

1. Необходимо склонировать репозиторий или скачать архив по [ссылке](https://github.com/SashaGracheva/QADiploma). 
2. Запустить необходимые базы данных MySQL и PostgreSQL, а также эмулятор банковского сервиса. Параметры для запуска хранятся в
   файле `docker-compose.yml`. Для запуска необходимо ввести в терминале IntelliJ IDEA команду:

 * `docker compose up`
3. Открыть отдельную вкладку в терминале и проверить запущенные контейнеры командой:

 * `docker container ls`
4. В новой вкладке терминала ввести следующую команду в зависимости от базы данных

 * `java "-Dspring.datasource.url=jdbc:mysql://localhost:3306/app" "-Dspring.datasource.username=app" "-Dspring.datasource.password=pass" -jar artifacts/aqa-shop.jar` - для MySQL
 * `java "-Dspring.datasource.url=jdbc:postgresql://localhost:5432/app" "-Dspring.datasource.username=app" "-Dspring.datasource.password=pass" -jar artifacts/aqa-shop.jar` - для PostgreSQL
5. Проверить доступность веб-сервиса  по адресу

 * `http://localhost:8080/`
 
 ## Запуск автотестов
1. Для запуска автотестов с "MySQL",  необходимо открыть новую вкладку терминала и ввести следующую команду:
 * `./gradlew test "-Ddb.url=jdbc:mysql://localhost:3306/app" "-Ddb.username=app" "-Ddb.password=pass"`
2. Для запуска автотестов с "PostgreSQL",  необходимо открыть новую вкладку терминала и ввести следующую команду:
 * `./gradlew test "-Ddb.url=jdbc:postgresql://localhost:5432/app" "-Ddb.username=app" "-Ddb.password=pass"`
 
## Запуск отчета тестирования
Для запуска и просмотра отчета по результатам тестирования, с помощью "Allure", выполнить по очереди команды:

 * `./gradlew allureReport`
 * `./gradlew allureServe`
 
## Завершения работы Sut 
Для завершения работы SUT, необходимо в терминале, где был запущен SUT, ввести команду:

 * `Ctrl+C`
 
## Остановка и удаление контейнера
Для остановки работы контейнеров "Docker-Compose", необходимо ввести в терминал следующую команду:
 * `docker-compose down`
