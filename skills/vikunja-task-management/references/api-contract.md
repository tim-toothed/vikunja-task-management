# Vikunja API Index

API base: `{VIKUNJA_URL}/api/{version}`

Supported versions: `v1`, `v2`.

Authentication:

```http
Authorization: Bearer <agent-api-token>
Content-Type: application/json
```

Get the token from the current agent's local credential source.

> Vikunja has no `organizations` API resource. Use `teams` and `projects`.

## System and Admin

| Method | Endpoint | Use |
|---|---|---|
| `GET` | `/info` | API version and service information |
| `GET` | `/admin/overview` | Administrator overview |
| `GET` | `/admin/projects` | All projects for an administrator |
| `GET` | `/admin/users` | All users for an administrator |
| `POST` | `/admin/users/{id}/admin` | Change administrator status |
| `POST` | `/admin/users/{id}/status` | Change user status |
| `POST` | `/admin/projects/{id}/owner` | Change project owner |

## Users and Account

| Method | Endpoint | Use |
|---|---|---|
| `GET` | `/user` | Current user |
| `GET` | `/users?s={username}` | Find users |
| `GET` | `/users/{username}/avatar` | User avatar |
| `POST` | `/user/token` | Create an API token |
| `DELETE` | `/user/token/{id}` | Delete an API token |
| `POST` | `/user/token/refresh` | Refresh a token |
| `GET` | `/user/settings/general` | General settings |
| `POST` | `/user/settings/general` | Update general settings |
| `POST` | `/user/settings/email` | Change email |
| `POST` | `/user/password` | Change password |
| `GET` | `/user/timezones` | Time zones |
| `GET` | `/user/export` | Export data |
| `POST` | `/user/export/request` | Request an export |
| `GET` | `/user/export/download` | Download an export |
| `POST` | `/user/logout` | Log out |

## Teams

| Method | Endpoint | Use |
|---|---|---|
| `GET` | `/teams` | List teams |
| `PUT` | `/teams` | Create a team |
| `GET` | `/teams/{teamID}` | Get a team |
| `POST` | `/teams/{teamID}` | Update a team |
| `DELETE` | `/teams/{teamID}` | Delete a team |
| `GET` | `/teams/{teamID}/members` | List members |
| `PUT` | `/teams/{teamID}/members` | Add a member |
| `DELETE` | `/teams/{teamID}/members/{userID}` | Remove a member |
| `POST` | `/teams/{teamID}/members/{userID}/admin` | Change member admin status |

## Projects

| Method | Endpoint | Use |
|---|---|---|
| `GET` | `/projects` | List projects |
| `PUT` | `/projects` | Create a project |
| `GET` | `/projects/{projectID}` | Get a project |
| `POST` | `/projects/{projectID}` | Update a project |
| `DELETE` | `/projects/{projectID}` | Delete a project |
| `POST` | `/projects/{projectID}/duplicate` | Duplicate a project |
| `GET` | `/projects/{projectID}/users` | Project users |
| `PUT` | `/projects/{projectID}/users` | Add a project user |
| `DELETE` | `/projects/{projectID}/users/{userID}` | Remove a project user |
| `GET` | `/projects/{projectID}/teams` | Project teams |
| `PUT` | `/projects/{projectID}/teams` | Add a team to a project |
| `DELETE` | `/projects/{projectID}/teams/{teamID}` | Remove a project team |
| `GET` | `/projects/{projectID}/shares` | Project share links |
| `PUT` | `/projects/{projectID}/shares` | Create a share link |
| `DELETE` | `/projects/{projectID}/shares/{shareID}` | Delete a share link |
| `GET` | `/projects/{projectID}/webhooks` | Project webhooks |
| `PUT` | `/projects/{projectID}/webhooks` | Create a webhook |
| `POST` | `/projects/{projectID}/webhooks/{webhookID}` | Update a webhook |
| `DELETE` | `/projects/{projectID}/webhooks/{webhookID}` | Delete a webhook |
| `GET` | `/projects/{projectID}/tasks` | Project tasks |
| `PUT` | `/projects/{projectID}/tasks` | Create a task in a project |

## Project Views and Kanban

