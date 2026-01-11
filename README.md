# Clemson Makerspace Printer Status Dashboard

**Live Dashboard:** https://lavahawk.github.io/Makerspace-PrinterStatus/printer-status.html

Example:

![firefox_5HP2UJQwRn-ezgif com-optimize](https://github.com/user-attachments/assets/16d8d951-4e31-423b-819b-58be70fad2c3)

---

##  About

A real-time dashboard displaying the status of the 3D printers at the Clemson Makerspace.

The script works currently from reading the excel sheet located here: https://docs.google.com/spreadsheets/d/13ukI4J5AQtzbRLEfyYABIhA7jCMH7g53veYQPVC5CWU
and reformating it into an easy to view and nice dashboard hosted on my github page.

## 📁 Files

- **printer-status.html** - Main dashboard (requires Google Apps Script setup)
- **printer-status-local.html** - Local version with CSV file upload basically ignore this I just used it for testing
- **Google-Apps-Script.js** - Backend script for Google Sheets integration if you wanted to do API calls
- **Printer Status Update - Dashboard.csv** - Sample CSV data

## Setup Options (Ignore all this unless you want to implement this differently)

### Option 1: Google Apps Script (I didn't actually do this)

This method allows your dashboard to fetch live data directly from your Google Sheet without CORS issues.

#### Steps:

1. **Open your Google Sheet**
   - Go to: https://docs.google.com/spreadsheets/d/13ukI4J5AQtzbRLEfyYABIhA7jCMH7g53veYQPVC5CWU/

2. **Open Apps Script Editor**
   - Click `Extensions` → `Apps Script`

3. **Add the Script**
   - Delete any existing code
   - Copy all code from `Google-Apps-Script.js`
   - Paste it into the Apps Script editor
   - Click the save icon (💾)

4. **Deploy as Web App**
   - Click `Deploy` → `New deployment`
   - Click the gear icon ⚙️ next to "Select type"
   - Choose `Web app`
   - Fill in the settings:
     - **Description**: "Printer Status API"
     - **Execute as**: `Me (your email)`
     - **Who has access**: `Anyone`
   - Click `Deploy`
   - Click `Authorize access` and grant permissions
   - Copy the **Web app URL** (it will look like: `https://script.google.com/macros/s/ABC.../exec`)

5. **Update the HTML File**
   - Open `printer-status.html`
   - Find line 296: `const SHEET_URL = 'YOUR_GOOGLE_APPS_SCRIPT_WEB_APP_URL_HERE';`
   - Replace with your Web App URL
   - Save the file

6. **Test It**
   - Open `printer-status.html` in a web browser
   - Data should load automatically and refresh every 30 seconds

---

### Option 2: Local CSV Upload (Manual Updates)

Use this if you don't want to set up Google Apps Script.

#### Steps:

1. **Open the Dashboard**
   - Open `printer-status-local.html` in a web browser

2. **Upload CSV File**
   - Click the "📁 Upload CSV File to Update Data" button
   - Select your `Printer Status Update - Dashboard.csv` file
   - Data will load immediately

3. **Update Data**
   - Export your Google Sheet as CSV (File → Download → CSV)
   - Upload the new CSV file to refresh the dashboard

---

### Option 3: Embed in Google Sites

Once you have either version working:

1. **Host the HTML file** on a web server (GitHub Pages, Google Drive, etc.)
2. **In Google Sites:**
   - Click `Insert` → `Embed`
   - Choose `Embed code` or `URL`
   - Paste your hosted HTML URL
   - Adjust size as needed

**OR**

1. **Copy all the HTML code** from `printer-status.html`
2. **In Google Sites:**
   - Click `Insert` → `Embed` → `Embed code`
   - Paste the entire HTML code
   - Click `Next` → `Insert`

---

## 🎨 Features

- ✅ Real-time status display for all printers (Currently just the 28 Prusas between watt and cooper)
- ✅ Color-coded status badges (Green=Available, Orange=In Use, Red=Offline)
- ✅ Filter by status (All, Available, In Use, Offline)
- ✅ Shows printer progress, time remaining, and current job

## 📊 Data Structure

Your Google Sheet should have this structure:
- **Row 1**: Notes
- **Row 2**: Printer names (Mini 1, Adobe 1, etc.)
- **Row 3**: Last Update timestamps
- **Row 4**: Status (PRINTING, IDLE, FINISHED)
- **Row 5**: Percent Complete
- **Row 6**: Time Remaining
- **Row 7**: Print Name label
- **Row 8**: Actual print job filename

## 🔧 Customization

### Change Colors

Edit the CSS in the `<style>` section:

```css
/* Background gradient */
background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);

/* Status colors */
.stat-card.available .stat-number { color: #10b981; } /* Green */
.stat-card.in-use .stat-number { color: #f59e0b; }    /* Orange */
.stat-card.offline .stat-number { color: #ef4444; }   /* Red */
```

### Change Refresh Rate

Find this line at the bottom of the script:

```javascript
setInterval(fetchPrinterData, 30000); // 30 seconds
```

Change `30000` to your desired interval in milliseconds (e.g., `60000` for 1 minute).

### Add Clemson Branding

Replace the gradient background:

```css
/* Clemson colors: Orange (#F66733) and Purple (#522D80) */
background: linear-gradient(135deg, #F66733 0%, #522D80 100%);
```

## ❓ Troubleshooting

### "Unable to load printer data"
- **With Google Apps Script**: Make sure you deployed the script and copied the correct Web App URL
- **With CSV**: Make sure the CSV file format matches the expected structure

### CORS Errors
- Direct CSV links from Google Sheets don't work due to CORS
- Use Google Apps Script method instead

### No Printers Showing
- Check browser console for errors (F12)
- Verify your CSV structure matches the expected format
- Make sure printer names contain "Mini", "Adobe", or "TAZ"

## 📝 License

Free to use for Clemson Makerspace and educational purposes.

---

**Donations** I accept paw points for caniac combos or starbucks
