# Punjab BLO Directory — Fast Search

A lightweight, client-side web app for searching the Polling Booth–Wise BLO (Booth Level Officer) list for Punjab. 

---

## Features

- **Instant search** across Name, AC No, Booth No, Booth Name, Designation, and Mobile
- **Infinite scroll** — renders 30 cards at a time instead of all 24,500+ at once
- **AC filter chips** — one-click filter by Assembly Constituency (AC 1–117)
- **Sort** by AC/Booth number or by BLO Name
- **Tap-to-call** — mobile-friendly `tel:` links on every card
- **Doughnut chart** — live breakdown of Education / Health & AWW / Other designations
- Works entirely in the browser — no backend, no database

---

## Project Structure

```
/
├── index.html                        # Main app (single file)
└── Polling_Booth_Wise_BLO_LIST.csv   # Data file (must be in the same folder)
```

> Both files must sit in the **same directory**. The app fetches the CSV at runtime via a relative URL.

---

## CSV Format

The app expects these exact column headers (case-sensitive):

| Column | Description |
|---|---|
| `AC No` | Assembly Constituency number (integer) |
| `Booth No` | Polling booth number (integer) |
| `Booth Name` | Name of the polling booth location |
| `BLO Name` | Full name of the Booth Level Officer |
| `Designation` | Job designation of the BLO |
| `BLO Mobile No` | Mobile number (10-digit, no spaces) |

Rows where `AC No` is missing or zero are automatically skipped.

---

## Deployment (Netlify)

1. Place `index.html` and `Polling_Booth_Wise_BLO_LIST.csv` in the same folder.
2. Drag and drop that folder onto [app.netlify.com](https://app.netlify.com) **→ Sites → Deploy manually**.
3. Or connect a GitHub repo and let Netlify auto-deploy on every push.

No build step required — it is a static site.

---

## Performance Notes

The original version rendered all ~24,500 records into the DOM on every search, which caused the slowness. The current version uses:

- **Pre-built search blob** — each record's searchable text is joined once at load time, not on every keystroke
- **250 ms debounce** — filtering only runs after the user stops typing
- **30-cards-at-a-time rendering** via `IntersectionObserver` (infinite scroll) — the DOM stays small regardless of result count
- **DocumentFragment batching** — card elements are built off-screen and inserted in one operation to avoid layout thrashing

---

## Dependencies (CDN — no install needed)

| Library | Purpose |
|---|---|
| [Tailwind CSS](https://cdn.tailwindcss.com/) | Utility-first styling |
| [PapaParse 5.4](https://www.papaparse.com/) | Fast CSV parsing |
| [Chart.js](https://www.chartjs.org/) | Doughnut breakdown chart |
| [Inter](https://fonts.google.com/specimen/Inter) | UI typeface |

All dependencies are loaded from CDN. The app works offline only if the CDN resources are cached.

---

## Local Development

No server is needed for most browsers if you open the file directly — but Chrome blocks `fetch()` on `file://` URLs. The easiest workaround:

```bash
# Python 3
python3 -m http.server 8080
# then open http://localhost:8080
```

or use the [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) extension in VS Code.

---

## Important Notice / ਜ਼ਰੂਰੀ ਸੂਚਨਾ

> **ਪੰਜਾਬੀ —** SIR ਲਈ ਆਏ BLO ਦੀ ਪਛਾਣ ਕਰਨ ਲਈ ਹੁਣ ਤੁਸੀਂ **blolookup.netlify.app** ਵੈਬਸਾਈਟ ਦੀ ਵਰਤੋਂ ਕਰਕੇ BLO ਦੀ ਜਾਣਕਾਰੀ ਆਨਲਾਈਨ ਚੈੱਕ ਕਰ ਸਕਦੇ ਹੋ। ਇਸ ਵੈਬਸਾਈਟ 'ਤੇ ਨਾਂ, ਮੋਬਾਈਲ, ਹਲਕਾ ਜਾਂ ਹੋਰ ਵੇਰਵਿਆਂ ਨਾਲ ਖੋਜ ਕਰਕੇ ਮਿਲੀ ਜਾਣਕਾਰੀ ਨਾਲ BLO ਦੀ ਪਛਾਣ ਪੱਕੀ ਕਰੋ।
>
> ⚠️ **ਨੋਟ:** ਇਹ ਵੈਬਸਾਈਟ ਗੈਰ-ਸਰਕਾਰੀ ਹੈ। ਡਾਟਾ ECP ਤੋਂ ਲਿਆ ਗਿਆ ਹੈ, ਪਰ ਇਹ ਅਧਿਕਾਰਿਕ ਸਰਕਾਰੀ ਵੈਬਸਾਈਟ ਨਹੀਂ ਹੈ। ਸਚੇਤ ਰਹੋ, ਜਾਣਕਾਰੀ ਪੱਕੀ ਕਰੋ।

> **English —** To verify the identity of a BLO visiting for SIR, you can check their details online at **blolookup.netlify.app** by searching with their Name, Mobile, Constituency, or other details.
>
> ⚠️ **Note:** This is an unofficial website. Data is sourced from ECP but this is not an official government website. Stay alert and verify all information.

---
