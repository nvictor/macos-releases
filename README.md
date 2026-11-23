# macos-releases

Public home for signed, notarized macOS app releases and their Sparkle appcasts.
App source repos stay private or public as they like. Sparkle only talks to this repo.

## Layout

- `<App>/appcast.xml`: Sparkle feed, written by CI on each release.
- Releases: one per app version, tagged `<app>-v<version>` (e.g. `bars-v1.2.3`), holding the DMG and deltas.
- `templates/release.yml`: app-agnostic release workflow to copy into each app repo.

## Feed URL

```
https://raw.githubusercontent.com/nvictor/macos-releases/main/<App>/appcast.xml
```

Set it as `SUFeedURL` in the app's `Info.plist`.

## Add an app

- Copy `templates/release.yml` to `<app>/.github/workflows/release.yml`.
- Set `SUFeedURL` to the feed URL above.
- Add the `RELEASES_TOKEN` secret to the app repo (fine-grained PAT, only `nvictor/macos-releases`, Contents: read and write).
- Release: `git tag v1.2.3 && git push origin v1.2.3`.

## Rules

- Never commit binaries to the repo. DMGs live only in Releases.
- Only CI writes `<App>/appcast.xml`.
