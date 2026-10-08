# BerrySMP resource pack

This repository hosts versioned Java resource-pack ZIPs for the network.

## Published pack

The first release mirrors the pack currently configured on Apoc Earth (the PEarth backend):

- [Download `pack.zip`](https://github.com/BerrySMP/resource-pack/releases/download/pack-2026-10-08-1/pack.zip)
- Version: `pack-2026-10-08-1`
- SHA-1: `4c139d3a63682161469cf1aaa199074f9679a04d`
- SHA-256: `1acb5fbc9936cddc06a52f3c5aa196f5604728829901d572d0bbf7bbe1691d1d`
- Source at publication: <https://lobfile.com/file/W8efRMeF.zip>

The GitHub download was checked anonymously against the source ZIP and matched both hashes. No Minecraft server configuration has been changed to use GitHub yet.

## Planned shared servers

This pack is intended to be shared by:

- Kiwi
- Mango
- Oneblock
- Survival
- Apoc Earth
- Power

The published ZIP is the current Apoc Earth pack only. It has not been merged or validated for the other listed servers. None of these servers has been switched to a GitHub pack URL.

## Publish a pack version

1. Download the exact intended ZIP from its current source. Keep its bytes unchanged.
2. Check that the archive opens and contains `pack.mcmeta` at its root. Record its SHA-1 (`Get-FileHash -Algorithm SHA1` on Windows).
3. Create a GitHub Release with a new version tag and attach the ZIP as `pack.zip`. GitHub's automatically generated “Source code (zip)” is a repository archive, not a Minecraft pack.
4. Confirm that the release asset downloads anonymously and that its SHA-1 matches the source ZIP.
5. In a separately authorized rollout, update the intended server's ItemsAdder `external-host.url` to the **versioned release asset URL** and follow that server's deployment schedule. Keep the previous URL for rollback.

The release asset URL has this form:

```text
https://github.com/BerrySMP/resource-pack/releases/download/<tag>/pack.zip
```

Do not point a server at a GitHub URL until the asset and download check are complete.
