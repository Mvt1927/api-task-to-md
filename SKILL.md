---
name: api-task-to-md
description: Use when the task is API-related and you need a markdown document in the same structure as mobile_api_docs, synthesized from AI analysis or commit changes. Do not use for non-API tasks.
---

# api-task-to-md

Generate API documentation markdown that follows the same form as the user's mobile_api_docs file.

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

1. Identify API scope.
- List all endpoints affected by the task/commit.
- Group by resource when possible.

2. Collect verified inputs.
- Read task description, code changes, and commit diff.
- Use only evidence-backed details.
- If missing details, write "TBD".

3. Build output using the exact form below.
- Keep section order unchanged.
- Keep table columns unchanged.
- Keep headings in Vietnamese as defined in the template.

4. Fill endpoint content consistently.
- For each API include method, endpoint, purpose.
- Include Query Params or Path Params where relevant.
- Include Response Success and relevant Response Error examples.

5. Add common response notes.
- Document data field meanings.
- Document pagination only for list APIs.
- Document auth error response.

## Output template (must follow this structure)

```md
# Mobile API Documentation

> **Base URL:** `{domain}/{api_prefix}` (ví dụ: `{domain}/connector/api`)
>
> **Authentication:** Bearer Token (header `Authorization: Bearer {token}`) (nếu endpoint yêu cầu)
>
> **Content-Type:** `application/json`

---

## Danh sách API

| # | API | Method | Endpoint | Mục đích |
|---|-----|--------|----------|----------|
| 1 | [Tên API] | [GET/POST/PUT/DELETE] | [/path] | [Mục đích ngắn] |

---

## Chi tiết từng API

### 1. [Tên API]

| Thuộc tính | Giá trị |
|------------|---------|
| **Method** | `[GET/POST/PUT/DELETE]` |
| **Endpoint** | `/[path]` |
| **Mục đích** | [Mô tả mục đích API] |

**Query Params:**

| Param | Type | Bắt buộc | Mô tả | Ví dụ |
|-------|------|----------|-------|-------|
| `[param]` | [string/int/bool] | [Có/Không] | [Mô tả] | `[value]` |

**Path Params:**

| Param | Type | Bắt buộc | Mô tả | Ví dụ |
|-------|------|----------|-------|-------|
| `[id]` | int | Có | [Mô tả] | `1` |

**Request Body:**

```json
{
	"field": "value"
}
```

**Response Success ([200/201]):**

```json
{
	"data": {}
}
```

**Response Error ([400/401/403/404/422/500]):**

```json
{
	"error": {
		"message": "..."
	}
}
```

---

## Cấu trúc Response chung

### Trường dữ liệu

| Trường | Type | Mô tả |
|--------|------|-------|
| `id` | int | ID của bản ghi |
| `name` | string | Tên hiển thị |
| `desc` | string | Mô tả (có thể rỗng `""`) |
| `status` | string | Trạng thái: `active` hoặc `inactive` |

### Phân trang (Pagination)

Tất cả API danh sách đều hỗ trợ phân trang. Response bao gồm:
- `links`: URL đến trang đầu, cuối, trước, sau.
- `meta`: Thông tin trang hiện tại, tổng số bản ghi, số trang.

### Lỗi xác thực (401)

```json
{
	"message": "Unauthenticated."
}
```

## Data Contract Delta
- Added fields:
- Updated fields:
- Removed fields:
- Default values / nullability changes:

## Risks and Migration
- Breaking points:
- Required client updates:
- Rollout/feature flag notes:

## Testing and Verification
- Unit tests:
- Integration/API tests:
- Manual verification checklist:

```

## Quality bar

- No hallucinated endpoint or payload fields.
- Every claim should be traceable to task context or commit/code evidence.
- Keep naming and terms consistent across summary table and detail sections.
- Keep output concise and ready to paste into a .md file.
