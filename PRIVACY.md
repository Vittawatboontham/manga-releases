# Privacy Policy — Singh Manga eiei

_Last updated: 2026-10-10_

Singh Manga eiei is a free, sideloaded manga reader. This describes what the app collects, why,
who can read it, and how to turn it off or erase it. We collect the minimum needed for the features
below and never sell data.

## What's collected

| Data | When | Why | Stored where |
|------|------|-----|--------------|
| Anonymous account id | First launch | Back up your library to the cloud and sync it. Without signing in, the account belongs to this install: a reinstall or a new phone starts empty unless you sign in (Google or Microsoft) first | Firebase Auth |
| Library: bookmarks (series titles and cover links), reading history (series and chapter titles, the page you reached), read/unread chapters, categories, reading status, links between copies of a series from different sources, and the rest of what syncs per item: your ratings (with any note), the Read next queue, shelves, per-manga reader settings, titles you hid or snoozed, and display titles you chose | While you use the app | Cloud backup and cross-device sync | Cloud Firestore, under your account; readable by you in the app and by the project admins in the Firebase console |
| Google or Microsoft account (name, email, photo) | Only if you sign in with Google or Microsoft | Link your sync data to a recoverable account | Cloud Firestore, under your account |
| AniList access token | Only if you connect AniList | Push your reading progress to your AniList list | On this device only |
| **Approximate location** (a ~5 km grid cell, stored as a geohash; never your exact coordinates) | **On by default** ("Nearby readers"), once you allow Android's location permission; refreshed each launch while on | Not used by any feature yet: matching nearby readers is not built | Cloud Firestore, under your account |
| **Contacts** (a one-way SHA-256 hash of each phone number; never names, never the numbers themselves) | **On by default** ("Find friends"), once you allow Android's contacts permission; while on, sent again only when your contacts change or you use another account | Not used by any feature yet: matching friends is not built | Cloud Firestore, under your account |
| Series catalogue: the title, source, slug, cover link and cover image of series the app shows you | As you browse | Keep browsing working when a source site is down | Shared Firestore/Storage catalogue; not tied to your account |
| Trending counter: a series' title, slug and source, plus a +1, once per series per install when you read it | When you read a series | Build the shared popularity list | Shared Firestore collection; not tied to your account |
| Bug reports you send: device details, Android and app version, your settings, the titles of up to 40 bookmarks and 15 recent history entries, and your note. Crash records the app uploads itself (see below) go to the same place | When you send a report. A crash record is saved on the device when the app crashes and uploaded on a later launch, with no prompt, once the app has an account to send it under | Fix problems | Firestore `bug_reports`, tagged with your anonymous id; read by the project admins |

The contact hashes are **unsalted** SHA-256 of phone numbers. A phone number has few possible values, so
someone who could read the hashes could recover numbers by guessing them. They are readable only by you
(the database rules) and by the project admins in the Firebase console.

