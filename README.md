# Chinese Christian Fellowship Bremen — Volunteer Scheduler

A full-stack web application for managing and coordinating volunteer duties for a church community. Built with vanilla HTML, CSS and JavaScript on the frontend, and Supabase as the backend database.

🌐 **Live Demo:** [https://ccfb-bremen.netlify.app](https://ccfb-bremen.netlify.app)

---

## Features

### For the Admin
- **Auto-schedule** — generate a full month of volunteer assignments in one click, automatically skipping members who have reported unavailability
- **Manual assignment** — change any role at any time using dropdown menus
- **Member management** — add and remove members; members set their own passwords on first login
- **Unavailability overview** — see all reported unavailability before scheduling
- **Personal calendar export** — download individual `.ics` calendar files per member, or all at once
- **Storage management** — view database usage with a visual breakdown and archive old data
- **Progress tracking** — live stats bar showing filled vs open slots for the month

### For Members
- **Live schedule view** — see the full monthly schedule for Friday Bible Study and Sunday Sermon; own assignments highlighted in yellow
- **My Roles** — personal assignment view with one-click calendar file download
- **Availability** — mark unavailability for the next month with a reason; admin sees this before scheduling
- **Profile** — upload a profile photo and change password

### General
- Fully responsive — works on laptop, tablet and mobile
- Persistent data — all schedules, members and photos saved in Supabase
- Secure login — each user has their own account with password
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

### Friday Bible Study
| Role | Description |
|------|-------------|
| Receptionist | Welcomes and assists guests |
| Cooking | Prepares the meal |
| Song Leading | Leads worship songs |
| Bible Study Leader — Group A | Leads Group A discussion |
| Bible Study Leader — Group B | Leads Group B discussion |

### Sunday Sermon
| Role | Description |
|------|-------------|
| Moderator | Leads and anchors the service |
| PPT Preparation | Prepares and operates presentation slides |
| Receptionist | Greets attendees at the door |
| Children Bible Study | Leads the children's programme |

---

## Getting Started

### Run locally

No build step required. Simply open `index.html` in any modern browser.

```bash
# Clone the repository
git clone https://github.com/amandawang90-spec/ccfb-scheduler.git

# Open in browser
open index.html
```

> When running locally the app connects to the Supabase instance configured in the source. To use your own database, follow the Supabase setup steps below.

---

### Set up your own Supabase database

1. Create a free project at [supabase.com](https://supabase.com)

2. Go to **SQL Editor** and run the following SQL to create the required tables:
```sql
CREATE TABLE profiles (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  name text NOT NULL,
  email text UNIQUE NOT NULL,
  role text NOT NULL DEFAULT 'member',
  photo text,
  password_hash text,
  created_at timestamp DEFAULT now()
);

CREATE TABLE schedules (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  year int NOT NULL,
  month int NOT NULL,
  day_type text NOT NULL,
  week_index int NOT NULL,
  role_id text NOT NULL,
  member_name text NOT NULL DEFAULT '',
  updated_at timestamp DEFAULT now(),
  UNIQUE(year, month, day_type, week_index, role_id)
);

CREATE TABLE unavailability (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  member_name text NOT NULL,
  date_key text NOT NULL,
  reason text NOT NULL DEFAULT 'Other',
  UNIQUE(member_name, date_key)
);

ALTER TABLE profiles ENABLE ROW LEVEL SECURITY;
ALTER TABLE schedules ENABLE ROW LEVEL SECURITY;
ALTER TABLE unavailability ENABLE ROW LEVEL SECURITY;

CREATE POLICY "Public access" ON profiles FOR ALL USING (true) WITH CHECK (true);
CREATE POLICY "Public access" ON schedules FOR ALL USING (true) WITH CHECK (true);
CREATE POLICY "Public access" ON unavailability FOR ALL USING (true) WITH CHECK (true);
```

3. Go to **Project Settings → Data API** and copy your **Project URL** and **Publishable Key**

4. Open `index.html` and replace the placeholder values at the top of the script section with your own:
```javascript
const SUPA_URL = "https://your-project.supabase.co";  // your Project URL
const SUPA_KEY = "your-publishable-key";               // your Publishable Key
```

5. Save the file — you are now connected to your own database
```

---

### Deploy to Netlify

1. Create a free account at [netlify.com](https://netlify.com)
2. From your dashboard click **Add new project → Deploy manually**
3. Drag and drop `index.html` onto the upload area
4. Netlify gives you a live URL instantly
5. Optionally rename your site under **Site configuration → Change site name**

---

## Default Admin Account

On first load the app automatically creates a default admin account:

| Field | Value |
|-------|-------|
| Email | admin@church.com |
| Password | Admin123 |

> **Important:** Change the admin password immediately after first login via Profile → Change Password.

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
- [ ] Multi-language support (English / Chinese)
- [ ] Proper password hashing (bcrypt)

---

## Built With

This project was built entirely through conversation with [Claude](https://claude.ai) by Anthropic — from initial concept to live deployment — without writing a single line of code manually.

---

## License

MIT License — free to use, modify and distribute.
