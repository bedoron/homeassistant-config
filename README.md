# homeassistant-config

This repository is now a **legacy snapshot/reference copy** of older Home Assistant files.

Operational Home Assistant work should happen in:

- the live host at `192.168.14.48`
- `../home-services/hassio/homeassistant/`

Do **not** treat this repository as an active source of truth anymore.

## What lives here

- Top-level Home Assistant YAML files such as `configuration.yaml`, `automations.yaml`, `scripts.yaml`, `groups.yaml`, `climate.yaml`, `media_player.yaml`, and `switch.yaml`
- `lovelace-storage.json`, an exported snapshot of the storage-mode main dashboard
- `ui-lovelace.yaml`, which is not present in the deploy tree under `home-services/hassio/homeassistant/`
- `Remote 1.txt` and `Remote 2.txt`, which appear to be reference material for IR or remote-control related setup

## What is missing

Compared with `home-services/hassio/homeassistant/`, this repository does not include several pieces of the deployed Home Assistant tree, including:

- `secrets.yaml`
- `google_service_account.json`
- `webostv.conf`
- `.HA_VERSION`
- `.storage/`
- `blueprints/`

Because of those gaps, this repository should be treated as a partial snapshot or reference copy rather than the full runtime configuration.

## Source of truth

The authoritative Home Assistant configuration should be treated as the config on the Home Assistant host at `192.168.14.48`. When local copies disagree:

1. Prefer the remote host as the current truth.
2. Use `home-services/hassio/homeassistant/` as the single maintained local deployable tree.
3. Treat this repository as archival/reference material only.

Remote verification showed that `/config` on the host resolves to `/homeassistant`. That remote tree currently includes items such as `.storage/`, `blueprints/`, `esphome/`, `google_assistant_integ.yaml`, `light.yaml`, `scenes.yaml`, `secrets.yaml`, and `webostv.conf`, which are not represented here as a complete set.

The remote host did not contain `ui-lovelace.yaml` during verification, so treat this repository as a curated subset rather than a direct mirror.

## Accessing the live Home Assistant config

Use the remote host when you need the real runtime configuration instead of this curated subset:

```powershell
Start-Service ssh-agent
ssh-add $HOME\.ssh\id_rsa
ssh root@192.168.14.48
```

Useful remote checks:

```sh
readlink -f /config
ls -la /homeassistant
find /config -maxdepth 3 -type l -ls
```

For a quick one-shot check from PowerShell:

```powershell
ssh root@192.168.14.48 "readlink -f /config; ls -la /homeassistant"
```

## File locations

- Live Home Assistant config on the host: `/homeassistant`
- Host alias path: `/config -> /homeassistant`
- Local deployable tree: `../home-services/hassio/homeassistant/`
- This repository: selected top-level YAML files and `ui-lovelace.yaml`

## When to use this repo

Use this repository only when you need historical reference from the older flat snapshot. For active HA edits, switch to `home-services` or read the remote host directly.
