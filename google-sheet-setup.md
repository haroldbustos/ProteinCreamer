# Connect the Claire Foods waitlist to a Google Sheet

The form POSTs each signup to a Google Apps Script "Web App" that appends a row to your Sheet. No server, no third-party service.

## 1. Create the Sheet
1. Go to https://sheets.new and name it e.g. **Claire Foods — Waitlist**.
2. In row 1, add headers: `timestamp`, `name`, `email`, `reason`, `source`.

## 2. Add the script
1. In the Sheet: **Extensions → Apps Script**.
2. Delete any boilerplate and paste this:

```javascript
function doPost(e) {
  var lock = LockService.getScriptLock();
  lock.tryLock(30000);
  try {
    var sheet = SpreadsheetApp.getActiveSpreadsheet().getSheets()[0];
    var p = (e && e.parameter) ? e.parameter : {};
    sheet.appendRow([
      p.timestamp || new Date().toISOString(),
      p.name || '',
      p.email || '',
      p.reason || '',
      p.source || ''
    ]);
    return ContentService
      .createTextOutput(JSON.stringify({ ok: true }))
      .setMimeType(ContentService.MimeType.JSON);
  } catch (err) {
    return ContentService
      .createTextOutput(JSON.stringify({ ok: false, error: String(err) }))
      .setMimeType(ContentService.MimeType.JSON);
  } finally {
    lock.releaseLock();
  }
}
```

3. **Save** (disk icon).

## 3. Deploy as a Web App
1. **Deploy → New deployment**.
2. Gear icon → **Web app**.
3. Settings:
   - **Execute as:** Me
   - **Who has access:** **Anyone**  ← required so the page can POST without login
4. **Deploy**, authorize when prompted (you may need to click *Advanced → Go to project (unsafe)* — it's your own script).
5. Copy the **Web app URL** (ends in `/exec`).

## 4. Paste the URL into the design
1. Open the design's **Tweaks** panel.
2. Paste the URL into **sheetEndpoint**.
3. Submit a test signup — a new row should appear in your Sheet within a second or two.

## Notes
- The request is sent "fire-and-forget" (`mode: 'no-cors'`), so the page can't read the response — it always shows the success state. Check the Sheet to confirm rows are landing.
- If you change the script later, use **Deploy → Manage deployments → Edit → New version** so the same URL keeps working.
- Leaving `sheetEndpoint` empty keeps the old demo behavior (success state only, nothing sent).
