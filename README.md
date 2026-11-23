# Carranam

**A shared task and habit tracker for couples, built around a virtual pet you raise together.**

Most to-do apps are built for one person. Couples end up splitting chores and goals across chats, notes and reminders, and nothing keeps both people engaged over time. Carranam puts personal and shared tasks for two people in one place and connects them to a common goal: keeping their cat, Murzik, fed and happy.

Every completed task adds a portion to Murzik's bowl. The bowl is split into two halves, one per partner, and it is only full when both people have done their part. A full bowl extends the couple's streak, and over weeks of consistent days Murzik grows from a kitten into a king.

![Screens](design/screens/all-screens.png)

## Key features

- **Personal and shared tasks in one list**, each partner with a consistent color across both devices
- **Split bowl mechanic.** Three portions per partner per day; a shared task feeds both halves
- **A pet that reflects the day.** Murzik is hungry, waiting, eating, happy, sleeping or sad depending on progress
- **Long-term growth.** Four growth stages with unlockable accessories, based on total full-bowl days, so a missed day never resets progress
- **Progress views.** Weekly strip, monthly calendar, per-partner contribution and achievements
- **Personal perspective.** Each partner sees themselves as "Me" and the other under a nickname they chose

## Documentation

| Document | Contents |
|---|---|
| [Business analysis](docs/BA.md) | Vision, target users, core mechanic, functional requirements, user stories, business rules, data model, MVP scope, risks |
| [Design guide](design/DESIGN.md) | Screens, color system, typography, components, character states, icons, app icon |
| [Interactive prototype](https://claude.ai/artifact/1HPMj4AmYbHgtNn2qLizX4) | Clickable design canvas with all screens (Ukrainian UI) |

## Repository structure

```
docs/
  BA.md                  Business analysis
design/
  DESIGN.md              Design guide
  overview.png           Visual summary on one page
  tokens.json            Colors, typography, spacing, radii
  screens/               Screen mockups
  murzik/                Character in six moods, plus the original sketch
  murzik/stages/         Growth stages with accessories
  accessories/           Bow, scarf, crown (SVG)
  icons/                 Interface and task icons (SVG)
  app-icon/              App icons for PWA, iOS and Android
```

## Platform and proposed stack

Progressive Web App: a single codebase that installs to the home screen on iOS and Android.

- **Frontend:** React, Vite, service worker for offline support
- **Backend:** Supabase (Auth, Postgres, Realtime, row-level security)
- **Notifications:** Web Push

## Status

Product analysis and design are complete. Development has not started yet.

## Credits

Character design: Tetiana Miskevych.
