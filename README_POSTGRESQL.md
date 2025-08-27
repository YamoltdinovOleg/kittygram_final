# Запуск Kittygram с PostgreSQL

## Быстрый старт

1. **Создайте файл .env:**
   ```bash
   cp env.example .env
   ```

2. **Запустите проект:**
   ```bash
   docker-compose up --build
   ```

3. **Выполните миграции (в новом терминале):**
   ```bash
   docker-compose exec backend python manage.py migrate
   ```

## Что настроено

- ✅ Django настроен для PostgreSQL
- ✅ Драйвер psycopg2 установлен
- ✅ python-dotenv добавлен для загрузки .env файла
- ✅ Docker Compose настроен
- ✅ Переменные окружения готовы
- ✅ load_dotenv() применен в settings.py

## Проверка работы

- Frontend: http://localhost:9000
- Backend API: http://localhost:9000/api/
- База данных: PostgreSQL в контейнере 