# Album of the Day

A shared log for the album each of us listens to every day: favorite songs, a rating if you want one,
a ranking against everything else, and a queue of albums to hear next, tagged with who suggested them.

It is a static site (`index.html`, `config.js`). Data lives in Firebase Firestore so everyone sees one log.

## Connect the shared database (about 5 minutes)

Until this is done the site works but saves to the current browser only.

1. Go to https://console.firebase.google.com and create a project (turn Google Analytics off).
2. Build → Firestore Database → Create database → production mode, any region.
3. Firestore → Rules → paste the contents of `firestore.rules` → Publish.
4. Project settings (gear) → Your apps → Web (`</>`) → register an app → copy the `firebaseConfig` values.
5. Paste them into `config.js`, commit and push. The site updates in a minute or so.

The config values are not secret. The rules let anyone with the link read and write, so keep the link
among friends. To lock it down later, add Firebase Auth and tighten `firestore.rules`.

## Data

Three collections: `albums` (title, artist, year, status `listened` or `queue`, date, suggestedBy),
`logs` (one per album and person: rating, favorites, note) and `ranks` (one per person: ordered album ids).
The group ranking averages each person's position.

## Run locally

```bash
python3 -m http.server 8000
```
