# Aureon v1.8.6 — update bootstrap

The user has already published v1.8.5 as a **pre-release**. Its internal version is incorrectly set to 1.7.6, so automatic update comparisons are unreliable.

Version **1.8.6** corrects the internal number, sets the default update feed URL, and treats empty legacy update settings as the default. A compiled v1.8.6 installer is available in the conversation. It has passed EXE payload and static import checks, **but has not been run on Windows**.

## Before enabling automatic updates

1. Install and test v1.8.6 on Windows. Back up important Minecraft saves.
2. Create a GitHub pre-release tag `v1.8.6` and upload the exact `AureonSetup_v1.8.6.exe`.
3. Check its SHA-256: `ee8199f9ded7f94572dfedf7f858307159c148122e1df478c11140f9e41235e7`.
4. When the asset is published and verified, create `update.json` at the repository root with:

```json
{
  "version": "1.8.6",
  "notes": "Update channel setup, corrected version detection, and improved upgrade compatibility.",
  "installer_url": "https://github.com/AureonModManager/Aureon/releases/download/v1.8.6/AureonSetup_v1.8.6.exe",
  "sha512": "31b81ecbabef988f3facab5a079c14ad05f8081c7ceb435ec412178caec6974656ebcf4cbc4b658b6f0b90739540d0c5e1809208142d06f34fa32ab16d6d112f"
}
```

The updater reads these exact JSON keys: `version`, `notes`, `installer_url`, `sha512`. Its default feed is `https://raw.githubusercontent.com/AureonModManager/Aureon/main/update.json`.

**Do not create a live update.json before publishing and verifying its installer.** Old v1.8.5 users must install v1.8.6 once manually; only future updates can be detected automatically.
