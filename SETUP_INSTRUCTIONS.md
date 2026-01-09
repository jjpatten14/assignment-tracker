# Google Sheets Sync Setup Instructions

Follow these steps to enable cross-device synchronization for your Assignment Tracker.

---

## Step 1: Create Google Cloud Project

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Click **"Create Project"**
3. Project name: `Assignment Tracker`
4. Click **"Create"**
5. Wait for the project to be created (notification will appear in top-right)

---

## Step 2: Enable Google Sheets API

1. Make sure your new project is selected (check the project name in the top bar)
2. Go to **"APIs & Services"** > **"Library"** (use the left sidebar menu)
3. Search for: `Google Sheets API`
4. Click on **"Google Sheets API"**
5. Click **"Enable"**
6. Wait for it to enable (you'll be redirected to the API dashboard)

---

## Step 3: Create OAuth 2.0 Credentials

1. Go to **"APIs & Services"** > **"Credentials"**
2. Click **"Create Credentials"** > **"OAuth client ID"**
3. If prompted to configure OAuth consent screen:
   - Click **"Configure Consent Screen"**
   - Choose **"External"** (unless you have a Google Workspace account)
   - Click **"Create"**
   - Fill in required fields:
     - App name: `Assignment Tracker`
     - User support email: (your email)
     - Developer contact: (your email)
   - Click **"Save and Continue"**
   - Skip "Scopes" section (click **"Save and Continue"**)
   - Skip "Test users" section (click **"Save and Continue"**)
   - Click **"Back to Dashboard"**
4. Return to **"Credentials"** tab
5. Click **"Create Credentials"** > **"OAuth client ID"**
6. Application type: **"Web application"**
7. Name: `Assignment Tracker Web Client`
8. Under **"Authorized JavaScript origins"**, click **"Add URI"**
   - Add your hosting URL (examples below)
   - For GitHub Pages: `https://yourusername.github.io`
   - For Netlify: `https://your-site-name.netlify.app`
   - For local testing: `http://localhost:8000` (won't work with OAuth)
9. Click **"Create"**
10. **IMPORTANT**: Copy the **Client ID** that appears (starts with numbers and ends with `.apps.googleusercontent.com`)
    - Save this somewhere safe! You'll need it later
11. Click **"OK"**

---

## Step 4: Create API Key

1. Still in **"Credentials"**, click **"Create Credentials"** > **"API key"**
2. **IMPORTANT**: Copy the **API Key** that appears
   - Save this somewhere safe! You'll need it later
3. Click **"Restrict Key"** (recommended for security)
4. Name: `Assignment Tracker API Key`
5. Under **"API restrictions"**:
   - Select **"Restrict key"**
   - In the dropdown, find and select **"Google Sheets API"**
6. Click **"Save"**

---

## Step 5: Create Google Sheet

1. Go to [Google Sheets](https://sheets.google.com)
2. Click **"Blank"** to create a new spreadsheet
3. Name it: `Assignment Tracker Data` (click the title at the top to rename)
4. At the bottom, click on the sheet tab name (probably "Sheet1")
5. Rename it to: `CompletionState`
6. In cell **A1**, type: `Assignment_ID`
7. In cell **B1**, type: `Completed`
8. **IMPORTANT**: Copy the **Spreadsheet ID** from the URL:
   - The URL looks like: `https://docs.google.com/spreadsheets/d/SPREADSHEET_ID_HERE/edit`
   - The Spreadsheet ID is the long string of letters and numbers between `/d/` and `/edit`
   - Example: If URL is `https://docs.google.com/spreadsheets/d/1BxiMVs0XRA5nFMdKvBdBZjgmUUqptlbs74OgvE2upms/edit`
   - Then Spreadsheet ID is: `1BxiMVs0XRA5nFMdKvBdBZjgmUUqptlbs74OgvE2upms`
   - Save this somewhere safe! You'll need it later

---

## Step 6: Update HTML File

1. Open `assignment-tracker-cloud.html` in a text editor
2. Find the `CONFIG` object (around line 318-325):
   ```javascript
   const CONFIG = {
       CLIENT_ID: 'YOUR_CLIENT_ID_HERE.apps.googleusercontent.com',
       API_KEY: 'YOUR_API_KEY_HERE',
       SPREADSHEET_ID: 'YOUR_SPREADSHEET_ID_HERE',
       SHEET_NAME: 'CompletionState',
       SCOPES: 'https://www.googleapis.com/auth/spreadsheets'
   };
   ```
3. Replace the placeholder values:
   - Replace `YOUR_CLIENT_ID_HERE.apps.googleusercontent.com` with your **Client ID** from Step 3
   - Replace `YOUR_API_KEY_HERE` with your **API Key** from Step 4
   - Replace `YOUR_SPREADSHEET_ID_HERE` with your **Spreadsheet ID** from Step 5
4. Save the file

**Example of filled CONFIG:**
```javascript
const CONFIG = {
    CLIENT_ID: '123456789-abc123def456.apps.googleusercontent.com',
    API_KEY: 'AIzaSyABC123DEF456GHI789JKL012MNO345PQR',
    SPREADSHEET_ID: '1BxiMVs0XRA5nFMdKvBdBZjgmUUqptlbs74OgvE2upms',
    SHEET_NAME: 'CompletionState',
    SCOPES: 'https://www.googleapis.com/auth/spreadsheets'
};
```

---

## Step 7: Host Online

**The tracker MUST be hosted online for Google OAuth to work. You have several free options:**

### Option A: GitHub Pages (Recommended - Free & Easy)
1. Create a GitHub account if you don't have one
2. Create a new repository (e.g., `assignment-tracker`)
3. Upload `assignment-tracker-cloud.html`
4. Go to repository Settings > Pages
5. Under "Source", select "main" branch
6. Click "Save"
7. Your site will be at: `https://yourusername.github.io/assignment-tracker/assignment-tracker-cloud.html`
8. **IMPORTANT**: Add this URL to "Authorized JavaScript origins" in Step 3

### Option B: Netlify (Free)
1. Go to [netlify.com](https://www.netlify.com/)
2. Drag and drop your `assignment-tracker-cloud.html` file
3. Your site will be at: `https://random-name.netlify.app`
4. **IMPORTANT**: Add this URL to "Authorized JavaScript origins" in Step 3

### Option C: Vercel (Free)
1. Go to [vercel.com](https://vercel.com/)
2. Import your project
3. Deploy
4. **IMPORTANT**: Add the deployment URL to "Authorized JavaScript origins" in Step 3

**Note:** Localhost won't work with Google OAuth for security reasons.

---

## Step 8: Test It Out!

1. Open your hosted tracker in a web browser
2. You should see a **"Sign In with Google"** button at the top
3. Click it and sign in with your Google account
4. Grant permission to access Google Sheets
5. Check off some assignments
6. Open the Google Sheet you created - you should see the data appear!
7. Open the tracker on another device (phone, tablet, etc.)
8. Sign in with the same Google account
9. Your checked assignments should sync across devices!

---

## Troubleshooting

### "Access blocked: This app's request is invalid"
- Make sure the hosting URL is added to "Authorized JavaScript origins" in Google Cloud Console
- Make sure you're using HTTPS (not HTTP)
- Wait a few minutes after updating settings for changes to propagate

### "The OAuth client was not found"
- Double-check that you copied the Client ID correctly
- Make sure the Client ID ends with `.apps.googleusercontent.com`

### "API key not valid"
- Double-check that you copied the API Key correctly
- Make sure the API Key is restricted to Google Sheets API

### "Unable to read from spreadsheet"
- Double-check the Spreadsheet ID is correct
- Make sure the sheet is named exactly `CompletionState`
- Make sure you've signed in with the same Google account that owns the sheet

### Sign-in button doesn't appear
- Check browser console for errors (F12 > Console)
- Make sure both Google API scripts are loading
- Check that CONFIG values are filled in correctly

---

## Security Notes

- **Never share your API Key or Client ID publicly** if you restrict them properly
- The OAuth consent screen will show a warning that the app is "unverified" - this is normal for personal projects
- Only your Google account can access your assignment data
- The app stores a backup in localStorage even when using Google Sheets

---

## Benefits of Cloud Sync

✅ **Cross-device access** - Check assignments on your phone, see updates on your laptop
✅ **Automatic backup** - Data stored in Google Sheets (plus localStorage backup)
✅ **No data loss** - Works offline, syncs when back online
✅ **Secure** - Only accessible with your Google account
✅ **Same interface** - Looks and works exactly like the original

---

## Still Using Local Version?

The original `assignment-tracker.html` file remains unchanged and works independently with localStorage only. You can use both versions:
- `assignment-tracker.html` - Local storage only (no sign-in needed)
- `assignment-tracker-cloud.html` - Google Sheets sync (requires setup)

---

## Need Help?

If you encounter issues:
1. Check the browser console (F12 > Console tab) for error messages
2. Verify all steps were completed exactly as written
3. Double-check all credentials are copied correctly (no extra spaces)
4. Make sure the hosting URL matches what's in "Authorized JavaScript origins"
