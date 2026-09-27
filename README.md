# Contact Directory

A password-protected **Phone Directory web app** with a clean, modern UI. Browse and search contact cards (name, role, phone, WhatsApp, email, social links, address) and add new entries through a form. The frontend is a pure static site; new entries are saved to a **Google Sheet** through a small **Google Apps Script** backend.

> Demo deployment: https://girish-directory.vercel.app/

## Features

- **Password-gated access** — a client-side password overlay guards the directory
- **Search** — instant live search by name or role
- **Contact cards** — grid of contacts with phone, WhatsApp, email, Instagram, Threads, and address
- **Add-contact form** (`add.html`) — submits entries to the Apps Script endpoint, which appends a row to Google Sheets
- **Sheet-test page** (`test-sheet.html`) — verifies the Apps Script connection
- **Modern UI** — Inter font, Lucide icons, responsive layout (`styles.css`)
- Works as a fully static frontend — no build step, no backend server to host

## Tech stack

- **Frontend:** HTML, CSS, JavaScript (vanilla)
- **Icons:** Lucide
- **Backend:** Google Apps Script (`Code.gs`)
- **Database:** Google Sheets (row schema: Timestamp, Name, Role, ContactNo, WhatsApp, Email, Instagram, Threads, Address)
- Sample fallback data ships in `directory-script.js` so the UI works without a sheet connected

## Quick start

No build or install needed:

```bash
git clone https://github.com/girishlade111/Contact-Directory.git
cd Contact-Directory
# open index.html in a browser, or serve it locally:
npx serve .
```

Then open http://localhost:3000 and enter the directory password to browse.

### Connecting your own Google Sheet (Apps Script)

1. Open `Code.gs` in [script.google.com](https://script.google.com) and paste the contents.
2. Set your Google Sheet ID in `SpreadsheetApp.openById('YOUR_SHEET_ID')`.
3. Deploy as a **Web App** with "Execute as: Me" and "Who has access: Anyone".
4. Copy the deployed Web App URL into `form-handler.js` / `add.html` where the POST endpoint is configured.

## Project structure

```
Contact-Directory/
├── index.html            # Directory UI (search + contact grid, password overlay)
├── add.html              # Add-new-contact form
├── test-sheet.html       # Apps Script connectivity test page
├── Code.gs               # Google Apps Script backend (doPost -> appends sheet row)
├── directory-script.js    # Directory rendering, search, sample data fallback
├── form-handler.js       # Form submit -> Apps Script POST logic
├── styles.css            # Styling
└── shahu palece.jpg      # Hero/background asset
```

## Environment variables

None required for the static frontend. The Apps Script piece needs:
- `SHEET_ID` — the Google Sheet ID edited into `Code.gs`
- The deployed Apps Script Web App URL — referenced by the frontend form handler

## Deployment notes

- The frontend is static — deploy to any static host (GitHub Pages, Vercel, Netlify).
- The backend is Google Apps Script (free) — no server costs.
- The password check is client-side and intended as a light access gate, not strong security; do not store genuinely sensitive contacts behind it without a real auth layer.

## Roadmap ideas

- Real server-side authentication and role-based access
- Edit/delete contacts from the UI
- CSV export of the directory

---

Built by **Girish Lade** · https://ladestack.in
