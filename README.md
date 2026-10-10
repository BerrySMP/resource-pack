# BerrySMP resource pack

This repository hosts versioned Java resource-pack ZIPs for the network.

## Which server uses which pack (2026-10-10)

Each link below is a versioned release asset. Every server's ItemsAdder `resource-pack.hosting.external-host.url` points at one of them. The old `download.mc-packs.net` links were replaced because that service is rate-limiting, returning errors and blocking some IPs.

| Release | Servers | Contents |
|---|---|---|
| [`shared-2026-10-10`](https://github.com/BerrySMP/resource-pack/releases/download/shared-2026-10-10/pack.zip) | Survival, PowerSMP, AvatarSMP Survival, Mango, Apoc Earth (Hub's config too, but ItemsAdder isn't running there) | The shared network pack: Muertos and Hellborn, the Polygony Nexus set, the dev-store assets, PokePals and BerryGuide. Replaces `shared-2026-10-09` (same content without PokePals/BerryGuide) as each server switches at its daily restart |
| [`kiwi-2026-10-09`](https://github.com/BerrySMP/resource-pack/releases/download/kiwi-2026-10-09/pack.zip) | Kiwi | Kiwi's own pack, until its ItemsAdder item IDs are aligned with the shared pack |
| [`oneblock-grape-2026-10-10`](https://github.com/BerrySMP/resource-pack/releases/download/oneblock-grape-2026-10-10/pack.zip) | Oneblock Grape | Grape's own pack plus PokePals and BerryGuide, until its ItemsAdder item IDs are aligned. Replaces `oneblock-grape-2026-10-09` at Grape's daily restart |
| [`earth-classic-2026-10-09`](https://github.com/BerrySMP/resource-pack/releases/download/earth-classic-2026-10-09/pack.zip) | Earth-Classic | Earth-Classic's separate full pack (stays separate) |
| [`avatar-hub-2026-10-09`](https://github.com/BerrySMP/resource-pack/releases/download/avatar-hub-2026-10-09/pack.zip) | AvatarSMP Hub | AvatarSMP Hub's own pack |

IslandSMP serves its pack from the server itself (ItemsAdder `simple_self_host`), so it isn't listed here. Each release's notes give the exact SHA-1 and SHA-256 hashes and the source.

### Why some servers can't share the pack yet

ItemsAdder gives each custom item a `custom_model_data` number per server, stored in `plugins/ItemsAdder/storage/items_ids_cache.yml`. A pack only shows the right textures on servers whose numbers match:

- Survival, PowerSMP, AvatarSMP Survival and Mango have identical caches. Hub and Apoc Earth are compatible with them.
- Kiwi differs on about 50 items, Grape on about 62, and Earth-Classic almost entirely.

Before moving a server onto the shared pack, align its cache, at a scheduled restart.

The Nexus items in the shared pack use `custom_model_data` 9100000 and up, a range ItemsAdder's own numbering won't reach.

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

In `plugins/ItemsAdder/config.yml`, the GitHub link goes in `resource-pack.hosting.external-host.url`. This example shows the shared pack URL:

```yaml
resource-pack:
  hosting:
    external-host:
      enabled: true
      url: https://github.com/BerrySMP/resource-pack/releases/download/shared-2026-10-10/pack.zip
      skip_url_file_type_check: true
```

For a later release, replace the value after `url:` with that release's `pack.zip` asset link. Keep the other settings already in your server's config.

Before using the link on a server, open it once to confirm `pack.zip` downloads. Then update that server's ItemsAdder `external-host.url` to the versioned asset link as a separate rollout. GitHub release downloads need the file-type check skipped because they use `application/octet-stream`. Older ItemsAdder versions call the key `skip-url-file-type-check___DONT_ASK_HELP_IF_SET_TRUE`; enable it only for a verified ZIP. Keep the previous URL for rollback, and follow that server's deployment schedule.
