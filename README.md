# Sound of Math — F-Droid Repository

A self-hosted F-Droid repository for distributing the **Sound of Math** app
outside the main F-Droid repo.

## Structure

```
sound-of-math-fdroid/
├── .github/
│   └── workflows/
│       └── fdroid.yml        # CI workflow that builds & publishes the repo
├── metadata/
│   └── YOUR.PACKAGE.NAME.yml # App metadata (rename to your real package id)
├── repo/
│   └── sound-of-math.apk     # The APK(s) served by this repo
├── icons/
│   └── YOUR.PACKAGE.NAME.0.png # App icon used in the repo listing
├── fdroid/
│   └── config.yml            # fdroidserver repo configuration
├── .gitignore
└── README.md
```

## Setup

1. Rename `metadata/YOUR.PACKAGE.NAME.yml` and
   `icons/YOUR.PACKAGE.NAME.0.png` to match your app's actual package ID
   (e.g. `com.example.soundofmath.yml`).
2. Edit `fdroid/config.yml` with your repo URL, name, and description.
3. Drop your signed release APK into `repo/`.
4. Install `fdroidserver` locally to initialize keys and generate the index:
   ```bash
   pip install fdroidserver
   fdroid init
   fdroid update --create-metadata
   ```
5. Commit and push — the GitHub Actions workflow in
   `.github/workflows/fdroid.yml` will rebuild the index and publish
   `repo/` to GitHub Pages on every push to `main`.

## Adding this repo to F-Droid client

Once published, users can add it in the F-Droid app via:

```
https://yourusername.github.io/sound-of-math-fdroid/repo
```

(Replace with your actual GitHub Pages URL.)

## Notes

- Keep your signing keystore **out of version control** (see `.gitignore`).
- `fdroid update` regenerates `index.xml`, `index-v1.json`, and related
  index files in `repo/` — these are ignored by git and rebuilt by CI.
