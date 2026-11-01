# Vikunja Task Management

![Vikunja Task Management](docs/banner.png)

Connect Vikunja boards with Hermes.

Manage tasks and projects through the Vikunja API. Works with self-hosted and hosted instances.

## Install

```bash
hermes skills install tim-toothed/vikunja-task-management/skills/vikunja-task-management --category productivity --yes
```

## Features

- Create and update tasks and projects.
- Manage assignees, due dates, priorities, and labels.
- Organize Kanban columns and move tasks between them.
- Manage team access.

## Configuration

Provide your instance URL and API token through the agent’s environment:

```env
VIKUNJA_URL=https://your-vikunja.example
VIKUNJA_API_TOKEN=***
```

Keep API tokens out of chat messages and version control.

## Usage

Ask Hermes:

```text
Show overdue tasks in my Website project.
```

```text
Create a task to review the landing page,
set the due date to Friday, and assign it to me.
```

```text
Move the landing page review task to In Progress.
```
