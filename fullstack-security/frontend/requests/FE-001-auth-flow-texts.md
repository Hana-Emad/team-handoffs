---
id: FE-001
title: Auth flow texts (sign-up, login, 2FA, forgot password)
from: backend
to: frontend
cc: [security]
status: open
priority: high
created: 2026-10-12
updated: 2026-10-12
author: your-name
---

# Auth flow texts

## Summary

All user-facing texts for sign-up, login, two-factor authentication, and forgot password, plus the error codes the backend will return. Applies to **web and mobile**.

## Context

These are the MVP auth screens. Wording is written to work on both touch devices and web (no "tap" or "click").

Error codes are **suggested**. Backend will confirm them when the API is ready. See `shared/error-codes.md` for the response format.
A code of `—` means the check happens in the frontend only, before calling the API.

## Behavior notes

- **Google sign-up** skips Email Verification (email is already verified, no password needed) and goes straight to Profile Setup.
- **We never reveal whether an email has an account.** This affects three places:
  - **Sign-up with an existing email:** no error. The user goes to Email Verification as usual. Instead of a code, the backend emails them: "You already have an account. Log in or reset your password."
  - **Login with a Google-only account:** shows the normal "Incorrect email or password." message.
  - **Forgot password:** always shows the same success message. If the account uses Google, the email tells them to use Continue with Google instead of sending a code.
- **Divider "or":** the lines on both sides are drawn in CSS. No dashes in the text.

---

## Sign-up flow

### Screen: Account creation

| Element | Text |
|---|---|
| Header | Create Your Account |
| Subheader | Start building and running your business in one place. |
| Google button | Continue with Google |
| Divider | or |
| Email label | Email Address |
| Email placeholder | name@example.com |
| Submit button | Send Verification Code |
| Terms line | By continuing, you agree to our Terms of Service and Privacy Policy. |
| Footer link | Already have an account? Log in |

| Code | When | Message |
|---|---|---|
| — | Email empty | Please enter your email address. |
| `AUTH_EMAIL_INVALID` | Email format is wrong | This doesn't look like a valid email address. |
| `COMMON_RATE_LIMITED` | Too many attempts | Too many attempts. Please try again in a few minutes. |
| `AUTH_GOOGLE_FAILED` | Google sign-in failed | We couldn't sign you in with Google. Please try again. |

### Screen: Email verification

| Element | Text |
|---|---|
| Header | Verify Your Email |
| Instruction | We sent a 6-digit code to {email}. It expires in 10 minutes. |
| Change email link | Change email |
| Code label | Verification Code |
| Resend link | Didn't get the code? Resend |
| Resend cooldown | Resend available in {seconds}s |
| Resend success | A new code has been sent. |
| Spam hint | Can't find it? Check your spam or junk folder. |
| Password label | Create Password |
| Password helper | At least 8 characters. |
| Confirm password label | Confirm Password |
| Show/hide toggle | Show / Hide |
| Submit button | Continue |

| Code | When | Message |
|---|---|---|
| `AUTH_CODE_INVALID` | Wrong code | That code isn't correct. Please check and try again. |
| `AUTH_CODE_EXPIRED` | Code expired | This code has expired. Please request a new one. |
| `AUTH_CODE_TOO_MANY_ATTEMPTS` | Too many wrong codes | Too many incorrect attempts. Please request a new code. |
| `AUTH_PASSWORD_TOO_SHORT` | Password under 8 characters | Password must be at least 8 characters. |
| — | Passwords don't match | Passwords don't match. |

### Screen: Profile setup

| Element | Text |
|---|---|
| Header | Set Up Your Profile |
| Display name label | Display Name |
| Display name helper | This is how your name appears to your team and customers. |
| Username label | Username |
| Username helper | 3 to 30 characters. Lowercase letters, numbers, and hyphens (-) only. |
| Username available | Available ✓ |
| Team question | How will you use the platform? |
| Option 1 | Individual: Just me |
| Option 2 | Team: Me and my team (you can invite them later) |
| Submit button | Create Account |

| Code | When | Message |
|---|---|---|
| — | Display name empty | Please enter a display name. |
| `PROFILE_USERNAME_TOO_SHORT` | Under 3 characters | Username must be at least 3 characters. |
| `PROFILE_USERNAME_TOO_LONG` | Over 30 characters | Username can't be longer than 30 characters. |
| `PROFILE_USERNAME_INVALID_CHARS` | Characters not allowed | Only lowercase letters, numbers, and hyphens are allowed. |
| `PROFILE_USERNAME_TAKEN` | Someone has it | This username is taken. Try another one. |
| `PROFILE_USERNAME_RESERVED` | Reserved by us | This username isn't available. Try another one. |
| — | No option chosen | Please choose Individual or Team. |

