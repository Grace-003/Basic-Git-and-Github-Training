# Lab 6 — Tags & Releases

[← Back to index](README.md)

## Step 25 — Create a Tag

Terminal:

```bash
git tag                             # list existing tags
git tag -a v1.0.0 -m "first release"
git tag                             # v1.0.0 appears ✅
git push origin --tags              # push to GitHub
```

Go to GitHub → Tags — `v1.0.0` is visible ✅

## Step 26 — Create a GitHub Release

```
GitHub → your repo → Releases → Create a new release
→ Choose tag: v1.0.0
→ Title: First Release
→ Write description
→ Publish Release ✅
```

## Step 27 — Delete a Tag

Terminal:

```bash
git tag -d v1.0.0                       # delete locally
git push origin --delete v1.0.0        # delete from GitHub
```

---
Next: [Lab 7 — Inspection & Utilities](Lab7-Inspection-Utilities.md)
