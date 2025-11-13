# perechitka.ru - Микросервисная платформа для онлайн-чтения книг

[![Rust](https://img.shields.io/badge/Rust-Fast-blue?logo=rust)](https://www.rust-lang.org/)
[![Docker](https://img.shields.io/badge/Docker-Containerized-green?logo=docker)](https://www.docker.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-DB-orange?logo=postgresql)](https://www.postgresql.org/)
[![MIT License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

## 🎯 О проекте

**Perechitka** — это **микросервисная архитектура** для создания онлайн-библиотеки. Позволяет пользователям регистрироваться, входить в систему, управлять аккаунтами и читать книги онлайн.

**Текущий микросервис: Authorization API**
- Регистрация пользователей
- Авторизация (JWT-токены)
- Выход из системы

**Планы развития:**
- Book Service (управление книгами)
- Reader Service (чтение и закладки)
- Frontend (React/Vue)
- Gateway (API Gateway)

## 🛠 Технологии

| Компонент           | Технология                           |
|---------------------|--------------------------------------|
| **Backend**         | Rust (Actix Web) + C# (ASP.NET Core) |
| **База данных**     | PostgreSQL                           |
| **Контейнеризация** | Docker, Docker Compose               |
| **Авторизация**     | JWT                                  |
| **Конфиг**          | .env                                 |

## 📚 API Документация

**Базовый URL:** `https://api.perechitka.ru/v1/auth`

### 1. Регистрация `POST /registry`
```bash
curl -X POST -H "Content-Type: application/json" \
-d '{
    "first_name": "John",
    "last_name": "Doe",
    "username": "User2",
    "email": "danil.vasilkov07@gmail.com",
    "password": "Abcd1234!"
}' https://api.perechitka.ru/v2/auth/registry
```
**Ответ:** 
```json
{
    "data": {
        "email": "danil.vasilkov07@gmail.com",
        "first_name": "John",
        "id": 3,
        "is_email_verified": false,
        "last_name": "Doe"
    },
    "message": "User registered successfully",
    "success": true
}
```

### 2. Вход `POST /login`
```bash
curl -X POST -H "Content-Type: application/json" \
-d '{
  "login": "ivan",
  "password": "password123",
  "device_id": "mobile_app_1"
}' https://api.perechitka.ru/v1/auth/login
```
**Ответ:** `{ "access_token": "...", "refresh_token": "..." }`

### 3. Выход `POST /logout`
```bash
curl -X POST -H "Content-Type: application/json" \
-d '{
  "device_id": "mobile_app_1"
}' -H "Authorization: Bearer <refresh_token>" \
https://api.perechitka.ru/v1/auth/logout
```

### 4. Подтверждение почты `POST /confirm`
```bash
curl -X POST https://api.perechitka.ru/v1/auth/confirm?token={token}
```

## 🏗 Архитектура

```
[Frontend] ──> [API Gateway (planned)]
                    │
              ┌─────┼─────┐
              │     │     │
         [Auth]  [Books] [Reader]
              │
         [PostgreSQL]
```

## 📄 Лицензия

[LICENSE](LICENSE) — ALL RIGHTS RESERVED. NO USE PERMITTED UNDER ANY CIRCUMSTANCES.

## 📞 Контакты

- **Автор:** [MozzarellaCheesee](https://github.com/MozzarellaCheesee), [qwonix-R](https://github.com/qwonix-R)
- **Telegram:** [@crvxiesd](https://t.me/crvxiesd)

**Спасибо за интерес! 🌟**

---
