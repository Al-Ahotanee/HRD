Here's the implementation plan:

---

## SGES HDRRC System — Implementation Plan

### Stack
- **Frontend:** React 18 (single HTML file, in-browser Babel) + Lucide icons CDN + Chart.js CDN
- **Backend:** Node.js + Express
- **DB:** SQLite (`better-sqlite3`)
- **Deploy:** Vercel (frontend as static, backend as serverless functions)

---

### 5-File Architecture

| # | File | Purpose |
|---|------|---------|
| 1 | `api/index.js` | Full Express REST API — all routes (auth, users, materials, courses, staff dev, repo, stats) |
| 2 | `api/db.js` | SQLite schema bootstrap + all DB helpers |
| 3 | `public/index.html` | Landing page (hero, carousel, features, CTA, footer) |
| 4 | `public/app.html` | Full SPA — login + all dashboards (Admin, Lecturer, Student) |
| 5 | `vercel.json` | Routing config (rewrites `/api/*` → serverless, static serving) |

---

### Modules Per Role

**Admin Dashboard**
- User management (create/edit/delete lecturers & students)
- Staff development tracking (training records, performance evals)
- Repository oversight (approve/reject uploads)
- Course management
- Analytics charts (Chart.js): user growth, uploads, course activity

**Lecturer Dashboard**
- Upload courseware (notes, videos, assignments)
- Manage own courses
- View student enrollment
- Repository contributions
- Personal development log

**Student Dashboard**
- Browse & access courseware
- Search repository
- Enrolled courses view
- Download materials

---

### DB Schema (SQLite)

```
users — id, name, email, password_hash, role, department, created_at
courses — id, title, code, description, lecturer_id, created_at
materials — id, title, type, file_url, course_id, uploaded_by, created_at
repository — id, title, abstract, file_url, category, author_id, approved, created_at
staff_development — id, user_id, training_title, date, status, notes
```

---

### Landing Page Sections
1. **Header** — logo, nav links, Login/Register CTA
2. **Hero** — headline, subtext, dual CTA buttons, animated background
3. **Carousel** — rotating feature highlights (3 slides)
4. **Features** — 6-card grid (HR, Repository, Courseware, Analytics, Security, Access)
5. **Stats** — animated counters
6. **Footer** — links, contact, university branding

---

### Deployment Notes
- `vercel.json` routes `/api/*` to `api/index.js` as a serverless function
- SQLite file stored at `/tmp/sges.db` on Vercel (ephemeral — for demo; production would swap to PlanetScale/Turso)
- Static files served from `public/`

---

Ready to build? I'll generate all 5 files in sequence. Confirm and I'll start with `api/db.js` + `api/index.js`, then the two HTML files, then `vercel.json`.
