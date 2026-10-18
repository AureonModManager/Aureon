# Publishing Aureon updates

This repository can host Aureon's update manifest and release installers.

## Important: do not enable the update feed yet

The current Aureon v1.8.5 source still defines `AUREON_VERSION=L"1.7.6"`, even though the UI says v1.8.5. Correct this to `1.8.5`, rebuild and test on Windows **before** enabling automatic updates for users.

The example at `updates/latest.example.json` is a template, **not a live update feed**.

## Publishing v1.8.5

1. Open **Releases → Draft a new release** in this repository.
2. Create tag `v1.8.5`, title `Aureon v1.8.5`.
3. Upload the actual tested installer asset named `AureonSetup_v1.8.5.exe`.
4. Write patch notes, then publish the release.
5. Compute the SHA-512 of that **exact published installer**; in PowerShell use: `Get-FileHash .\AureonSetup_v1.8.5.exe -Algorithm SHA512`.
6. Copy `updates/latest.example.json` to repository-root `update.json`; verify that the asset URL, SHA-512, version and notes match the published release. Never point a live manifest to an absent asset.
7. Aureon supports a manifest with the exact keys: `version`, `notes`, `installer_url`, `sha512`. The hash must be 128 hexadecimal characters.

## Feed URL

Once `update.json` is published on `main`, the feed URL will be:

`https://raw.githubusercontent.com/AureonModManager/Aureon/main/update.json`

To test on an Aureon installation, open **Settings → Update Settings**, put that HTTPS URL as the first line of `update_channel.txt`, save, and use **Check for Updates**.

For a public release, configure the same verified HTTPS URL in `release_channel.hpp` as `AUREON_DEFAULT_UPDATE_FEED` and ship a rebuilt, tested installer, so users do not need manual setup. Keep previous installations' settings in mind.

## New releases

For a future version (e.g. `v1.9.0` Halloween Update): build and test the app, set its internal `AUREON_VERSION` accurately, publish the new EXE to a release, calculate its exact SHA-512, and only then update `update.json`. Users will then see its patch notes and can opt to update.

## Safety

Only publish binaries you built and verified. Test actual installation/update on Windows and backup important data. Ensure updating preserves worlds and modpacks. Hash verification protects downloads from accidental corruption but does not replace trustworthy hosting or code signing.
