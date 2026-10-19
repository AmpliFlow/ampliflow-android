# AmpliFlow for Android

Install the official AmpliFlow Android APK from [Releases](https://github.com/AmpliFlow/ampliflow-android/releases). This public repository contains installation instructions, Obtainium configuration and release downloads, not the application source. The source is maintained privately.

## Install and update with Obtainium

1. Install [Obtainium](https://github.com/ImranR98/Obtainium/releases).
2. Use the Add to Obtainium link below on your Android device and confirm the import.
3. Check for updates in Obtainium, review the release notes, then install AmpliFlow. Android may ask you to allow installation from Obtainium.

[Add to Obtainium](https://apps.obtainium.imranr.dev/redirect?r=obtainium%3A%2F%2Fapp%2F%257B%2522id%2522%253A%2522com.ampliflow.mobile%2522%252C%2522url%2522%253A%2522https%253A%252F%252Fgithub.com%252FAmpliFlow%252Fampliflow-android%2522%252C%2522author%2522%253A%2522AmpliFlow%2522%252C%2522name%2522%253A%2522AmpliFlow%2522%252C%2522additionalSettings%2522%253A%2522%257B%255C%2522includePrereleases%255C%2522%253Atrue%252C%255C%2522verifyLatestTag%255C%2522%253Afalse%252C%255C%2522apkFilterRegEx%255C%2522%253A%255C%2522%255EAmpliFlow-android-v%255B0-9%255D%252B%255C%255C%255C%255C.%255B0-9%255D%252B%255C%255C%255C%255C.%255B0-9%255D%252B%2528%253F%253A-%255B0-9A-Za-z%255D%252B%2528%253F%253A%255B.-%255D%255B0-9A-Za-z%255D%252B%2529%252A%2529%253F%255C%255C%255C%255C.apk%2524%255C%2522%257D%2522%257D)

If the link does not open, download [obtainium.json](https://raw.githubusercontent.com/AmpliFlow/ampliflow-android/main/obtainium.json) and use Obtainium's Import/Export screen to import it. Alternatively, add the app manually:

| Setting | Value |
| --- | --- |
| App source URL | `https://github.com/AmpliFlow/ampliflow-android` |
| App name | `AmpliFlow` |
| Package ID | `com.ampliflow.mobile` |
| Include prereleases | On |
| Verify latest tag | Off (`verifyLatestTag: false`) |
| APK filename filter (regular expression) | `^AmpliFlow-android-v[0-9]+\.[0-9]+\.[0-9]+(?:-[0-9A-Za-z]+(?:[.-][0-9A-Za-z]+)*)?\.apk$` |

This GitHub distribution repository is public: no GitHub token is needed. Prereleases must be included because `android-v0.9.1` is a prerelease. The filter selects only versioned `AmpliFlow-android-vVERSION.apk` files, excluding checksums, signatures and certificates.

The config uses Obtainium's JSON-encoded string for `additionalSettings`. The link imports the same app object via the supported `obtainium://app/<URL-encoded JSON>` scheme, wrapped in the official redirect for browser compatibility. See the [Obtainium deep-link documentation](https://wiki.obtainium.imranr.dev/deep_links/) and [upstream import/export implementation](https://github.com/ImranR98/Obtainium/blob/main/lib/models/app.dart).

## Install an APK directly

Open [Releases](https://github.com/AmpliFlow/ampliflow-android/releases), choose the release, and download only `AmpliFlow-android-vVERSION.apk`. Open it on Android and allow installation from your browser or file manager if prompted. Check release notes before updating. Do not install checksum or certificate files as apps. If no APK is listed, wait for the release upload; do not substitute an unofficial download.

## Signing and existing installations

The current signed APK is version **0.9.1**, version code **10**, package **`com.ampliflow.mobile`**. Its signing certificate SHA-256 fingerprint is:

```text
337b062a4b5754ec1fa4b99dec109851473bd22ccb5919d1ea5d02301ed2d8ab
```

Updates must preserve the package ID and signing identity. A debug-signed build cannot update in place to this release-signed build. If Android reports a signature conflict, stop: do not uninstall or clear app data without a state-recovery plan. First confirm how to recover your account access and any local-only state with your AmpliFlow administrator or support contact. Obtainium cannot bypass Android's signature checks.

## Diagnostics and usage measurement

Distributed APKs always send Sentry diagnostics and Rybbit usage events; there is no telemetry opt-out. Activity notifications are a separate, optional feature.

- **Sentry:** sanitized native Java/ANR failure locations (exception type and verified code-only frames), app release, environment, source commit, a fixed failure category and numeric HTTP status when present. Raw exception messages, account/tenant/activity IDs, credentials, request/response contents, URLs, headers/cookies, user fields, extras/contexts, breadcrumbs, locals and attachments are removed. Automatic sessions, tracing/profiling, replay, logs/metrics, screenshots and view hierarchy are disabled.
- **Rybbit:** four fixed native actions (foreground, notification enabled, notification opened, download saved), schema version, app version/code and environment. Events contain no explicit user/account/tenant ID, page URL/content, notification content, file name/content or device fingerprint.

Both collectors/proxies receive connection metadata, including source IP addresses. Rybbit can derive server-side visitor IDs, so requests are not described as anonymous. Event counts are best-effort, not total user counts or proof of successful notification delivery. Read each release's notes for collection and retention caveats.
