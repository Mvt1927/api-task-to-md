---
name: api-task-to-md
description: Use when the task is API-related and you need a structured markdown summary from AI analysis or commit changes. Do not use for non-API tasks.
---

# api-task-to-md

Generate a clean, actionable markdown report for API work based on task context, AI output, and/or commit diff.

## When to use

Use this skill only when the task is related to API work, including:
- API design or contract updates
- Endpoint implementation or refactor
- Request/response schema changes
- Validation, authentication, permission, or error handling changes
- Pagination/filter/search/sort updates
- API docs updates from code or commit history

Do not use this skill for non-API tasks such as UI-only, styling, infra-only, or generic refactor with no API impact.

## Instructions

1. Identify API scope first.
- List touched endpoints and methods.
- Detect whether changes are breaking or backward-compatible.

2. Gather source of truth.
- Read task description, relevant files, and commit diff.
- Prefer actual code/commit evidence over assumptions.

3. Extract change details per endpoint.
- Endpoint path and HTTP method.
- Purpose/business behavior.
- Request changes: path params, query params, headers, body.
- Response changes: success payload, error payload, status codes.
- Auth/permission requirements.

4. Highlight risk and impact.
- Breaking changes and migration notes.
- Affected consumers (mobile/web/other services).
- Test coverage gaps or follow-up tasks.

5. Output in markdown using the template below.
- Keep wording concise and implementation-focused.
- If information is missing, mark as "TBD" instead of guessing.

## Output template

```md
# API Task Summary

## 1) Overview
- Task:
- Source:
- Scope:
- Compatibility: Backward-compatible | Breaking | Mixed

## 2) Endpoint Changes

### [METHOD] /path
- Purpose:
- Change type: Added | Updated | Deprecated | Removed
- Authentication:

Request
- Path params:
- Query params:
- Headers:
- Body schema:

Response
- Success status:
- Success payload:
- Error status and payload:

Notes
- Validation rules:
- Business rules:

## 3) Data Contract Delta
- Added fields:
- Updated fields:
- Removed fields:
- Default values / nullability changes:

## 4) Risks and Migration
- Breaking points:
- Required client updates:
- Rollout/feature flag notes:

## 5) Testing and Verification
- Unit tests:
- Integration/API tests:
- Manual verification checklist:

## 6) Open Items
- TBD:
- Questions:
```

## Quality bar

- No hallucinated endpoint or payload fields.
- Every claim should be traceable to task context or commit/code evidence.
- Prefer short bullet points over long paragraphs.
