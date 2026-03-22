# Chinese Christian Fellowship Bremen — Volunteer Scheduler

不来梅华人基督教会 服侍排班系统

A full-stack web application for managing and coordinating volunteer service duties for a church community. Built with vanilla HTML, CSS and JavaScript on the frontend, and Supabase as the backend database.

🌐 **Live Demo:** [https://ccfb-bremen.netlify.app](https://ccfb-bremen.netlify.app)

---

## Features

### For the Admin
- **Auto-schedule** — generate a full month of volunteer assignments in one click, automatically skipping members who have submitted absence requests
- **Manual assignment** — change any role at any time using dropdown menus
- **Member management** — add and remove members; members set their own passwords on first login
- **Absence request overview** — see all reported absences before scheduling
- **Personal calendar export** — download individual `.ics` calendar files per member, or all at once; members can also download their own
- **Storage management** — view database usage with a visual breakdown and archive old data
- **Progress tracking** — live stats bar showing filled vs open slots for the month

### For Members
- **Schedule overview** — see the full monthly schedule for Friday Bible Study (周五查经) and Sunday Sermon (周日崇拜); own assignments highlighted in yellow
- **My Roles** — personal assignment view with one-click calendar file download
- **Absence Request** — submit absence requests for the next month with a reason; admin sees this before scheduling
- **Profile** — upload a profile photo and change password

### General
- Fully responsive — works on laptop, tablet and mobile
- Multi-language — fully available in three languages: English, Deutsch and 中文 (Chinese), switchable in the header on any page
- Persistent data — all schedules, members and photos saved in Supabase
- Each user has their own account with password
- Zero dependencies — no frameworks, no npm, no build step required

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | Vanilla HTML, CSS, JavaScript |
| Backend / Database | [Supabase](https://supabase.com) (PostgreSQL + REST API) |
| Hosting | [Netlify](https://netlify.com) |
| Calendar Export | iCalendar (.ics) format |

---

## Service Roles

### Friday Bible Study (周五查经)
| Role | Chinese | Description |
|------|---------|-------------|
| Receptionist | 接待 | Welcomes and assists guests |
| Cooking | 爱宴 | Prepares the meal |
| Song Leading | 诗歌带领 | Leads worship songs |
| Bible Study Leader — Group A | 查经带领 A组 | Leads Group A discussion |
| Bible Study Leader — Group B | 查经带领 B组 | Leads Group B discussion |

### Sunday Sermon (周日崇拜)
| Role | Chinese | Description |
|------|---------|-------------|
| Moderator | 主持人 | Leads and anchors the service |
| PPT Preparation | PPT制作 | Prepares and operates presentation slides |
| Receptionist | 接待 | Greets attendees at the door |
| Children Bible Study | 儿童圣经班 | Leads the children's programme |

---

## Setup

This app is connected to a Supabase database and hosted on Netlify.

To run your own instance you will need a free [Supabase](https://supabase.com) account and a free [Netlify](https://netlify.com) account.

---

## How Members Join

1. Admin adds a member by name and email only — no password set by admin
2. Member visits the app and clicks **"First time here? Set your password"**
3. Member enters their email and chooses their own password
4. They are immediately logged in

---

## Project Structure

```
index.html       — The entire application (single file, no dependencies)
README.md        — This file
```

The entire application lives in a single HTML file. All JavaScript is vanilla, all styling is inline CSS, and all data is fetched from Supabase via its REST API — no build tools, no package manager, no framework.

---

## Limitations

- Passwords are stored as plain text in Supabase — suitable for internal church use, not for sensitive data
- No real-time sync — changes are visible on next page load, not pushed live
- Calendar export is a snapshot — `.ics` files do not update automatically when the schedule changes

---

## Future Improvements

- [ ] Real-time schedule updates using Supabase subscriptions
- [ ] Email notifications when the monthly schedule is published
- [ ] Live calendar subscription URL
- [ ] Role assignment history and statistics
- [ ] Proper password hashing (bcrypt)

---

## Built With

This project was built entirely through conversation with [Claude](https://claude.ai) by Anthropic — from initial concept to live deployment — without writing a single line of code manually.

---

## License

MIT License — free to use, modify and distribute.
