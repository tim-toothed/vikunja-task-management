---
name: vikunja-task-management
description: Use when an agent must read, create, update, assign, or organize tasks in Vikunja through its API.
version: 1.0.0
author: tim-toothed
license: MIT
metadata:
  hermes:
    tags: [vikunja, викунжа, викунья, задачник, задачи, доска, tasks, kanban, ghannt, api]
    related_skills: []
---

# Vikunja Task Management

## Purpose

Работа с любым экземпляром Vikunja через API: проекты, задачи, назначения, сроки, приоритеты, метки и Kanban-колонки.

Skill не зависит от способа размещения Vikunja, домена, конкретной команды, проекта или пользователя.

## Configuration

Использовать:

- `VIKUNJA_URL` — базовый URL Vikunja;
- `VIKUNJA_API_TOKEN` — API-токен текущего агента из локального credential source (обычно `.env` файла);

Не зашивать в skill username, project ID, team ID, API-токены, пароли или структуру конкретной организации. Если credential source не содержит нужных данных, сообщить об этом без вывода секрета.

Перед изменением данных:

1. Проверить доступ к API.
2. Найти пользователя по точному username.
3. Найти проект по точному названию.
4. Проверить существующие задачи и защититься от дублей.
5. Не создавать новый проект или команду без явного указания.

## Projects and team access

Членство пользователя в команде не делает его личные проекты общедоступными. Чтобы проект был виден команде, проект нужно отдельно связать с командой через project-team permission.

При изменении доступа:

- найти точную команду;
- проверить текущую связь проекта и команды;
- не менять владельца проекта;
- назначать минимально необходимые права;
- перечитать связь после изменения.

## Tasks

При создании или обновлении задачи:

- назначать её на точного пользователя через API;
- хранить рабочий статус в Kanban-колонке проекта;
- для завершённых задач использовать также `done=true`;
- срок указывать полями `start_date` и `due_date`;
- приоритет указывать полем `priority`;
- тематическую группировку делать через labels;
- не записывать в description служебные поля, миграционные ID, внутренние маркеры и дубли статуса;
- не дублировать в description данные, которые уже представлены колонкой, сроком, приоритетом, меткой или assignee.

## Kanban

Перед перемещением задачи:

1. Получить Kanban view проекта.
2. Получить существующие bucket’ы этого view.
3. Использовать существующие колонки, не создавать дубликаты.
4. Переместить задачу через endpoint bucket tasks.
5. Проверить связь задачи с bucket и её позицию.

`bucket_id` в обычном обновлении задачи не заменяет операцию перемещения в Kanban.

## API operations

Точные форматы запросов и ответов приведены в `references/api-contract.md`. Полный индекс путей и методов из OpenAPI — в `references/openapi-path-index.md`. Загружать references при работе через API, а не дублировать их содержимое в основном skill.

Основные операции:

- `GET /api/v1/projects`;
- `GET /api/v1/projects/{id}/tasks`;
- `PUT /api/v1/projects/{id}/tasks`;
- `POST /api/v1/tasks/{id}`;
- `DELETE /api/v1/tasks/{id}`;
- `GET /api/v1/tasks/{id}/assignees`;
- `PUT /api/v1/tasks/{id}/assignees`;
- `GET /api/v1/projects/{project}/views`;
- `GET /api/v1/projects/{project}/views/{view}/buckets`;
- `POST /api/v1/projects/{project}/views/{view}/buckets/{bucket}/tasks`;
- `GET /api/v1/labels`;
- `PUT /api/v1/labels`;
- `GET /api/v1/tasks/{task}/labels`;
- `PUT /api/v1/tasks/{task}/labels`.

## Safe updates

Полное обновление задачи может сбросить или не включить связанные данные. После полного `POST /tasks/{id}` повторно проверить и при необходимости восстановить:

- assignee;
- labels;
- Kanban bucket;
- priority;
- даты;
- `done`.

HTTP-код успеха сам по себе не подтверждает результат. Состояние задачи и связанные endpoint’ы нужно перечитать после изменения.

## Credential safety

API-токен и другие credentials:

- не выводить в чат, логи, URL или описания задач;
- не помещать в файлы skill;
- не передавать между агентами через текст задачи;
- использовать только через штатный credential source текущего агента.

## Completion criteria

Операция считается завершённой, когда API подтверждает, что:

- задача находится в нужном проекте;
- назначен точный пользователь;
- выставлены приоритет и сроки;
- задача находится в нужной Kanban-колонке;
- labels соответствуют операции;
- дубликаты не созданы;
- проект и командный доступ не изменены за пределами запроса.