| Method | Endpoint | Use |
|---|---|---|
| `GET` | `/projects/{projectID}/views` | Project views |
| `PUT` | `/projects/{projectID}/views` | Create a view |
| `POST` | `/projects/{projectID}/views/{viewID}` | Update a view |
| `DELETE` | `/projects/{projectID}/views/{viewID}` | Delete a view |
| `GET` | `/projects/{projectID}/views/{viewID}/buckets` | Kanban columns |
| `PUT` | `/projects/{projectID}/views/{viewID}/buckets` | Create a bucket |
| `POST` | `/projects/{projectID}/views/{viewID}/buckets/{bucketID}` | Update a bucket |
| `DELETE` | `/projects/{projectID}/views/{viewID}/buckets/{bucketID}` | Delete a bucket |
| `POST` | `/projects/{projectID}/views/{viewID}/buckets/{bucketID}/tasks` | Move a task |
| `GET` | `/projects/{projectID}/views/{viewID}/tasks` | Tasks through a view |

Move a task:

```json
{"task_id":123,"project_view_id":456,"bucket_id":789}
```

## Tasks

| Method | Endpoint | Use |
|---|---|---|
| `GET` | `/tasks/{taskID}` | Get a task |
| `POST` | `/tasks/{taskID}` | Update a task |
| `DELETE` | `/tasks/{taskID}` | Delete a task |
| `GET` | `/tasks/{taskID}/assignees` | List assignees |
| `PUT` | `/tasks/{taskID}/assignees` | Assign a user |
| `DELETE` | `/tasks/{taskID}/assignees/{userID}` | Remove an assignee |
| `POST` | `/tasks/{taskID}/assignees/bulk` | Bulk assignments |
| `GET` | `/tasks/{taskID}/labels` | Task labels |
| `PUT` | `/tasks/{taskID}/labels` | Add a label |
| `DELETE` | `/tasks/{taskID}/labels/{labelID}` | Remove a label |
| `POST` | `/tasks/{taskID}/labels/bulk` | Bulk labels |
| `GET` | `/tasks/{taskID}/comments` | Comments |
| `PUT` | `/tasks/{taskID}/comments` | Add a comment |
| `POST` | `/tasks/{taskID}/comments/{commentID}` | Update a comment |
| `DELETE` | `/tasks/{taskID}/comments/{commentID}` | Delete a comment |
| `GET` | `/tasks/{taskID}/attachments` | Attachments |
| `PUT` | `/tasks/{taskID}/attachments` | Add an attachment |
| `DELETE` | `/tasks/{taskID}/attachments/{attachmentID}` | Delete an attachment |
| `GET` | `/tasks/{taskID}/relations` | Task relations |
| `PUT` | `/tasks/{taskID}/relations` | Create a relation |
| `DELETE` | `/tasks/{taskID}/relations/{kind}/{otherTaskID}` | Delete a relation |
| `POST` | `/tasks/{taskID}/duplicate` | Duplicate a task |
| `POST` | `/tasks/{taskID}/position` | Change task position |
| `POST` | `/tasks/{taskID}/read` | Mark as read |
| `PUT` | `/tasks/bulk` | Bulk task update |

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

| Method | Endpoint | Use |
|---|---|---|
| `GET` | `/labels` | List labels |
| `PUT` | `/labels` | Create a label |
| `GET` | `/labels/{labelID}` | Get a label |
| `POST` | `/labels/{labelID}` | Update a label |
| `DELETE` | `/labels/{labelID}` | Delete a label |

## Other

| Method | Endpoint | Use |
|---|---|---|
| `POST` | `/migration/csv/preview` | Preview CSV import |
| `GET/PUT` | `/projects/{projectID}/background` | Project background |
| `GET/PUT` | `/projects/{projectID}/backgrounds/unsplash` | Unsplash background |
| `PUT` | `/projects/{projectID}/backgrounds/upload` | Upload a background |
| `GET/PUT` | `/user/settings/webhooks` | User webhooks |
| `GET/PUT` | `/user/settings/totp` | TOTP |
| `GET/PUT` | `/user/settings/avatar` | Avatar |
| `GET/PUT` | `/user/settings/token/caldav` | CalDAV token |

Vikunja v2 additionally exposes time entries:

```text
GET/PUT /projects/{projectID}/time-entries
GET/PUT /tasks/{taskID}/time-entries
```
