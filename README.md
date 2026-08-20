# Seltzer Sounds Audio — update manifest

One file, read by Seltzer Sounds Audio apps to answer a single question: is there a
newer version than the one I am running?

This repository is public **on purpose**, and it is the only public part of any
of it. An app cannot carry a password to read a private file — anything
embedded in a shipped binary can be pulled straight back out of it — so the
version numbers live somewhere that needs no credentials at all.

What that discloses: that a version exists. Nothing else. No code, no
installers, no artwork. The download links point at private repositories, so
anyone who is not an invited collaborator follows them to a 404.

## Format

```json
{
  "<app-id>": {
    "version": "1.2.0",
    "url": "https://github.com/<owner>/<repo>/releases/latest",
    "notes": "optional one-liner shown next to the button"
  }
}
```

Rules the apps enforce, so a mistake here cannot become a security problem:

- `version` must be plain dotted digits — `1.2.0`, not `v1.2.0` or `1.2-beta`.
- `url` must be **https** and its host must be on the app's own allowlist
  (`github.com` or `seltzersounds.com`). A link anywhere else is ignored.
- Nothing is ever downloaded or installed by an app. The button opens this page
  in a browser; the person installs it themselves, so macOS checks the
  signature and the notarisation ticket.

## Adding an app

Add a key. That is the whole job — the mechanism is already in every app.

## Releasing a new version

1. Ship the build (`macapp/release.sh` in the app's repo) and publish the
   release with the DMG attached.
2. Bump `version` here and push.

Order matters: bump this only once the release is actually downloadable, or
everyone is told to fetch something that does not exist yet.
