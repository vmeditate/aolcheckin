Art of Living — Event Check-In App
A mobile-friendly volunteer check-in app backed by Google Sheets. Multiple volunteers can use it simultaneously from their phones. All status changes (Arrived, No Show, Cancelled) write instantly to the sheet, and direct edits in the sheet reflect in the app on next refresh. A Summary tab is auto-maintained with live counts.

Requirements
The app is a single `index.html` — no build step, no dependencies. It talks to a Google Apps Script Web App deployed from the event's Google Sheet. The script must be deployed as a web app, executed as the owner, accessible by anyone. The resulting `/exec` URL is what volunteers paste into the app on first launch (saved in localStorage after that).
The Google Sheet needs row 1 as headers. Required header names: `Name`, `Guest Type`, `Tier`, `Wristband Color`, `Arrived`, `No Show`, `Cancelled`, `Checked In By`. Columns E/F/G should be Sheets checkboxes. Column order doesn't matter — the script resolves everything by header name.
Per Event
Copy the previous sheet (File → Make a copy), swap in the new guest list, update `SHEET_ID` in the Apps Script, and create a new deployment. Share the new `/exec` URL with volunteers. The GitHub Pages URL never changes.
