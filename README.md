# BerrySMP resource pack

This repository hosts versioned Java resource-pack ZIPs for the network.

## Published pack

The first release mirrors the pack currently configured on Apoc Earth (the PEarth backend):

- [Download `pack.zip`](https://github.com/BerrySMP/resource-pack/releases/download/pack-2026-10-08-1/pack.zip)
- Version: `pack-2026-10-08-1`
- SHA-1: `4c139d3a63682161469cf1aaa199074f9679a04d`
- SHA-256: `1acb5fbc9936cddc06a52f3c5aa196f5604728829901d572d0bbf7bbe1691d1d`
- Source at publication: <https://lobfile.com/file/W8efRMeF.zip>

The GitHub download was checked anonymously against the source ZIP and matched both hashes. Apoc Earth's ItemsAdder configuration pointed to this first-release URL when it was published. GitHub serves release ZIPs as `application/octet-stream`, so ItemsAdder's `skip_url_file_type_check` is enabled for this verified URL. ItemsAdder accepted it after a reload on October 8, 2026. No server restart was triggered; player download and visuals have not yet been verified.

## Planned shared servers

This pack is intended to be shared by:

- Kiwi
- Mango
- Oneblock
- Survival
- Apoc Earth
- Power

The published ZIP is the current Apoc Earth pack only. It has not been merged or validated for the other listed servers. Kiwi, Mango, Oneblock, Survival, and Power have not been switched to a GitHub pack URL.

## Geyser reference files

Use [Geyser latest](geyser/latest/README.md) to record the most recent Geyser mappings and Bedrock `.mcpack` together. This folder is for reference and logging only; no server configuration should point to its files. It is empty until fresh files are uploaded and recorded.

## Upload a new pack ZIP to GitHub

Upload the pack as a **release asset** so it has its own versioned download link.

1. Put the finished ZIP on your computer and open it. `pack.mcmeta` and the `assets` folder must be directly inside the ZIP, not inside another folder. Name the ZIP `pack.zip`; renaming the file does not change its contents.
2. Sign in to a GitHub account with write access and open the [BerrySMP resource-pack repository](https://github.com/BerrySMP/resource-pack). Click **Releases** on the repository page, then **Draft a new release**.
3. Open **Choose a tag**, type a new tag such as `pack-YYYY-MM-DD-2`, and select **Create new tag**. Do not reuse a tag from an older pack. Target the `main` branch, enter a release title, and describe which server or source the ZIP came from.
4. Drag `pack.zip` into the release form's binary file box, or select it from your computer. Wait until the upload finishes and `pack.zip` appears in the file list. Click **Publish release**.
5. On the published release page, scroll to **Assets** below the release notes. Click **Assets** to expand the list if needed. Right-click the uploaded **pack.zip** file and choose **Copy link address** (in Chrome or Opera GX). Paste the copied link into a text editor to check it. Do **not** copy **Source code (zip)**; that contains this repository, not the Minecraft pack. Do not copy the browser address after starting a download, because GitHub may redirect to a temporary download address.

The release asset URL has this form:

```text
https://github.com/BerrySMP/resource-pack/releases/download/<tag>/pack.zip
```

For example, the [second release](https://github.com/BerrySMP/resource-pack/releases/tag/pack-2026-10-08-2) has this `pack.zip` link:

```text
https://github.com/BerrySMP/resource-pack/releases/download/pack-2026-10-08-2/pack.zip
```

## ItemsAdder config example

In `plugins/ItemsAdder/config.yml`, the GitHub link goes in `resource-pack.hosting.external-host.url`. This example shows the URL currently configured on Apoc Earth:

```yaml
resource-pack:
  hosting:
    external-host:
      enabled: true
      url: https://github.com/BerrySMP/resource-pack/releases/download/pack-2026-10-08-2/pack.zip
      skip_url_file_type_check: true
```

For a later release, replace the value after `url:` with that release's `pack.zip` asset link. Keep the other settings already in your server's config.

Before using the link on a server, open it once to confirm `pack.zip` downloads. Then update that server's ItemsAdder `external-host.url` to the versioned asset link as a separate rollout. GitHub release downloads may require `skip_url_file_type_check: true` because they use `application/octet-stream`; enable it only for a verified ZIP. Keep the previous URL for rollback, and follow that server's deployment schedule.
