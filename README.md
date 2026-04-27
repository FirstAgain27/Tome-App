
---
# 📚 Tome App — Интернет-магазин книг

[![Django](https://img.shields.io/badge/Django-092E20?style=for-the-badge&logo=django&logoColor=white)](https://www.djangoproject.com/)
[![Django REST Framework](https://img.shields.io/badge/DRF-300000?style=for-the-badge&logo=django&logoColor=white)](https://www.django-rest-framework.org/)
[![Vue.js](https://img.shields.io/badge/Vue.js-4FC08D?style=for-the-badge&logo=vue.js&logoColor=white)](https://vuejs.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![JWT](https://img.shields.io/badge/JWT-000000?style=for-the-badge&logo=jsonwebtokens&logoColor=white)](https://django-rest-framework-simplejwt.readthedocs.io/)

Полноценное веб-приложение книжного интернет-магазина.  
Backend на Django REST Framework, frontend на Vue.js 3, JWT-аутентификация, корзина и оформление заказов.

---

## 🔥 Особенности

- 📖 **Каталог книг** — пагинация, фильтрация по категориям и авторам, полнотекстовый поиск
- 🛒 **Корзина** — добавление/удаление товаров, изменение количества
- 📦 **Заказы** — оформление заказа, история заказов пользователя
- 👤 **Аутентификация** — JWT-токены (access + refresh), регистрация, профиль, смена пароля
- 👨‍💼 **Админ-панель** — управление книгами, авторами, категориями, заказами
- 🎨 **Современный фронтенд** — Vue.js 3 + Pinia + Vue Router + Tailwind CSS
- 📡 **REST API** — ViewSet + APIView, вложенные сериализаторы, slug-based URL

---

## 🛠 Технологический стек

| Слой | Инструменты |
|------|-------------|
| **Backend** | Django 5, Django REST Framework |
| **Frontend** | Vue.js 3, Pinia, Vue Router, Axios, Tailwind CSS |
| **База данных** | PostgreSQL |
| **Аутентификация** | JWT (djangorestframework-simplejwt) |
| **API** | ViewSet, APIView, DefaultRouter, вложенные сериализаторы |

---

## 📁 Структура проекта

```
tome-app/
├── backend/
│   ├── apps/
│   │   ├── catalog/        # Книги, авторы, категории
│   │   ├── cart/           # Корзина и элементы корзины
│   │   ├── orders/         # Заказы
│   │   └── accounts/       # Пользователи, регистрация, JWT
│   ├── config/             # Настройки Django
│   └── manage.py
├── frontend/
│   ├── src/
│   │   ├── components/     # Переиспользуемые компоненты
│   │   ├── views/          # Страницы
│   │   ├── stores/         # Pinia-хранилища
│   │   ├── router/         # Маршрутизация
│   │   └── api/            # Axios-клиенты
│   └── package.json
└── README.md
```

---

## 🚀 Быстрый старт

### 1. Клонирование
```bash
git clone <repo-url>
cd tome-app
```

### 2. Backend
```bash
cd backend
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
python manage.py migrate
python manage.py runserver
```

### 3. Frontend
```bash
cd frontend
npm install
npm run dev
```

Приложение доступно на `http://localhost:5173`, API на `http://localhost:8000/api/v1/`.

---

## 📡 API Endpoints

### 🔐 Аутентификация
| Метод | URL | Описание |
|-------|-----|----------|
| `POST` | `/api/v1/accounts/register/` | Регистрация |
| `POST` | `/api/v1/accounts/login/` | Вход |
| `POST` | `/api/v1/accounts/logout/` | Выход |
| `GET` | `/api/v1/accounts/profile/` | Профиль |
| `PUT` | `/api/v1/accounts/profile/` | Обновление профиля |
| `POST` | `/api/v1/accounts/change-password/` | Смена пароля |
| `POST` | `/api/v1/accounts/token/refresh/` | Обновление токена |

### 📚 Каталог
| Метод | URL | Описание |
|-------|-----|----------|
| `GET` | `/api/v1/catalog/books/` | Список книг (пагинация, поиск, фильтр) |
| `POST` | `/api/v1/catalog/books/` | Добавить книгу |
| `GET` | `/api/v1/catalog/books/{slug}/` | Детали книги |
| `PUT` | `/api/v1/catalog/books/{slug}/` | Обновить книгу |
| `DELETE` | `/api/v1/catalog/books/{slug}/` | Удалить книгу |
| `GET` | `/api/v1/catalog/categories/` | Список категорий |
| `GET` | `/api/v1/catalog/authors/` | Список авторов |
| `GET` | `/api/v1/catalog/categories/{slug}/books/` | Книги по категории |
| `GET` | `/api/v1/catalog/authors/{slug}/books/` | Книги по автору |
| `GET` | `/api/v1/catalog/stats/` | Статистика каталога |

### 🛒 Корзина
| Метод | URL | Описание |
|-------|-----|----------|
| `GET` | `/api/v1/cart/` | Содержимое корзины |
| `POST` | `/api/v1/cart/items/` | Добавить товар |
| `PUT` | `/api/v1/cart/items/{id}/` | Обновить количество |
| `DELETE` | `/api/v1/cart/items/{id}/` | Удалить товар |

### 📦 Заказы
| Метод | URL | Описание |
|-------|-----|----------|
| `GET` | `/api/v1/orders/` | История заказов |
| `POST` | `/api/v1/orders/` | Создать заказ |

Swagger/ReDoc: [`http://localhost:8000/api/v1/docs`](http://localhost:8000/api/v1/docs)

---

## 🗄️ Модели данных

| Модель | Описание |
|--------|----------|
| `User` | Расширенная модель пользователя |
| `Book` | Книга (название, slug, цена, описание, обложка, автор, категория) |
| `Author` | Автор (имя, slug, биография) |
| `Category` | Категория (название, slug) |
| `Cart` | Корзина пользователя (OneToOne к User) |
| `CartItem` | Элемент корзины (книга, количество) |
| `Order` | Заказ (пользователь, адрес, статус) |
| `OrderItem` | Элемент заказа (книга, цена, количество) |

---

## 🎯 В процессе

- Спроектировал REST API на Django REST Framework
- Написал сериализаторы (включая вложенные) и вьюхи (APIView + ViewSet)
- Использовал DefaultRouter для автоматической маршрутизации
- Реализовал JWT-аутентификацию через `simplejwt`
- Интегрировал Vue.js с DRF-бэкендом (Axios, Pinia, Vue Router)
- Работал с PostgreSQL и спроектировал связи между моделями

---

## 👤 Автор

GitHub: https://github.com/FirstAgain27
