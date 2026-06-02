A quick reminder of what to do before each new event:
  New Google Sheet → update SHEET_ID in Apps Script → deploy new version
  Add the event code to config.json → commit and push to GitHub
  Send volunteers: "tiny.cc/aolcheckin — Today's code: xyz"

Art of Living — Event Check-In App
A mobile-friendly volunteer check-in app backed by Google Sheets. Multiple volunteers can use it simultaneously from their phones. All status changes (Arrived, No Show, Cancelled) write instantly to the sheet, and direct edits in the sheet reflect in the app on next refresh. A Summary tab is auto-maintained with live counts.

Requirements
The app is a single `index.html` — no build step, no dependencies. It talks to a Google Apps Script Web App deployed from the event's Google Sheet. The script must be deployed as a web app, executed as the owner, accessible by anyone. The resulting `/exec` URL is what volunteers paste into the app on first launch (saved in localStorage after that).

The Google Sheet needs row 1 as headers. Required header names: `Name`, `Guest Type`, `Tier`, `Wristband Color`, `Arrived`, `No Show`, `Cancelled`, `Checked In By`. Columns E/F/G should be Sheets checkboxes. Column order doesn't matter — the script resolves everything by header name.
Per Event

Copy the previous sheet (File → Make a copy), swap in the new guest list, update `SHEET_ID` in the Apps Script, and create a new deployment. Share the new `/exec` URL with volunteers. The GitHub Pages URL never changes.


Assuming you have a blank Google Sheet with your guest list ready, here are the exact steps:

1. Set up the Google Sheet

Row 1 must have these exact headers (any column order is fine):
Name, Guest Type, Tier, Wristband Color, Arrived, No Show, Cancelled, Checked In By
Select the Arrived, No Show, and Cancelled columns → Insert → Checkbox
Name the sheet tab at the bottom Guests (not Sheet1)


2. Get the Sheet ID
From the sheet URL:
https://docs.google.com/spreadsheets/d/  ← COPY THIS PART →  /edit

3. Open Apps Script
In the sheet go to Extensions → Apps Script. Delete any existing code. Paste the full Apps Script code from the README. Replace YOUR_GOOGLE_SHEET_ID_HERE with the ID you copied.

4. Deploy the Apps Script

Click Deploy → New deployment
Click the gear next to "Select type" → Web app
Execute as: Me
Who has access: Anyone
Click Deploy — copy the URL ending in /exec


5. Open the app and connect it

Open your GitHub Pages URL on your phone
Enter your volunteer name
Paste the /exec URL
Tap Start Check-In — the guest list should load


6. Test it

Mark one guest as Arrived in the app → confirm the checkbox turns TRUE in the sheet
Check the Checked In By column populated with your name
Tap Latest Counts → confirm a Summary tab appears in the sheet with correct numbers
Edit a checkbox directly in the sheet → tap Refresh List in the app → confirm it reflects the change

Once step 6 works, you're live. Share the GitHub Pages URL with other volunteers — they each do step 5 on their own phone.

The authorization step is key. The first time you deploy, Google requires you to explicitly grant the script permission to access your Sheets. If you skipped that or it errored, the script has no permission to read the sheet even though you own both.

2. Run the function manually once to trigger authorization

At the top, make sure getGuests is selected in the function dropdown
Click the Run button
Google will show a popup: "Authorization required"
Click Review permissions → select your account
You may see "Google hasn't verified this app" — click Advanced → Go to (app name) anyway
Click Allow

3. Now redeploy