**The project admins review reading activity.** For accounts linked to Google or Microsoft, the admins may look at the
library and reading history synced to the account, together with its sign-in email (for example a private report of the
most-read series and each reader's recent reads), to understand what is read. It is never sold or shared. Reading in
Incognito, not linking an account in the app, or not signing in on the web keeps a read out of it.

### Analytics and crash reports

- **Google Analytics (anonymous usage events):** events such as `series_opened` and `chapter_read`
  carry a source name and series/chapter ids, **never titles** and never the text you search for. They are
  not tied to your account.
- **Crashlytics (crash reports):** a stack trace, device details and the app version. Its user id is your anonymous
  Firebase id, so a crash can be matched to your synced library if you ask us to look into it. A crash report
  also carries a short trail of coarse app events (screen names, which source site is in use, sync status,
  source failures), never titles or ids, and none of the reading ones while Incognito is on.
- Crash records the app also uploads to Firestore by itself, on a later launch and without asking, carry the
  same device details, version and stack trace plus the error message, tagged with the same id. They are the
  `bug_reports` rows above.

### App Check (telling the real app from scripts)

Release builds attach a Firebase App Check token to their requests to Firebase. Google's Play Integrity service issues it,
to show that the request comes from the real Singh Manga app and not from a script. The token holds no personal data, no
account id and nothing from your library. Because the app is sideloaded, Play Integrity is set to accept builds installed
outside Google Play; the check is about the app, not about you.

### Incognito ("Private reading")

Turn it on under Settings → Privacy, or for this session only. While it is on:

- the reader saves **no history, progress or read state**, sends **no `chapter_read` event**, and does not feed
  recommendations; so none of that reaches sync, the trending counter or AniList;
- opening a series sends no `series_opened` event, and switching to another source does **not** link the two
  automatically (a link is saved and synced with titles);
- what you search for is not added to your recent searches, and opening a result from a search is not kept as
  a "Worked before" suggestion; the "For you" rail does not note which titles it showed or which you opened
  (the search itself still works, and the sites it asks still see the words);
- the Recents preview is blank on Android 13 and later.

It does **not** cover what you do by hand: bookmarks, chapters you mark read, links you confirm, and downloads
are saved (and synced) as usual. Local books you import keep their page on this device. The manga sites and
your network can still see what you load and search for. "This session only" survives Android freeing the app's
memory in the background and ends when you end it or close the app and open it again.

## Your control

- **Location** ("Nearby readers") and **Contacts** ("Find friends") are **on by default** for everyone, new
  installs and existing ones (this update switches both on once, even if you had turned them off before). On
  first launch the app explains what they share, then Android asks for each permission. **Nothing is uploaded
  until you have seen that explanation and allowed the permission** (even one you allowed in an earlier
  version); refuse a permission and that feature is turned off. Turn either off any time in
  Settings → Privacy to stop collection and erase what was stored for it; that choice stays, including after
  signing out, "Delete my cloud data" (which turns both off itself) and restoring a backup. Revoking the
  permission later in Android settings also turns the feature off and erases what was stored. The switches are
  **not** restored from a backup: a restore leaves this device's switches as they are.
- **Sign out** (Settings → Account) asks whether to keep or remove this device's library. If you remove it,
  the library is cleared from this device and nothing from the old session syncs to the new one.
- **Delete my cloud data** (Settings → Account) erases your synced data and your account. Deleting the app
  removes everything on the device.
- The shared catalogue and trending counters are not tied to your account, so they cannot be erased per user.

## Backups

Backup files you export (or the automatic backups you turn on) are plain JSON in the place you choose. They
hold your library, history, search history and settings. They do **not** hold your AniList token, the
Location/Contacts switches, sync state or the download index.

## Permissions

- `ACCESS_COARSE_LOCATION`: asked for once at first launch, because Nearby readers is on by default (and again
  only if you switch it back on in Settings); coarse, foreground-only (never background).
- `READ_CONTACTS`: asked for at the same time, because Find friends is on by default; the app reads phone
  numbers only (not names) and uploads a one-way hash of each.
- `POST_NOTIFICATIONS`: new-chapter alerts. On Android 13 and later it is asked for once your library has a bookmark
  (normally when you bookmark your first series; a library restored or synced from another device counts too),
  not when the app starts. If Android is blocking the alerts, Settings → Updates says so and offers to open Android's
  notification settings. On a locked screen the alert hides the series title.
- `REQUEST_INSTALL_PACKAGES`: to install the app's own updates (the app is sideloaded, not on Play Store).

## The web version (Singh Manga Web)

The web version is the same reader in a browser, installable as an app. It reads the same manga sites and shows the same
library when you sign in. What differs:

- **Not signed in:** nothing about you reaches your account. Your library (bookmarks, history, read chapters, ratings and
  notes, shelves) stays in this browser's storage (IndexedDB); clearing the site's data erases it. The browser still talks to
  the host of the web app (a server the owner rents from Amazon Web Services in Sydney, Australia, reached through an ngrok tunnel; ngrok and that server see your IP address and the pages you request), to Google (Firebase Remote
  Config, to learn about maintenance and paused sources, which sends a Firebase installation id and your IP address; and
  Firebase Storage for cover images, which sees your IP address) and to the manga sites you read from, which see your IP
  address and the pages you load, as in the app (except for the sources read through the relay, described in the next item). On phones and in Safari, the page also loads Google's sign-in script
  (apis.google.com) and a manga-singh-eiei.firebaseapp.com frame as soon as it opens, before you sign in or decide to, so Google
  receives your IP address and the address of the site.
- **Through the web app's relay:** the web app is served from the owner's server (Amazon Web Services, Sydney). For nano, dark-manga, speed-manga,
  zen-manga, kingsmanga, whytoon and bully-manga (their lists, searches, series and chapter pages), and for the lists and
  series pages (covers, genres and status) of up-manga, slow-manga, sing-manga, flash-manga and mangakimi, your browser asks
  a small program on that server, the relay, to fetch the page. Those sources then see that server's IP address (an AWS
  address), not yours, and no Origin header from your browser; the owner's server, and the ngrok tunnel in front of it, handle the
  addresses you open and what you search on them. The relay keeps a copy of each source page for up to 10 minutes and sets no
  cookies. go-manga, and the searches, chapter lists and chapter pages of the other five, go straight from your browser to
  the source, which sees your IP address. Page images, and covers that come from a source, load straight from the source
  into your browser (or from the copy this browser keeps); the relay never carries images. While you read a chapter, the web
  version also downloads the rest of it and the next chapter in advance (not with the browser's Data Saver on), so a source
  sees requests for pages you may never open.
- **Signed in with Google or Microsoft** (the same providers as the app; the web never creates an anonymous account): it uses
  the same account as the app, so the same library syncs both ways: bookmarks, reading history, read chapters, categories,
  reading status, ratings and notes, Read next, shelves, per-manga reader settings, hidden titles and display titles. When the
  build has a reCAPTCHA key, the page loads Google reCAPTCHA (App Check) before its first request to your account, to prove the
  request comes from the real site; Google receives your IP address and browser details for that. While signed in, the browser
  also keeps the Firebase account session (account id, name, email and photo link) and an App Check token. The web does not use
  contacts, location, analytics or crash reports, and it never writes the links between sources (it reads them to file your
  ratings under the right title).
- **Sign out** asks whether to keep or remove this browser's copy of the library, and removes the account session; the App Check
  token stays until the site's data is cleared. "Remove" first sends any change not yet in your account, and does nothing if it
  cannot. "Delete my cloud data" in the app erases what the web wrote too, since both use one account.
- The web app itself sets no cookies (Google's reCAPTCHA, when loaded, may). Its service worker stores the app's own files and
  copies of the page images and covers you have seen (about 1,000 at most, the oldest dropped first), and the page lists of the
  chapters you opened, or that were fetched ahead, are kept for a week, to load faster. "Remove this browser's library", and
  signing out with "Remove", delete them too.

## Third parties

Google (Firebase Auth, Firestore, Storage, Analytics, Crashlytics, Remote Config, and App Check with Play Integrity,
which checks that requests come from this app) receives the data above and the technical data any connection
carries (IP address). The manga source sites you read from see your IP
address and the pages you load. AniList sees your progress if you connect it. Microsoft sees the sign-in if you
sign in with Microsoft. GitHub sees your IP address when the app checks for updates.

## Contact

Maintainer: Singh. Questions or deletion requests: open an issue on the public releases repo.
