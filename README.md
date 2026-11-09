# TizenTube Persian subtitles

Modified TizenTube userscript for **TizenTube Cobalt (Android TV)** that:

- keeps **auto-translated Persian (`fa`) subtitles** selected on every video, including after
  the next video in a playlist / autoplay starts,
- shows **only Persian** in the caption language pickers (the auto-translate list and the
  language list), so the player cannot silently fall back to English/original subtitles,
- re-applies Persian if the caption track gets reset (track list change, caption settings
  change, new video).

Based on [reisxd/TizenTube](https://github.com/reisxd/TizenTube) (GPL-3.0). Changes are limited
to `mods/features/persianCaptions.js` plus one import line in `mods/userScript.js` and the
`enablePersianCaptions: true` default in `mods/config.js`.

## Files

| File | Purpose |
| --- | --- |
| `fa.js` | The built userscript that the modified app downloads. Must keep this exact name and stay in the repository root. |
| `LICENSE` | GPL-3.0 license of the original project. |

## Uploading

1. Open <https://github.com/parsadegame/TizenTube_persiansub>
2. **Add file → Upload files**
3. Drag in `fa.js` and `LICENSE` (they must land in the repository **root**, not in a folder)
4. **Commit changes** to the `main` branch

The app fetches:

```
https://cdn.jsdelivr.net/gh/parsadegame/TizenTube_persiansub/fa.js
```

Check that URL in a browser after uploading — it must return the JavaScript file, not a 404.

### Two rules

- **Do not rename the repository** (the URL is compiled into the APK and cannot be changed
  afterwards).
- **Do not create releases or git tags** in this repository. The version-less jsDelivr URL
  prefers tags over branches, so a tag would start serving a pinned old copy.

### After editing `fa.js`

jsDelivr caches files for up to ~12 hours. To force a refresh, open:

```
https://purge.jsdelivr.net/gh/parsadegame/TizenTube_persiansub/fa.js
```

## Disabling the behaviour

The mod is on by default. To turn it off without changing this repo, set
`enablePersianCaptions` to `false` in the TizenTube settings storage
(`localStorage["tizentube-config"]`); the rest of TizenTube keeps working.

## Installable APK

The companion build (`TizenTube-FA-2.0.3-arm.apk`) is TizenTube Cobalt 2.0.3 with:

- package id `io.gh.parsa.tizentube.persian` (so it installs next to the official app),
- launcher label `PersianTT`,
- userscript URL pointed at `fa.js` in this repository.

Because the package id and signing key are different, it does **not** replace or update the
official app, and the official app's updater will not overwrite it.
