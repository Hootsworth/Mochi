# Mochi Inbox

Mochi is a static Gmail inbox client. Firebase Authentication provides Google sign-in; Gmail messages are read and changed through the Gmail API using the signed-in user's Google OAuth access token. Firestore is not used for Gmail data.

## Deploy to Vercel

Import this directory as a Vercel project and deploy with the **Other** framework preset. No build command or environment variables are required. The root URL is rewritten to `mochi-inbox.html` by `vercel.json`.

## Firebase and Google setup

The Firebase web app config is in `mochi-inbox.html`. It is a client identifier, not a server credential. In Firebase Console:

1. Enable Google under **Authentication → Sign-in method**.
2. Add the deployed Vercel hostname (and any custom hostname) under **Authentication → Settings → Authorized domains**.
3. In Google Cloud Console for the same project, enable the **Gmail API** and configure the OAuth consent screen. Add `gmail.modify` and `gmail.send` scopes. While the app is in testing mode, add each tester's Google account.
4. Ensure the Google OAuth web client used by Firebase permits the Firebase auth handler domain `auth-plain.firebaseapp.com`.

The app requests `gmail.modify` to display, mark, archive, star, and delete mail, and `gmail.send` to compose and reply. Google may require consent screen verification before these scopes can be used by a public production audience. Gmail access tokens live in memory and are reacquired on sign-in; Firebase persists the user session.

## Local preview

Serve this directory over HTTP (for example, `python3 -m http.server 8000`) and open `http://localhost:8000`. Firebase Authentication must allow `localhost` in its authorized domains.
