---
id: SEC-001
title: Review auth flows before MVP
from: backend
to: security
cc: [frontend]
status: open
priority: high
created: 2026-10-12
updated: 2026-10-12
author: your-name
---

# Review auth flows before MVP

## Summary

Please review the sign-up, login, 2FA, and forgot password flows before they ship.

## Context

Full texts and behavior are in `fullstack-security/frontend/requests/FE-001-auth-flow-texts.md`.

## Requirements

Please check and confirm:

1. **No account enumeration.** None of these should reveal whether an email has an account:
   - Sign-up with an existing email (we send an email instead of showing an error)
   - Login with a Google-only account (shows the normal "Incorrect email or password.")
   - Forgot password (same success message every time)
   - Response times should also be similar in both cases
2. **Rate limits** on: sending codes, entering codes, login, 2FA, backup codes, forgot password.
3. **Codes:** 6 digits, expire after 10 minutes, invalid after too many wrong tries.
4. **Passwords:** minimum 8 characters. Is that enough, or should we also block common or leaked passwords?
5. **"Remember this device for 30 days":** how it's stored, and how a user can remove remembered devices.
6. **Backup codes:** each works only once and is stored hashed.

## Done when

- [ ] Each point above is confirmed or has a follow-up request

## Open questions

- Any extra checks you want for Continue with Google?

## Changes

- 2026-10-12: Created.
