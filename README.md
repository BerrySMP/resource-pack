# BerrySMP resource pack

This repository is the GitHub home for the Java resource pack used by the network. Pack ZIPs belong in **versioned GitHub Releases** so each server can use a fixed download URL.

## Current source

Survival's ItemsAdder `external-host.url`, checked on 2026-10-08:

<https://download.mc-packs.net/pack/4f248ff935587104fced3f690e59a3910cac2522.zip>

Power and Mango currently advertise the same link. The exact ZIP from that link is the intended first release asset. No release has been published yet because the source host returns HTTP 403 to the setup computer. A server-generated or older local ZIP must not be substituted for the configured download.

## Publish a pack version

1. Download the exact ZIP from the source link above. Keep its bytes unchanged.
2. Check that the archive opens and contains `pack.mcmeta` at its root. Record its SHA-1 (`Get-FileHash -Algorithm SHA1` on Windows).
3. Create a GitHub Release with a new version tag, such as `pack-2026-10-08-1`, and attach the ZIP as `pack.zip`. GitHub's automatically generated “Source code (zip)” is a repository archive, not a Minecraft pack.
4. Confirm that the release asset downloads anonymously and that its SHA-1 matches the source ZIP.
5. Update each intended server's ItemsAdder `external-host.url` to the **versioned release asset URL** and follow that server's deployment schedule. Keep the previous URL for rollback.

The release asset URL has this form:

```text
https://github.com/BerrySMP/resource-pack/releases/download/<tag>/pack.zip
```

Do not point a server at a GitHub URL until the asset and download check are complete.
