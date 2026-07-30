# Vikunja API index

API base: `{VIKUNJA_URL}/api/{version}`

Поддерживаемые версии: `v1`, `v2`.

Auth:

```http
Authorization: Bearer <agent-api-token>
Content-Type: application/json
```

Токен брать из локального credential source агента.

> `organizations` в Vikunja API отсутствует. Используются `teams` и `projects`.

## System and admin

| Method | Endpoint | Использование |
|---|---|---|
| `GET` | `/info` | Версия и информация API |
| `GET` | `/admin/overview` | Сводка администратора |
| `GET` | `/admin/projects` | Все проекты для администратора |
| `GET` | `/admin/users` | Все пользователи для администратора |
| `POST` | `/admin/users/{id}/admin` | Изменить admin-статус |
| `POST` | `/admin/users/{id}/status` | Изменить статус пользователя |
| `POST` | `/admin/projects/{id}/owner` | Изменить владельца проекта |

## Users and account

| Method | Endpoint | Использование |
|---|---|---|
| `GET` | `/user` | Текущий пользователь |
| `GET` | `/users?s={username}` | Поиск пользователей |
| `GET` | `/users/{username}/avatar` | Avatar пользователя |
| `POST` | `/user/token` | Создать API token |
| `DELETE` | `/user/token/{id}` | Удалить API token |
| `POST` | `/user/token/refresh` | Обновить token |
| `GET` | `/user/settings/general` | Общие настройки |
| `POST` | `/user/settings/general` | Изменить общие настройки |
| `POST` | `/user/settings/email` | Изменить email |
| `POST` | `/user/password` | Изменить пароль |
| `GET` | `/user/timezones` | Часовые пояса |
| `GET` | `/user/export` | Экспорт данных |
| `POST` | `/user/export/request` | Запросить экспорт |
| `GET` | `/user/export/download` | Скачать экспорт |
| `POST` | `/user/logout` | Завершить сессию |

## Teams

| Method | Endpoint | Использование |
|---|---|---|
| `GET` | `/teams` | Список команд |
| `PUT` | `/teams` | Создать команду |
| `GET` | `/teams/{teamID}` | Команда |
| `POST` | `/teams/{teamID}` | Обновить команду |
| `DELETE` | `/teams/{teamID}` | Удалить команду |
| `GET` | `/teams/{teamID}/members` | Участники |
| `PUT` | `/teams/{teamID}/members` | Добавить участника |
| `DELETE` | `/teams/{teamID}/members/{userID}` | Удалить участника |
| `POST` | `/teams/{teamID}/members/{userID}/admin` | Изменить admin-статус участника |

## Projects

| Method | Endpoint | Использование |
|---|---|---|
| `GET` | `/projects` | Список проектов |
| `PUT` | `/projects` | Создать проект |
| `GET` | `/projects/{projectID}` | Проект |
| `POST` | `/projects/{projectID}` | Обновить проект |
| `DELETE` | `/projects/{projectID}` | Удалить проект |
| `POST` | `/projects/{projectID}/duplicate` | Дублировать проект |
| `GET` | `/projects/{projectID}/users` | Пользователи проекта |
| `PUT` | `/projects/{projectID}/users` | Добавить пользователя |
| `DELETE` | `/projects/{projectID}/users/{userID}` | Удалить пользователя |
| `GET` | `/projects/{projectID}/teams` | Команды проекта |
| `PUT` | `/projects/{projectID}/teams` | Добавить команду к проекту |
| `DELETE` | `/projects/{projectID}/teams/{teamID}` | Удалить команду проекта |
| `GET` | `/projects/{projectID}/shares` | Shared links проекта |
| `PUT` | `/projects/{projectID}/shares` | Создать shared link |
| `DELETE` | `/projects/{projectID}/shares/{shareID}` | Удалить shared link |
| `GET` | `/projects/{projectID}/webhooks` | Webhooks проекта |
| `PUT` | `/projects/{projectID}/webhooks` | Создать webhook |
| `POST` | `/projects/{projectID}/webhooks/{webhookID}` | Обновить webhook |
| `DELETE` | `/projects/{projectID}/webhooks/{webhookID}` | Удалить webhook |
| `GET` | `/projects/{projectID}/tasks` | Задачи проекта |
| `PUT` | `/projects/{projectID}/tasks` | Создать задачу в проекте |

## Project views and Kanban

