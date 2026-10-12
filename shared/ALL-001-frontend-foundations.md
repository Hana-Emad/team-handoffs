---
id: ALL-001
title: Frontend foundations (look, language, layout, cards)
from: frontend
to: everyone
cc: []
status: open
priority: high
created: 2026-10-12
updated: 2026-10-12
author: your-name
---

# Frontend foundations

## Summary

The things frontend decides **once**, before building screens, so every screen looks and behaves the same for the whole year.
Frontend owns the decisions. Sections marked **Needs a yes from** affect other teams, so those teams must agree.

## Context

- Term 1 plan, week 4: frontend delivers wireframes of all term 1 screens and the landing page design.
- Technical structure, section 11: Arabic right-to-left and mobile from day one; the AI answers with the same cards the pages use; the sales screen must stay fast.
- Each answer below is a **suggestion**. Replace it with the decision and fill the `Decision:` line.

---

## Decide this week (week 4)

### 1. Language and direction

| Question | Suggestion |
|---|---|
| Default language | Arabic, with English as a switch |
| Direction | RTL for Arabic, LTR for English. Build with logical CSS (`margin-inline-start`, not `margin-left`) so one layout works both ways |
| Digits | Western digits (0 to 9) everywhere, including Arabic. Easier for prices and phone numbers |
| Money | Backend sends piastres (`total_cents: 7500`). Frontend shows `75 ج.م` in Arabic and `EGP 75` in English. Show decimals only when not zero |
| Dates and time | Business timezone (Cairo). 12-hour clock with ص / م in Arabic, AM / PM in English |
| Where texts live | One translation file per language, using keys (`auth.login.submit`). No text written directly in components |
| Who writes the Arabic texts | **Needs an owner.** FE-001 only has English |

Decision:

### 2. Devices and sizes

| Question | Suggestion |
|---|---|
| Screens to support | Phone, tablet, laptop. The sales screen is designed **tablet first** |
| Breakpoints | Phone under 640px, tablet 640 to 1024px, desktop over 1024px |
| Touch targets | At least 44px tall. Sales screen buttons bigger (around 64px) |
| Dark mode | Not in term 1 |

Decision:

### 3. Colors

Pick colors by **role**, not by name. Every color in the code must come from this list.

| Role | Used for | Value |
|---|---|---|
| `primary` | Main buttons, links, active items | |
| `primary-text` | Text on top of `primary` | |
| `background` | Page background | |
| `surface` | Cards, panels | |
| `border` | Lines, input borders | |
| `text` | Main text | |
| `text-muted` | Helper text, labels | |
| `success` | Done, paid, in stock | |
| `warning` | Running low, needs attention | |
| `danger` | Errors, cash gaps, cancel | |
| `info` | Neutral notices | |
| `ai` | Things the AI did or suggests (so the owner can tell them apart) | |

Rules:

- Text must be readable on its background (contrast at least 4.5:1, check with any online contrast checker).
- Never use color alone to show meaning. Add an icon or a word (colorblind users, sunlight on a tablet).
- **The app's colors and each café's store website colors are separate.** The store website will use the business's own brand colors (Studio, term 2), so build it with variables that can be swapped per business from day one.

Decision:

### 4. Fonts and sizes

| Question | Suggestion |
|---|---|
| Font | One font that has good Arabic and Latin letters. Options: IBM Plex Sans Arabic, Cairo, Tajawal, Noto Sans Arabic |
| Size scale | 12, 14, 16, 20, 24, 32. Body text 16 |
| Weights | Regular and bold only |

Decision:

### 5. Spacing and shapes

| Question | Suggestion |
|---|---|
| Spacing | Steps of 4: 4, 8, 12, 16, 24, 32, 48 |
| Corner radius | One for small items (inputs, buttons), one for cards |
| Shadows | One light shadow for cards, none elsewhere |
| Icons | One icon set only (for example Lucide or Tabler). Check that arrows flip in RTL |

Decision:

### 6. Tools

| Question | Suggestion |
|---|---|
| Design tool | Figma. One shared file, link it here |
| Framework | Frontend's choice. It must handle RTL well |
| Component library | Use a ready one with RTL support, or build a small own set. Decide now; switching later is expensive |

Decision:
Figma link:

---

## Decide with other teams (by week 6)

### 7. AI answer cards

**Needs a yes from:** AI agent, backend

The AI answers with the same cards the pages use (due week 7). We need to agree on:

- The list of cards for term 1. Suggestion: order, item, customer, stock level, sales number, approval request.
- For each card: the data it needs (fields and types), and its buttons and what they do.
- How the AI says "show this card" in its answer.

Each card gets its own request file once agreed (for example `AGT-00X-order-card.md`).

Decision:

### 8. Talking to the backend

**Needs a yes from:** backend, security

| Question | Suggestion |
|---|---|
| Error format | As in `shared/error-codes.md`. Frontend shows messages by code |
| Unknown error message | Something went wrong. Please try again. |
| Login session | Decide with security: cookies or tokens, and how long a session lasts |
| Fake data | Backend shares example responses for each feature so frontend can build before the real API exists (working rule 2 in the plan) |

Decision:

### 9. Shared behavior

Every screen handles these the same way:

| State | Suggestion |
|---|---|
| Loading | Grey placeholder shapes, not spinners, for lists and cards |
| Empty | A short sentence and one action ("No items yet. Add your first item.") |
| Error | The message for the error code, and a "Try again" button |
| Saved | A short message at the bottom that disappears |
| Risky action (delete, cancel order) | Ask "Are you sure?" first |
| Role can't see it | Hide it. Don't show a disabled button |

**Needs a yes from:** security (for the last row)

Decision:

---

## Done when

- [ ] Sections 1 to 6 decided and filled in
- [ ] Figma file has the colors, fonts, and basic components (button, input, card, list row)
- [ ] Sections 7 to 9 agreed with the teams named
- [ ] Wireframes of all term 1 screens use these foundations

## Open questions

- Who writes and checks the Arabic texts?
- Do we have a product name and logo yet? Colors are easier to pick after that.

## Changes

- 2026-10-12: Created.
