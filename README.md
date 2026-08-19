# Vikunja Task Management for Hermes

A portable Hermes Agent skill for working with [Vikunja](https://github.com/go-vikunja/vikunja) through its API.

The skill is deployment-agnostic: it works with self-hosted and hosted Vikunja instances. It covers projects, tasks, assignees, dates, priorities, labels, team access, and Kanban columns.

## Install with Hermes

Install directly from this public GitHub skill path:

```bash
hermes skills install tim-toothed/vikunja-task-management/skills/vikunja-task-management --category productivity --yes
```

The full `owner/repo/path` identifier is required for GitHub skills. Hermes also downloads the referenced files under `references/`.

To make the skill discoverable through `hermes skills search`, add the repository as a tap first:

```bash
hermes skills tap add tim-toothed/vikunja-task-management
hermes skills search vikunja --source github
```

Install from a direct `SKILL.md` URL when only the main skill is needed:

```bash
hermes skills install https://raw.githubusercontent.com/tim-toothed/vikunja-task-management/main/skills/vikunja-task-management/SKILL.md --category productivity --yes
```

Check the installed skill:

```bash
hermes skills list
hermes skills inspect tim-toothed/vikunja-task-management/skills/vikunja-task-management
```

## Configuration

Provide these variables through the current Hermes credential/environment mechanism:

```env
VIKUNJA_URL=https://your-vikunja.example
VIKUNJA_API_TOKEN=<agent-api-token>
```

Do not commit `.env` or real credentials. The token is intentionally not included in this repository.

## Publish or update from a local checkout

```bash
hermes skills publish ./skills/vikunja-task-management --to github --repo tim-toothed/vikunja-task-management
```

Or use Git directly:

```bash
git add .
git commit -m "Update Vikunja Hermes skill"
git push origin main
```

## Contents

```text
skills/vikunja-task-management/SKILL.md
skills/vikunja-task-management/references/api-contract.md
skills/vikunja-task-management/references/openapi-path-index.md
```

---

# Vikunja Task Management для Hermes

Переносимый skill Hermes Agent для работы с Vikunja через API.

Skill не зависит от способа размещения Vikunja: подходит для self-hosted и hosted-инстансов. Поддерживает проекты, задачи, назначения, сроки, приоритеты, метки, доступ команд и Kanban-колонки.

## Установка через Hermes

Установка из публичного GitHub skill path:

```bash
hermes skills install tim-toothed/vikunja-task-management/skills/vikunja-task-management --category productivity --yes
```

Для GitHub необходим полный идентификатор в формате `owner/repo/path/to/skill`. Hermes также загрузит связанные файлы из `references/`.

Чтобы skill находился через поиск Hermes:

```bash
hermes skills tap add tim-toothed/vikunja-task-management
hermes skills search vikunja --source github
```

Проверка установленного skill:

```bash
hermes skills list
hermes skills inspect tim-toothed/vikunja-task-management/skills/vikunja-task-management
```

## Конфигурация

Передайте текущему Hermes-агенту:

```env
VIKUNJA_URL=https://your-vikunja.example
VIKUNJA_API_TOKEN=<agent-api-token>
```

`.env` и реальные credentials нельзя коммитить в репозиторий.

## Состав

```text
skills/vikunja-task-management/SKILL.md
skills/vikunja-task-management/references/api-contract.md
skills/vikunja-task-management/references/openapi-path-index.md
```