| Method | Endpoint | Использование |
|---|---|---|
| `GET` | `/projects/{projectID}/views` | Views проекта |
| `PUT` | `/projects/{projectID}/views` | Создать view |
| `POST` | `/projects/{projectID}/views/{viewID}` | Обновить view |
| `DELETE` | `/projects/{projectID}/views/{viewID}` | Удалить view |
| `GET` | `/projects/{projectID}/views/{viewID}/buckets` | Колонки Kanban |
| `PUT` | `/projects/{projectID}/views/{viewID}/buckets` | Создать колонку |
| `POST` | `/projects/{projectID}/views/{viewID}/buckets/{bucketID}` | Обновить колонку |
| `DELETE` | `/projects/{projectID}/views/{viewID}/buckets/{bucketID}` | Удалить колонку |
| `POST` | `/projects/{projectID}/views/{viewID}/buckets/{bucketID}/tasks` | Переместить задачу |
| `GET` | `/projects/{projectID}/views/{viewID}/tasks` | Задачи через view |

Move task:

```json
{"task_id":123,"project_view_id":456,"bucket_id":789}
```

## Tasks

| Method | Endpoint | Использование |
|---|---|---|
| `GET` | `/tasks/{taskID}` | Задача |
| `POST` | `/tasks/{taskID}` | Обновить задачу |
| `DELETE` | `/tasks/{taskID}` | Удалить задачу |
| `GET` | `/tasks/{taskID}/assignees` | Назначения |
| `PUT` | `/tasks/{taskID}/assignees` | Назначить пользователя |
| `DELETE` | `/tasks/{taskID}/assignees/{userID}` | Снять назначение |
| `POST` | `/tasks/{taskID}/assignees/bulk` | Массовые назначения |
| `GET` | `/tasks/{taskID}/labels` | Метки задачи |
| `PUT` | `/tasks/{taskID}/labels` | Добавить метку |
| `DELETE` | `/tasks/{taskID}/labels/{labelID}` | Удалить метку |
| `POST` | `/tasks/{taskID}/labels/bulk` | Массовые метки |
| `GET` | `/tasks/{taskID}/comments` | Комментарии |
| `PUT` | `/tasks/{taskID}/comments` | Добавить комментарий |
| `POST` | `/tasks/{taskID}/comments/{commentID}` | Обновить комментарий |
| `DELETE` | `/tasks/{taskID}/comments/{commentID}` | Удалить комментарий |
| `GET` | `/tasks/{taskID}/attachments` | Вложения |
| `PUT` | `/tasks/{taskID}/attachments` | Добавить вложение |
| `DELETE` | `/tasks/{taskID}/attachments/{attachmentID}` | Удалить вложение |
| `GET` | `/tasks/{taskID}/relations` | Связи задач |
| `PUT` | `/tasks/{taskID}/relations` | Создать связь |
| `DELETE` | `/tasks/{taskID}/relations/{kind}/{otherTaskID}` | Удалить связь |
| `POST` | `/tasks/{taskID}/duplicate` | Дублировать задачу |
| `POST` | `/tasks/{taskID}/position` | Изменить позицию |
| `POST` | `/tasks/{taskID}/read` | Отметить прочитанной |
| `PUT` | `/tasks/bulk` | Массовое изменение задач |

Task fields:

```json
{
  "title":"Task title",
  "description":"Text",
  "done":false,
  "priority":3,
  "start_date":"2026-08-03T00:00:00Z",
  "due_date":"2026-08-09T23:59:59Z"
}
```

## Labels

| Method | Endpoint | Использование |
|---|---|---|
| `GET` | `/labels` | Список меток |
| `PUT` | `/labels` | Создать метку |
| `GET` | `/labels/{labelID}` | Метка |
| `POST` | `/labels/{labelID}` | Обновить метку |
| `DELETE` | `/labels/{labelID}` | Удалить метку |

## Other

| Method | Endpoint | Использование |
|---|---|---|
| `POST` | `/migration/csv/preview` | Предпросмотр CSV-импорта |
| `GET/PUT` | `/projects/{projectID}/background` | Background проекта |
| `GET/PUT` | `/projects/{projectID}/backgrounds/unsplash` | Unsplash background |
| `PUT` | `/projects/{projectID}/backgrounds/upload` | Загрузить background |
| `GET/PUT` | `/user/settings/webhooks` | Пользовательские webhooks |
| `GET/PUT` | `/user/settings/totp` | TOTP |
| `GET/PUT` | `/user/settings/avatar` | Avatar |
| `GET/PUT` | `/user/settings/token/caldav` | CalDAV token |

Vikunja v2 дополнительно содержит time entries:

```text
GET/PUT /projects/{projectID}/time-entries
GET/PUT /tasks/{taskID}/time-entries
```
