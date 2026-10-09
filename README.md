# MineRace — сапёр на время

Учебный full-stack проект: пользователи регистрируются, играют в сапёр и соревнуются по времени прохождения. Результаты побед сохраняются в таблице лидеров.

## Стек

| Часть | Технологии |
|-------|------------|
| Backend | Ruby on Rails 8 (API), SQLite, JWT, bcrypt |
| Frontend | React 19, TypeScript, Vite, React Router |
| UI | Собственный UI Kit (`frontend/src/ui-kit`) |

## Требования курса

- **Регистрация и авторизация** — `POST /auth/register`, `POST /auth/login`, JWT в заголовке `Authorization: Bearer …`
- **Модели** — `User`, `GameResult` (связи и валидации)
- **Автотесты моделей** — `backend/test/models/user_test.rb`, `backend/test/models/game_result_test.rb`
- **UI Kit** — страница `/ui-kit` и переиспользуемые компоненты

## Быстрый старт

### Backend

```powershell
cd backend
bundle install
bundle exec rails db:prepare
bundle exec rails db:seed
bundle exec rails server
```

На Windows запускайте команды **из папки `backend`**. Если сервер уже упал с `bin/rails (Errno::ENOENT)` — остановите процесс (Ctrl+C) и запустите снова; в `config/puma.rb` отключён автоперезапуск Puma под Windows.

API: http://localhost:3000

Демо-пользователь после `db:seed`: `demo@minesweeper.local` / `demo123`

### Frontend

```powershell
cd frontend
npm install
npm run dev
```

Сайт: http://localhost:5173

Переменная окружения (опционально): `VITE_API_URL=http://localhost:3000` — см. `.env.example`.

### Тесты бэкенда

```powershell
cd backend
rails test
```

## API (кратко)

| Метод | Путь | Описание |
|-------|------|----------|
| POST | `/auth/register` | Регистрация `{ user: { username, email, password, password_confirmation } }` |
| POST | `/auth/login` | Вход `{ email, password }` |
| GET | `/auth/me` | Текущий пользователь (JWT) |
| POST | `/game_results` | Сохранить результат (JWT) |
| GET | `/game_results` | История игрока (JWT) |
| GET | `/leaderboard?difficulty=beginner` | Топ побед |

Сложности: `beginner` (9×9, 10 мин), `intermediate` (16×16, 40), `expert` (16×30, 99).

## Структура репозитория

```
backend/     Rails API
frontend/    React-приложение + UI Kit + игра
```
