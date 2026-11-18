# Publishing সেনানথি, step by step

Follow the parts in order. Parts 1 to 4 are needed; Part 5 removes the small address bar in the Android app; Part 7 is optional.

You need: your GitHub account (`Mahmud629`), the Google Cloud project you already set up, and the separate **senanothi-signing-key** folder (keep that folder private; never upload it).

---

## Part 1. Put the project on GitHub

1. Unzip the project. You get a folder named `Shena-nothi`.
2. Open **github.com/Mahmud629/Shena-nothi**.
3. Press **Add file**, then **Upload files**.
4. Open the unzipped `Shena-nothi` folder, select **everything inside it** (including the `.github` folder and the `.nojekyll` file), and drag it into the GitHub page.
   - On Windows, if `.github` or `.nojekyll` is hidden, in File Explorer choose **View**, then **Show**, then **Hidden items**.
5. Press **Commit changes**.
6. Check the repository now shows `.github`, `android`, `user-site`, `index.html`, `README.md` and `PUBLISHING.md`.

**If the `.github` folder did not upload:** press **Add file**, then **Create new file**, type the name `.github/workflows/build-apk.yml`, paste the contents of that file from the zip, and press **Commit changes**.

## Part 2. Check the website

1. In the repository, open **Settings**, then **Pages**.
2. Source: **Deploy from a branch**. Branch: **main**, folder **/ (root)**. Press **Save** if anything changed.
3. After a minute, open **https://mahmud629.github.io/Shena-nothi/** and press Ctrl+F5.

## Part 3. Let anyone with Gmail log in

1. Open **console.cloud.google.com** and select your project.
2. Search for **Google Auth Platform** and open **Audience**.
3. Press **Publish app** and confirm.
4. Under **Branding**, check the app name, support email and the home page `https://mahmud629.github.io/Shena-nothi/`.

Publishing is free. While the app is in *Testing*, only the 100 test users you listed can log in.

## Part 4. Build the Android APK

### 4a. Add the signing key to GitHub (once)

The APK must always be signed with the same key, or phones will refuse updates.

1. In the repository, open **Settings**, then **Secrets and variables**, then **Actions**.
2. Press **New repository secret** four times and add these, copying each value from `KEY-DETAILS.txt` in the signing-key folder:

| Name | Value |
|---|---|
| `KEYSTORE_BASE64` | the whole contents of `keystore-base64.txt` (one long line) |
| `KEYSTORE_PASSWORD` | the password in `KEY-DETAILS.txt` |
| `KEY_ALIAS` | `senanothi` |
| `KEY_PASSWORD` | the same password |

### 4b. Run the build

1. Open the **Actions** tab of the repository. If GitHub asks, press **I understand my workflows, go ahead and enable them**.
2. Choose **Build Android APK** on the left, press **Run workflow**, then **Run workflow** again.
3. Wait 3 to 6 minutes for a green tick.
4. Open the **Releases** page (right side of the repository's front page). The newest release has **senanothi.apk**.

The permanent download link for the newest APK is:
**https://github.com/Mahmud629/Shena-nothi/releases/latest/download/senanothi.apk**

**If the build fails (red cross):** open the failed run, click the red step, copy the error lines and send them to me.

## Part 5. Open full screen, without an address bar

Android shows a thin address bar unless the website proves the app belongs to it. The proof file must sit at `https://mahmud629.github.io/.well-known/assetlinks.json`, which needs a second repository.

1. On GitHub, press **+**, then **New repository**.
2. Name it exactly **`Mahmud629.github.io`**, make it **Public**, and press **Create repository**.
3. Press **uploading an existing file** and upload everything inside the project's `user-site` folder: `.nojekyll`, `index.html` and the `.well-known` folder. Press **Commit changes**.
   - If the `.well-known` folder will not upload, press **Add file**, then **Create new file**, type `.well-known/assetlinks.json`, paste that file's contents, and commit.
4. Open **Settings**, then **Pages**, and set Branch **main**, folder **/ (root)**.
5. After a few minutes, open **https://mahmud629.github.io/.well-known/assetlinks.json**. You should see the text with your fingerprint.
6. On the phone, uninstall and reinstall the APK. It now opens full screen.

This file only works with the APK signed by your release key (Part 4a).

## Part 6. Share the app

- **Android users:** send the link `https://github.com/Mahmud629/Shena-nothi/releases/latest/download/senanothi.apk`. They open the downloaded file and allow installing unknown apps when asked. Google Chrome must be installed.
- **iPhone users:** an APK does not run on iPhone. They open `https://mahmud629.github.io/Shena-nothi/` in Safari, then Share, then **Add to Home Screen**.

### Updating the app

- **Changes to the app itself** (`index.html`): upload the new file to the repository. Both the website and the Android app use it straight away; nobody needs a new APK.
- **Changes to the Android wrapper** (`android/` folder, icon or name): upload them, and a new APK builds automatically. Users install it over the old one.

## Part 7 (optional). Google Play Store

- A Google Play developer account costs a **one-time US$25**.
- Upload **senanothi.aab** from the release (not the APK).
- Play needs a privacy policy page, screenshots and a short description.
- New personal developer accounts must run a closed test with at least 12 testers for 14 days before going public.
- Play may re-sign the app with its own key; it then shows a new fingerprint under **App integrity**, which must be added to `assetlinks.json` as a second entry.

---

Prepared by: BA 11108 Capt Asif Mahmud, Sigs
