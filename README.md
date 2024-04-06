Запуск проекта Kittygram в контейнерах и CI/CD с помощью GitHub Actions.

Для локального запуска тестов создайте виртуальное окружение, установите в него зависимости из backend/requirements.txt и запустите в корневой директории проекта `pytest`.

- Проект Taski доступен по доменному имени, указанному в `tests.yml`.
- Проект Kittygram доступен по доменному имени, указанному в `tests.yml`.
- Пуш в ветку main запускает тестирование и деплой Kittygram, а после успешного деплоя вам приходит сообщение в телеграм.
- В корне проекта есть файл `kittygram_workflow.yml`.

Для запуска проекта через docker compose необходимо выполнить следующие команды:

-docker compose -f docker-compose.production.yml pull
# загружает последние версии образов
-docker compose -f docker-compose.production.yml up -d
# считывает конфигурацию из файла docker-compose.production.yml и запускает соответствующие сервисы в фоновом режиме
-docker compose -f docker-compose.production.yml exec backend python manage.py migrate
# выполняем миграции
-docker compose -f docker-compose.production.yml exec backend python manage.py collectstatic
# собираем статику
-docker compose -f docker-compose.production.yml exec backend cp -r /app/collected_static/. /backend_static/static/
# копируем статику в volume static
