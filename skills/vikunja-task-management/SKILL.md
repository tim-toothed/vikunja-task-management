---
name: vikunja-task-management
description: Use when an agent works with Vikunja tasks via API. Использовать при работе агента с задачами Vikunja через API.
version: 1.0.0
author: Hermes Agent
license: MIT
metadata:
  hermes:
    tags: [vikunja, tasks, kanban, api, задачи, задачник, канбан]
    related_skills: []
---

# Vikunja Task Management

## Overview

Use this skill to work with any Vikunja instance through its API: projects, tasks, assignees, dates, priorities, labels, and Kanban columns.

The skill is independent of the deployment model, domain, organization, project, and user.

## When to Use

Use this skill when an agent must:

- discover Vikunja users, teams, projects, views, or tasks;
- create, update, assign, move, label, or complete tasks;
- manage project access for users or teams;
- organize work through Kanban columns.

Do not hardcode organization-specific IDs, usernames, URLs, or credentials.

## Configuration

Use:

- `VIKUNJA_URL` — the Vikunja base URL;
- `VIKUNJA_API_TOKEN` — the current agent's API token from the local credential source, commonly the Hermes `.env` file.

Never put usernames, project IDs, team IDs, API tokens, passwords, or organization-specific structure into this skill. If the credential source is missing a required value, report the missing variable without exposing a secret.

Before changing data:

1. Verify API access.
2. Resolve the user by exact username.
3. Resolve the project by exact title.
4. Check existing tasks and prevent duplicates.
5. Do not create a project or team unless explicitly requested.

## Projects and Team Access

Team membership does not automatically make a personal project visible to the team. Sharing a project with a team is a separate project-team permission operation.

When changing access:

- resolve the exact team;
- check the current project-team relation;
- do not change the project owner;
- grant the minimum required permission;
- read the relation back after the change.

## Tasks

When creating or updating a task:

- assign it to the exact user through the API;
- store the working status in the project's Kanban column;
- use `done=true` for completed tasks;
- store dates in `start_date` and `due_date`;
- store importance in `priority`;
- use labels for thematic grouping;
- do not put `source`, migration IDs, internal markers, or duplicated status in `description`;
- do not duplicate in `description` information already represented by a column, date, priority, label, or assignee.

## Kanban

Before moving a task:

1. Get the project's Kanban view.
2. Get the existing buckets for that view.
3. Use an existing bucket; do not create duplicates.
4. Move the task through the bucket-task endpoint.
5. Read back the task-bucket relation and position.

A `bucket_id` in a normal task update does not replace the Kanban move operation.

## API Operations

Use `references/api-contract.md` for request formats and common endpoint usage. Use `references/openapi-path-index.md` for the complete path and method index generated from the v1 and v2 OpenAPI schemas.

Load references on demand instead of duplicating their contents in this file.

## Safe Updates

A full task update can reset or omit related data. After a full `POST /tasks/{id}`, re-check and restore when necessary:

- assignee;
- labels;
- Kanban bucket;
- priority;
- dates;
- `done`.

An HTTP success status alone is not completion proof. Read the task and its related endpoints after each change.

## Credential Safety

API tokens and other credentials:

- never print them in chat, logs, URLs, or task descriptions;
- never put them in skill files;
- never transfer them between agents through task text;
- use them only through the current agent's credential source.

## Completion Criteria

An operation is complete only when the API confirms that:

- the task is in the intended project;
- the exact user is assigned;
- priority and dates are set;
- the task is in the intended Kanban column;
- labels match the operation;
- no duplicate was created;
- project and team access were not changed beyond the request.
