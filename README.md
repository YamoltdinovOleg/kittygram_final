# Kittygram_final

[![Main Kittygram workflow](https://github.com/yamoltdinovoleg/kittygram_final/actions/workflows/main.yml/badge.svg)](https://github.com/yamoltdinovoleg/kittygram_final/actions)

**Kittygram** — это веб-приложение для создания и управления профилями котиков. Пользователи могут добавлять своих питомцев, загружать их фотографии, указывать достижения и делиться информацией о своих любимцах.

## ✨ Основные функции

- �� **Управление профилями котиков** — создание, редактирование и удаление профилей
- 📸 **Загрузка фотографий** — поддержка изображений в формате Base64
- 🏆 **Система достижений** — добавление и управление достижениями котиков
- �� **Цветовая палитра** — выбор цвета котика из предустановленной палитры
- 👤 **Аутентификация пользователей** — регистрация и авторизация
- 📱 **Адаптивный дизайн** — удобное использование на всех устройствах
- �� **Безопасность** — защищенные API endpoints с токенной аутентификацией

## 🛠 Технологический стек

### Backend
- **Python 3.8+** — основной язык программирования
- **Django 3.2.3** — веб-фреймворк
- **Django REST Framework 3.12.4** — API
- **PostgreSQL 13.10** — база данных
- **Djoser 2.1.0** — аутентификация
- **Pillow 9.0.0** — обработка изображений
- **psycopg2-binary 2.9.3** — драйвер PostgreSQL

### Frontend
- **React 17.0.2** — пользовательский интерфейс
- **React Router DOM 5.3.0** — маршрутизация
- **CSS Modules** — стилизация компонентов

### DevOps & Infrastructure
- **Docker & Docker Compose** — контейнеризация
- **Nginx** — веб-сервер и reverse proxy
- **GitHub Actions** — CI/CD
- **Docker Hub** — реестр образов

## 🚀 Развертывание проекта

### Локальная разработка

1. **Клонируйте репозиторий:**
   ```bash
   git clone https://github.com/yamoltdinovoleg/kittygram_final.git
   cd kittygram_final
   ```

2. **Настройте переменные окружения:**
   Создайте файл `.env` в корне проекта:
   ```env
   SECRET_KEY=your-secret-key-here
   DEBUG=True
   ALLOWED_HOSTS=localhost,127.0.0.1
   POSTGRES_DB=kittygram
   POSTGRES_USER=kittygram_user
   POSTGRES_PASSWORD=your-password
   DB_HOST=localhost
   DB_PORT=5432
   ```

3. **Запустите с помощью Docker Compose:**
   ```bash
   docker-compose up --build
   ```

4. **Выполните миграции:**
   ```bash
   docker-compose exec backend python manage.py migrate
   docker-compose exec backend python manage.py collectstatic --noinput
   ```

5. **Создайте суперпользователя:**
   ```bash
   docker-compose exec backend python manage.py createsuperuser
   ```

### Продакшн развертывание

1. **Настройте сервер:**
   - Установите Docker и Docker Compose
   - Настройте доменное имя
   - Получите SSL сертификат

2. **Настройте переменные окружения для продакшна:**
   ```env
   SECRET_KEY=your-production-secret-key
   DEBUG=False
   ALLOWED_HOSTS=yourdomain.com,www.yourdomain.com
   POSTGRES_DB=kittygram_prod
   POSTGRES_USER=kittygram_prod_user
   POSTGRES_PASSWORD=strong-production-password
   DB_HOST=localhost
   DB_PORT=5432
   ```

3. **Запустите продакшн версию:**
   ```bash
   docker-compose -f docker-compose.production.yml up -d
   ```

## 🔧 Настройка переменных окружения

### Обязательные переменные

| Переменная | Описание | Пример |
|------------|----------|---------|
| `SECRET_KEY` | Секретный ключ Django | `django-insecure-...` |
| `DEBUG` | Режим отладки | `True` / `False` |
| `ALLOWED_HOSTS` | Разрешенные хосты | `localhost,127.0.0.1` |
| `POSTGRES_DB` | Имя базы данных | `kittygram` |
| `POSTGRES_USER` | Пользователь БД | `kittygram_user` |
| `POSTGRES_PASSWORD` | Пароль БД | `strong-password` |
| `DB_HOST` | Хост БД | `localhost` |
| `DB_PORT` | Порт БД | `5432` |

### Переменные для CI/CD

Для автоматического развертывания добавьте в секреты GitHub:

- `DOCKER_USERNAME` — логин Docker Hub
- `DOCKER_PASSWORD` — пароль/токен Docker Hub
- `HOST` — IP адрес сервера
- `USER` — пользователь сервера
- `SSH_KEY` — приватный SSH ключ
- `SSH_PASSPHRASE` — пароль SSH ключа
- `TELEGRAM_TOKEN` — токен Telegram бота
- `TELEGRAM_TO` — ID для уведомлений

## 📁 Структура проекта
kittygram_final/
├── backend/ # Django backend
│ ├── cats/ # Приложение котиков
│ ├── kittygram_backend/ # Настройки Django
│ ├── manage.py
│ └── requirements.txt
├── frontend/ # React frontend
│ ├── src/
│ │ ├── components/ # React компоненты
│ │ └── utils/ # Утилиты
│ └── package.json
├── nginx/ # Конфигурация Nginx
├── docker-compose.yml # Локальная разработка
├── docker-compose.production.yml # Продакшн
└── kittygram_workflow.yml # GitHub Actions

## 🧪 Тестирование

### Локальное тестирование

```bash
# Backend тесты
cd backend
python manage.py test

# Frontend тесты
cd frontend
npm test

# Линтинг
python -m flake8 backend/
```

### Автоматическое тестирование

Проект использует GitHub Actions для автоматического тестирования:
- Тесты запускаются на каждое изменение в любой ветке
- Поддерживаются версии Python: 3.8, 3.9, 3.10
- Проверяется код с помощью flake8
- Выполняются Django и React тесты

## �� API Endpoints

### Аутентификация
- `POST /api/auth/users/` — регистрация
- `POST /api/auth/token/login/` — авторизация
- `POST /api/auth/token/logout/` — выход

### Котики
- `GET /api/cats/` — список котиков
- `POST /api/cats/` — создание котика
- `GET /api/cats/{id}/` — детали котика
- `PUT /api/cats/{id}/` — обновление котика
- `DELETE /api/cats/{id}/` — удаление котика

### Достижения
- `GET /api/achievements/` — список достижений
- `POST /api/achievements/` — создание достижения

## 👨‍💻 Автор

**yamoltdinovoleg** — разработчик проекта Kittygram

## 📄 Лицензия

Этот проект создан в рамках учебной программы Яндекс.Практикум.

---

**Доступ к репозиторию предоставлен пользователю Port-tf для просмотра.**