---

## Login flow

### Screen: Login

| Element | Text |
|---|---|
| Header | Welcome Back |
| Google button | Continue with Google |
| Divider | or |
| Email label | Email Address |
| Password label | Password |
| Show/hide toggle | Show / Hide |
| Forgot password link | Forgot password? |
| Submit button | Log In |
| Footer link | New here? Create an account |

| Code | When | Message |
|---|---|---|
| — | Email or password empty | Please enter your email and password. |
| `AUTH_INVALID_CREDENTIALS` | Wrong email or password, **or** the account only uses Google | Incorrect email or password. |
| `COMMON_RATE_LIMITED` | Too many attempts | Too many attempts. Please try again in a few minutes. |

### Screen: Two-factor authentication

Shown only if the user has two-factor authentication turned on.

| Element | Text |
|---|---|
| Header | Two-Factor Authentication |
| Instruction | Open your authenticator app and enter the 6-digit code. |
| Code label | Authenticator Code |
| Remember device checkbox | Remember this device for 30 days |
| Submit button | Verify & Log In |
| Backup code link | Use a backup code instead |
| Back link | Back to login |

| Code | When | Message |
|---|---|---|
| `AUTH_TOTP_INVALID` | Wrong code | That code isn't correct. Please try again. |
| `COMMON_RATE_LIMITED` | Too many attempts | Too many incorrect attempts. Please try again in a few minutes. |

### Screen: Backup code

| Element | Text |
|---|---|
| Header | Use a Backup Code |
| Instruction | Enter one of the backup codes you saved when you set up two-factor authentication. |
| Code label | Backup Code |
| Submit button | Verify & Log In |
| Back link | Use authenticator app instead |

| Code | When | Message |
|---|---|---|
| `AUTH_BACKUP_CODE_INVALID` | Wrong or already used | This backup code isn't valid or has already been used. |

---

## Forgot password flow

### Screen: Forgot password

| Element | Text |
|---|---|
| Header | Reset Your Password |
| Instruction | Enter your email and we'll send you a code to reset your password. |
| Email label | Email Address |
| Submit button | Send Reset Code |
| Back link | Back to login |
| Success (always shown) | If an account exists for {email}, you'll get a code shortly. |

### Screen: Set new password

| Element | Text |
|---|---|
| Header | Set a New Password |
| Instruction | Enter the 6-digit code we sent to {email}. It expires in 10 minutes. |
| Code label | Verification Code |
| Resend link | Didn't get the code? Resend |
| New password label | New Password |
| New password helper | At least 8 characters. |
| Confirm password label | Confirm New Password |
| Submit button | Reset Password |
| Success | Your password has been reset. You can now log in. |

| Code | When | Message |
|---|---|---|
| `AUTH_CODE_INVALID` | Wrong code | That code isn't correct. Please check and try again. |
| `AUTH_CODE_EXPIRED` | Code expired | This code has expired. Please request a new one. |
| `AUTH_PASSWORD_TOO_SHORT` | Password under 8 characters | Password must be at least 8 characters. |
| — | Passwords don't match | Passwords don't match. |

---

## Done when

- [ ] All screens use the texts above on web and mobile
- [ ] Each error code shows its message
- [ ] Unknown error codes show a general fallback message
- [ ] Sign-up with an existing email goes to Email Verification with no error

## Open questions

- Fallback message for unknown errors. Suggestion: "Something went wrong. Please try again."
- Backend to confirm the final error codes.
- Arabic versions of all texts are still needed (Arabic is the default language, see `shared/ALL-001-frontend-foundations.md`).

## Not in MVP

- Phone number sign-up with WhatsApp OTP (SMS fallback)
- Continue with Facebook (also connects Facebook page / Instagram / WhatsApp Business)

## Changes

- 2026-10-12: Created from backend's text list.
- 2026-10-12: Removed "email already registered" (sign-up) and "Google-only account" (login) errors so we don't reveal which emails have accounts. Replaced "Tap Resend" with "Please request a new one" to work on web and mobile. Added suggested error codes.
