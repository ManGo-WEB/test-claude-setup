# test-claude-setup

Тестовый монорепозиторий: FastAPI backend + React frontend.

## Stack
- Backend: Python 3.12, FastAPI, SQLAlchemy 2.0 (async), Alembic
- Frontend: React 19 + Vite + TypeScript
- Tests: pytest (backend), Vitest (frontend)
- Package managers: uv (backend), pnpm (frontend)

## Команды

### Backend (из `backend/`)
- `uv run uvicorn app.main:app --reload` — dev-сервер
- `uv run pytest` — тесты
- `uv run ruff check .` — линтер
- `uv run ruff format .` — форматер
- `uv run mypy app` — типы
- `uv run alembic upgrade head` — применить миграции

### Frontend (из `frontend/`)
- `pnpm dev` — dev-сервер
- `pnpm build` — продакшн-сборка
- `pnpm test` — юнит-тесты
- `pnpm lint` — линтер

## Структура
backend/app/
api/        — роутеры FastAPI (тонкие, без бизнес-логики)
models/     — SQLAlchemy ORM-модели
schemas/    — Pydantic-схемы (вход/выход API)
services/   — бизнес-логика
backend/tests/  — pytest
frontend/src/
components/ — переиспользуемые React-компоненты
pages/      — страницы
api/        — клиент к backend

## Конвенции

### Backend
- Type hints везде, ruff + mypy strict
- Async/await для всех операций с БД
- Pydantic v2 для валидации
- Зависимости через `Depends()`, не глобальные синглтоны
- Бизнес-логика в `services/`, роутеры только маршрутизация

### Frontend
- Функциональные компоненты + hooks, никаких классов
- TypeScript strict, никаких `any` (используй `unknown` + narrowing)
- Импорты через алиасы (`@/components/...`), не `../../../`
- API-вызовы только через `src/api/`, не из компонентов напрямую

## Что НЕ делать
- Не использовать sync-запросы к БД в async-роутах
- Не размещать бизнес-логику в роутерах FastAPI
- Не использовать `any` без обоснования в комментарии
- Не коммитить `.env`, `__pycache__`, `.venv`, `node_modules`, `dist/`
- Не делать `git add .` — выбирай файлы осознанно
