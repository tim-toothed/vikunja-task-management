# Vikunja Task Management for Hermes

A portable Hermes Agent skill for working with Vikunja through its API.

The skill is deployment-agnostic: it works with self-hosted and hosted Vikunja instances. It covers projects, tasks, assignees, dates, priorities, labels, team access, and Kanban columns.

## Install with Hermes

Install directly from the public GitHub repository:

```bash
hermes skills install tim-toothed/vikunja-task-management --category productivity --yes
```

The repository form is recommended because it includes the linked API references.

Install from a direct `SKILL.md` URL when only the main skill is needed:

```bash
hermes skills install https://raw.githubusercontent.com/tim-toothed/vikunja-task-management/main/SKILL.md --category productivity --yes
```

Check the installed skill:

```bash
hermes skills list
hermes skills inspect tim-toothed/vikunja-task-management
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
hermes skills publish ./vikunja-task-management --to github --repo tim-toothed/vikunja-task-management
```

Or use Git directly:

```bash
git add .
git commit -m "Update Vikunja Hermes skill"
git push origin main
```

## Contents

```text
SKILL.md
references/api-contract.md
references/openapi-path-index.md
```

---

# Vikunja Task Management для Hermes

Переносимый skill Hermes Agent для работы с Vikunja через API.

Skill не зависит от способа размещения Vikunja: подходит для self-hosted и hosted-инстансов. Поддерживает проекты, задачи, назначения, сроки, приоритеты, метки, доступ команд и Kanban-колонки.

## Установка через Hermes

Установка из публичного GitHub-репозитория:

```bash
hermes skills install tim-toothed/vikunja-task-management --category productivity --yes
```

Этот способ предпочтителен, потому что устанавливает основной skill вместе с API-reference.

Проверка установленного skill:

```bash
hermes skills list
hermes skills inspect tim-toothed/vikunja-task-management
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
SKILL.md
references/api-contract.md
references/openapi-path-index.md
```
