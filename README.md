# Financial Record (installable app)

One web app for iPhone, iPad and Mac. It reads and writes your "Financial Document" Google Sheet directly. The sheet stays the database.

Files: `index.html` (the app), `config.js`, `manifest.webmanifest`, `sw.js`, and three icons. Keep them together in one folder.

## 1. Get a Google sign-in key (about 10 minutes, free, once)

1. Go to https://console.cloud.google.com and create a project (any name).
2. APIs & Services > Library > search **Google Sheets API** > Enable.
3. APIs & Services > OAuth consent screen: choose **External**, fill in an app name and your email, then under **Test users** add your own Google address. Leave it in Testing. No Google review is needed for one person.
4. APIs & Services > Credentials > Create credentials > **OAuth client ID** > type **Web application**.
   - Authorised JavaScript origins: the site address, for example `https://yourname.github.io`
   - Authorised redirect URIs: the full address of the app, for example `https://yourname.github.io/financial-record/` (with the final slash). The app shows the exact address on its first screen.
5. Copy the **Client ID**. It ends with `.apps.googleusercontent.com`.

## 2. Put the folder online (any free static host)

The app must be served over https. Easy options:
- **Netlify Drop** (app.netlify.com/drop): drag the folder in, you get an address at once.
- **GitHub Pages** or **Cloudflare Pages**: upload the folder as a repository.

Then add your final address to the OAuth client in step 1 (origin and redirect URI).

## 3. First open

Open the address. Paste the Client ID (or put it in `config.js` before uploading to skip this on every device), press Save, then Sign in with Google. Choose the account that owns the sheet. In Testing mode Google shows "Google hasn't verified this app": press Advanced > Continue. That is expected for your own app.

## 4. Install it

- **iPhone / iPad:** open the address in Safari > Share > **Add to Home Screen**.
- **Mac:** Safari > File > **Add to Dock**, or in Chrome use the install icon in the address bar.

## Good to know

- The Google sign-in lasts about an hour. When it ends the app signs in again quietly, or shows a Sign in button.
- The page re-reads the sheet every minute while open, and after every save.
- Dates on SET 50, Fund, USD and Shopping are still stamped by the sheet's own formulas.
- To use a different sheet, set `sheetId` in `config.js`: `window.FIN_CONFIG = { clientId: "...", sheetId: "..." }`.
- In Testing mode Google may ask you to sign in again every 7 days. Publishing the consent screen to Production removes that, still without review for personal use.
