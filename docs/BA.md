# Carranam: Business Analysis

> **Product:** Carranam, a shared task tracker for couples. **Mascot:** Murzik, the cat.
> **Document version:** 0.2 · November 2026

## Contents

1. [Product overview](#1-product-overview)
2. [Problem and solution](#2-problem-and-solution)
3. [Target users](#3-target-users)
4. [Goals and success metrics](#4-goals-and-success-metrics)
5. [Core mechanic](#5-core-mechanic)
6. [Functional requirements](#6-functional-requirements)
7. [User stories and acceptance criteria](#7-user-stories-and-acceptance-criteria)
8. [Business rules](#8-business-rules)
9. [Non-functional requirements](#9-non-functional-requirements)
10. [Data model](#10-data-model)
11. [MVP scope](#11-mvp-scope)
12. [Risks and open questions](#12-risks-and-open-questions)
13. [Glossary](#13-glossary)

---

## 1. Product overview

Carranam is a task and habit tracker designed for two people. A couple manages personal and shared tasks in one place, and every completed task feeds their shared virtual cat, Murzik. The cat reacts to how the day is going and grows over time as the couple builds consistent habits.

**In one sentence:** a shared to-do list where progress is expressed through a pet you look after together, rather than through checkboxes and percentages.

**Name.** *Carranam* comes from Sarah J. Maas's *Throne of Glass* series, where it describes two people whose powers combine into one. The product applies the same idea to everyday life: two people whose efforts add up to a shared result.

**Platform:** Progressive Web App. One codebase runs on iOS and Android and installs to the home screen like a native app.

## 2. Problem and solution

### Problem
- Mainstream task managers are designed for individuals. Couples coordinate shared responsibilities through chats and notes, where tasks get lost.
- Habit trackers lose engagement quickly. Checkmarks and percentages offer little emotional reason to come back every day.
- There is no low-friction way to encourage a partner without it feeling like nagging.

### Solution
- **One shared space.** Each partner's personal tasks and the couple's shared tasks live in a single list, with a clear color for each owner.
- **An emotional motivator.** A shared pet whose state depends on completed tasks and is visible to both partners.
- **Mutual accountability instead of control.** The pet's bowl is split in two and is only full when both partners contribute. Encouragement comes from a common goal, not from reminders aimed at one person.

## 3. Target users

| Segment | Description | Key needs |
|---|---|---|
| **Couples living together** (primary) | Ages 20–35, sharing a household and wanting fewer conflicts over chores | Shared household tasks, transparency, ease of use |
| **Long-distance couples** | Living in different cities or countries | A sense of presence, a shared daily ritual, time zone support |
| **Friends and roommates** (secondary) | Two people with a common goal | Shared habits such as exercise or study |

### Personas
- **The Organizer.** Manages many tasks, values good design and wants shared planning to feel pleasant rather than like another productivity tool.
- **The Minimalist.** Values speed and simplicity. Expects to complete a task with a single tap and without extra screens or settings.

## 4. Goals and success metrics

| Goal | Metric | MVP target |
|---|---|---|
| Daily engagement | DAU / MAU per couple | ≥ 60% |
| Shared participation | Share of days on which **both** partners complete at least one task | ≥ 50% |
| Retention | Couples still active four weeks after onboarding | ≥ 40% |
| Mechanic effectiveness | Average streak length | ≥ 5 days |
| Activation | Couple created and first shared task completed on day one | ≥ 70% |

## 5. Core mechanic

### 5.1 Shared pet
Each couple has one cat, **Murzik** (the couple can rename it). Its state reflects how the couple is doing today.

### 5.2 Split bowl
- Every day Murzik starts with an empty bowl divided into **two halves**, one per partner.
- Each half holds **3 portions**.
- A completed **personal** task adds 1 portion to its owner's half.
- A completed **shared** task adds 1 portion to **both** halves.
- The bowl is **full** when both halves reach 3/3. Murzik becomes happy and the couple's streak increases by one day.

### 5.3 Moods

| Mood | Shown when |
|---|---|
| Hungry | 0–2 of 6 portions |
| Waiting | 3–5 of 6 portions |
| Eating | about 1.3 seconds of animation right after a task is completed |
| Happy | bowl is full (6/6) |
| Sleeping | night time, 23:00–07:00 in the couple's time zone |
| Sad | yesterday's bowl was not full and no portions have been added today |

### 5.4 Growth
Murzik grows based on the **total number of full-bowl days**, not the current streak, so a missed day never sets progress back.

| Stage | Threshold | Reward |
|---|---|---|
| Kitten | from day one | — |
| Teen | 7 days | bow |
| Adult | 30 days | scarf |
| King Murzik | 100 days | crown |

### 5.5 Streak and streak recovery
- The streak is the number of consecutive full-bowl days.
- A missed day resets the streak but not the growth level.
- Once every 7 days the streak can be **recovered** by filling a double bowl the following day (6 portions per partner).

### 5.6 Personal perspective
- Each partner sees themselves as **"Me"** and the other partner under a **nickname they set themselves**. For example, one partner sees "Alex" while the other sees "Kate".
- **Colors belong to people, not to "Me".** One partner is always pink, the other always blue, and shared tasks are lavender, so both phones show the same colors.
- Murzik addresses each partner from their own perspective ("2 more from you and 1 from Alex").

## 6. Functional requirements

Priority follows MoSCoW: **M** must, **S** should, **C** could.

### 6.1 Account and pairing
| ID | Requirement | Priority |
|---|---|---|
| FR-01 | Sign up and sign in (email magic link, Apple or Google) | M |
| FR-02 | Create a couple: the owner generates an invite code or link | M |
| FR-03 | Join a couple with a code or link | M |
| FR-04 | During setup each partner sets their own name, color and a nickname for the other | M |
| FR-05 | Change the partner's nickname (visible only to the person who set it) | S |
| FR-06 | Leave a couple, archiving the pet and history | S |

### 6.2 Tasks
| ID | Requirement | Priority |
|---|---|---|
| FR-10 | Create a task with a title, icon and owner (me / partner / together) | M |
| FR-11 | Set a date or deadline and a reminder time | M |
| FR-12 | Repeat: once, daily, weekly, custom days | M |
| FR-13 | Quantity goals (for example 5 chapters or 150 pages) with partial progress on the card | S |
| FR-14 | Edit and delete tasks | M |
| FR-15 | Complete a task with one tap and undo completion | M |
| FR-16 | Filter: all / mine / partner's / together | M |
| FR-17 | Group by today / this week / later | S |
| FR-18 | Notes on tasks | C |
| FR-19 | Per-task streaks for recurring tasks | S |

### 6.3 Pet
| ID | Requirement | Priority |
|---|---|---|
| FR-30 | Home screen with the pet, its mood, the split bowl and a hint showing what each partner has left | M |
| FR-31 | "Eating" reaction immediately after a task is completed | M |
| FR-32 | Mood calculation according to section 5.3 | M |
| FR-33 | Growth screen: current stage, progress to the next stage, rewards | M |
| FR-34 | Accessories unlocked at growth stages | S |
| FR-35 | Rename the pet | S |
| FR-36 | Streak recovery (section 5.5) | C |

### 6.4 Progress
| ID | Requirement | Priority |
|---|---|---|
| FR-40 | Weekly strip showing the pet's face for each day | M |
| FR-41 | Monthly calendar: full days, sad days, today | S |
| FR-42 | Statistics: tasks per partner, shared tasks, full bowls, current streak | S |
| FR-43 | Achievements with progress (first week, 10 full bowls, 100 shared tasks) | C |

### 6.5 Notifications
| ID | Requirement | Priority |
|---|---|---|
| FR-50 | Task reminders at a set time (push) | M |
| FR-51 | Gentle notification when the partner has completed their half | S |
| FR-52 | Evening reminder if the bowl is not full (no later than 21:00) | S |
| FR-53 | Quiet hours and per-type notification settings | S |

### 6.6 Sync
| ID | Requirement | Priority |
|---|---|---|
| FR-60 | Partner changes appear in real time (≤ 2 s) | M |
| FR-61 | Offline completions are stored locally and synced when back online | S |

## 7. User stories and acceptance criteria

**US-01. Create a couple**
As a user, I want to invite my partner with a link so that we share one pet.
- *Given* I am registered and not in a couple, *when* I tap "Invite", *then* I see a link and a code I can send through any messenger.
- *Given* my partner opens the link and signs up, *then* we both see the same pet and an empty bowl.

**US-02. Complete a personal task**
As a partner, I want to complete my task with one tap so that I feed the pet.
- *Given* the task "Workout" belongs to me, *when* I tap its check circle, *then* the card fills with color, a green check appears, the pet shows the "eating" state and my half of the bowl gains one portion.
- *Given* my half is already at 3/3, *then* no portion is added beyond the limit, but the task still counts in statistics.

**US-03. Complete a shared task**
- *When* either partner completes a shared task, *then* one portion is added to both halves and the other partner sees it in real time.

**US-04. Fill the bowl**
- *Given* both halves are at 3/3, *then* the pet becomes happy, the streak increases by one and the day is marked as full in the calendar.

**US-05. Undo a completion**
- *When* I uncheck a task, *then* the portion is removed from the corresponding half and mood and streak are recalculated.

**US-06. See my partner under my own nickname**
- *Given* I named my partner "Alex", *then* all of my screens label their tasks "Alex", while on their device the same tasks are labeled "Me".

**US-07. Add a task with a quantity goal**
- *When* I create "Finish coursework" with a goal of 5 chapters and log 2, *then* the card is 40% filled with a "2/5" chip.

**US-08. Miss a day**
- *Given* yesterday's bowl was not full, *then* this morning the pet is sad, the streak is 0, and the growth level and rewards are kept.

## 8. Business rules

| ID | Rule |
|---|---|
| BR-01 | The couple's day starts at 00:00 in the **couple's time zone**, set at creation and editable later. |
| BR-02 | Limit of 3 portions per partner per day. Tasks beyond the limit count toward statistics but not the bowl. |
| BR-03 | A shared task can be completed by either partner, once per period. |
| BR-04 | A recurring task can be completed once per period (day or week). |
| BR-05 | A task with a quantity goal N counts toward the bowl once N/N is reached. |
| BR-06 | Completions logged after a day has ended do not change that day's bowl. |
| BR-07 | The streak is evaluated at the end of the couple's day: +1 if the bowl is full, otherwise reset to 0 (subject to recovery). |
| BR-08 | Growth level equals the total number of full-bowl days and never decreases. |
| BR-09 | Streak recovery is available at most once every 7 days. |
| BR-10 | A partner's nickname and a user's color are personal settings; colors must be unique within a couple. |
| BR-11 | Either partner can delete a shared task; only the owner can delete a personal task. |

## 9. Non-functional requirements

| Category | Requirement |
|---|---|
| Platforms | PWA: iOS Safari 16.4+ (push requires installation to the home screen), Android Chrome 110+ |
| Performance | First screen in ≤ 2 s on 4G; tap response ≤ 100 ms using optimistic updates |
| Offline | Open the app and complete tasks without a connection; sync on reconnect |
| Accessibility | WCAG 2.1 AA: text contrast ≥ 4.5:1, touch targets ≥ 44 px, screen reader labels, animations disabled with reduced motion |
| Security | Couple data is accessible only to its two members (row-level security); HTTPS only |
| Privacy | Minimal personal data; account export and deletion |
| Localization | Ukrainian and English |

## 10. Data model

```
User        id, name, color, timezone, created_at
Pair        id, cat_name, timezone, created_at, archived_at
PairMember  pair_id, user_id, partner_nickname, joined_at
Task        id, pair_id, owner (user_id | "both"), title, icon,
            note, due_at, remind_at, repeat_rule, goal_count, created_by
Completion  id, task_id, user_id, period_date, progress, completed_at
DailyBowl   pair_id, date, portions_a, portions_b, is_full
CatState    pair_id, level_days, streak, last_rescue_at, accessories[]
Achievement pair_id, code, progress, unlocked_at
```

**Proposed stack:** React and Vite (PWA with service worker) on the frontend; Supabase (Postgres, Auth, Realtime, row-level security) on the backend; Web Push for notifications. Hosting on Vercel, Netlify or GitHub Pages.

## 11. MVP scope

**In scope for MVP (v0.1)**
- Pairing: create, invite, names, colors, nicknames
- Tasks: create, edit, repeat, complete, filters
- Pet: split bowl, six moods, eating animation
- Streak and weekly strip
- Task reminders
- Real-time sync

**Later releases**
- v0.2: growth stages and accessories, quantity goals, monthly calendar, statistics
- v0.3: achievements, streak recovery, "partner completed their half" notifications
- Later: widgets, themes, custom pet artwork

## 12. Risks and open questions

| # | Risk or question | Proposed approach |
|---|---|---|
| R-1 | Partners in different time zones: when does the day end? | Use the couple's time zone (BR-01) and show both partners the time remaining in Murzik's day |
| R-2 | Guilt and pressure ("the cat is hungry because of you") | Neutral, blame-free copy; the pet never dies or leaves, it only gets sad |
| R-3 | Push notification limitations on iOS | Prompt to install to the home screen during onboarding |
| R-4 | Unequal workload between partners | 3-portion cap per partner per day; each partner's contribution is visible |
| R-5 | What happens to the pet if a couple separates? | Archive the pet; each person can start a new couple |
| Q-1 | "Carranam" is a term coined by Sarah J. Maas. Is it suitable for a public release? | Acceptable for a portfolio project; run a trademark check before any public launch |
| Q-2 | Support for multiple pets or groups larger than two? | Out of scope for MVP |

## 13. Glossary

| Term | Definition |
|---|---|
| **Couple** | Two users who share one pet |
| **Bowl** | The couple's daily progress: two halves of 3 portions each |
| **Portion** | The unit of progress earned by completing a task |
| **Full bowl** | Both halves at 3/3 |
| **Streak** | Number of consecutive full-bowl days |
| **Level** | Total number of full-bowl days; determines the pet's growth stage |
| **Nickname** | The name a user sees for their partner |

---

Design and screens: [design/DESIGN.md](../design/DESIGN.md)
