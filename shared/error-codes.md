---
title: Error codes (skeleton)
team: shared
updated: 2026-10-12
author: your-name
---

# Error codes

A starting point. Backend owns this. Change anything here once the real API exists.

## Why

The backend sends a **code**. The frontend decides what **message** to show.
This way we can change wording (or translate it) without touching the backend.

## Suggested response shape

```json
{
  "error": {
    "code": "AUTH_EMAIL_INVALID",
    "message": "Developer-facing text, not shown to users",
    "field": "email"
  }
}
```

- `code` is what the frontend checks.
- `message` is only for logs and debugging.
- `field` is optional. Use it when the error belongs to one input.

## Naming

`AREA_WHAT_HAPPENED`, all caps, underscores.

| Area | Prefix |
|---|---|
| Sign-up, login, passwords, 2FA | `AUTH_` |
| Profile, username | `PROFILE_` |
| Anything not specific | `COMMON_` |

Add new areas as you need them.

## Common codes

| Code | When |
|---|---|
| `COMMON_RATE_LIMITED` | Too many requests in a short time |
| `COMMON_VALIDATION` | Input failed validation (use `field`) |
| `COMMON_SERVER_ERROR` | Something broke on our side |

Codes for specific features live in the request file for that feature
(for example, the auth codes are in `fullstack-security/frontend/requests/FE-001-auth-flow-texts.md`).
