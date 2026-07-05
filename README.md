# appsync_main_source

The **default** source repo for [AppSync](https://github.com/unix14/appSync).

Every AppSync client is seeded with `main` in its sources list on first launch,
and the entry cannot be removed from the Settings screen — it's the "always-on"
public catalog every device sees.

## What's in it

| App            | Kind       | Platforms          |
| -------------- | ---------- | ------------------ |
| Tailscale      | Play Store | Android TV, Mobile |
| Spotify        | Play Store | Android TV, Mobile |
| Downloader     | Play Store | Android TV         |
| SmartTube      | URL (APK)  | Android TV         |
| Button Mapper  | Play Store | Android TV, Mobile |
| File Manager+  | Play Store | Android TV, Mobile |
| Stremio        | Play Store | Android TV, Mobile |

Apps with `install_kind: play` open the Play Store to the package id. Apps with
`install_kind: url` are side-loaded from the APK URL in `apk_url`.

## How the Hub reads it

The Hub resolves a source name to `unix14/appsync_<name>_source/source.json`.
Adding a new source on a device (Settings → **+**) is just typing the `<name>`
part; the client's request goes to `POST /source/validate`, which fetches this
file's schema-validated equivalent from that repo.

Schema: [source.schema.json](https://github.com/unix14/appSync/blob/main/shared/schemas/source.schema.json).

## Updating

Push a change to `main` — the Hub re-fetches on the next `/catalog` request
(cache TTL is short) or on the next resync from any device. There's no
`app-manifest.json` here because this source only lists external apps; managed
apps still live in their own repos and are referenced by `app_repos` in a
group's entry.
