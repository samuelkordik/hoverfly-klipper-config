# Hoverfly — Klipper / Moonraker config

Live configuration for **Hoverfly**, a heavily-modified Creality Ender 3 Pro
running Klipper on `delicass` (a ThinkPad P52s). Companion to the main build
log at <https://github.com/samuelkordik/Hoverfly>.

Hardware: SKR Mini E3 V2.0, Sprite Extruder Pro (direct drive), CRTouch probe,
series-wired dual Z. The Hoverfly repo has the full story and migration history.

## What's tracked

This repo uses a **default-deny `.gitignore`** (public-repo safety): only the
hand-authored config files are committed, so secrets and third-party/generated
files can never be pushed by the automated backup.

| File | What it is |
| --- | --- |
| `printer.cfg` | Klipper config — calibrated PID, `rotation_distance`, bed mesh, macros |
| `moonraker.conf` | Moonraker API server config |
| `crowsnest.conf` | Webcam (Logitech C615) config |
| `timelapse.cfg` | moonraker-timelapse macros |

**Deliberately NOT tracked** (excluded by `.gitignore`):

- `moonraker-obico.cfg` — contains a private Obico auth token
- `printer-*.cfg` — Klipper `SAVE_CONFIG` auto-backups
- `mainsail.cfg`, `moonraker_obico_macros.cfg` — third-party symlinked configs
- any `*.backup` / `*.bkp`

## Automated backup

A `systemd` timer on the host commits and pushes changes on a schedule. A
pre-commit **secret scan** aborts the push if anything sensitive (tokens, keys,
private-key blocks) ever appears in a tracked file — belt-and-suspenders on top
of the default-deny ignore.

## License

[GPLv3](./LICENSE).

_Backup automation verified active: 2026-07-09_
