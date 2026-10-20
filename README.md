<!-- Watermark: Living_Sin (intricos777-dot) + AI agents (Hermes, Lia, opencode) - collaborative work -->
# Sword Tale: Lost Excalibur — Controller / Gamepad Support

Controller remap for **Sword Tale: Lost Excalibur** (Steam App ID: **3305630**,
UE 4.18). Works on **Windows, Linux, macOS (Whisky/Crossover), and Steam Deck**
— any OS or kernel that runs the game, because it does not patch the game: it
layers **Unreal Engine's native `Input.ini`** on top of the game's built-in
bindings.

The game's default gamepad scheme is awkward (`RT = Dodge`, `LT = Charge`,
`RB = Block`, slots unbound). This repo re-forges it into a souls-style layout:

## The layout

| Action           | Gamepad (Steam/Xbox labels)        |
|------------------|------------------------------------|
| **Attack**       | **RT** — Right Trigger             |
| **Block / Defend** | **LT** — Left Trigger            |
| Charge (heavy)   | RB — Right Shoulder                |
| Dodge            | LB — Left Shoulder                 |
| Jump             | A                                  |
| Interact         | B                                  |
| Inventory        | X                                  |
| Sprint           | Y                                  |
| WeaponToggle     | L3 (left stick click)              |
| SkillTree        | R3 (right stick click; keyboard `K` kept) |
| Item Slot 1–4    | D-pad Up / Down / Left / Right     |
| Item Slot 5      | Select / Back                      |
| Pause / Menu     | Start / Menu                       |
| Move             | Left stick (unchanged)             |
| Camera           | Right stick (unchanged)            |

Keyboard/mouse bindings are untouched.

---

## Install — Method A: drop-in `Input.ini` (recommended, all OS)

The file [`Input.ini`](Input.ini) goes into the game's *Saved* config directory
(Unreal Engine merges it over the built-in defaults at launch — no mod loader,
no game files touched).

### 1. Find your Saved config directory

| OS | Path |
|----|------|
| **Windows** | `%LOCALAPPDATA%\SwordTale\Saved\Config\WindowsNoEditor\` |
| **Linux / Steam Deck** (Proton) | `~/.steam/steam/steamapps/compatdata/3305630/pfx/drive_c/users/steamuser/AppData/Local/SwordTale/Saved/Config/WindowsNoEditor/` |
| **macOS** (Whisky / CrossOver bottle) | inside the bottle: `drive_c/users/<user>/AppData/Local/SwordTale/Saved/Config/WindowsNoEditor/` |
| **Heroic / Lutris (non-Steam)** | your prefix's `drive_c/users/<user>/AppData/Local/SwordTale/Saved/Config/WindowsNoEditor/` |

### 2. Place the file

Copy `Input.ini` from this repo into that directory.

- **Linux / Steam Deck (copy-paste):**

  ```bash
  PREFIX="$HOME/.steam/steam/steamapps/compatdata/3305630/pfx"
  DEST="$PREFIX/drive_c/users/steamuser/AppData/Local/SwordTale/Saved/Config/WindowsNoEditor"
  mkdir -p "$DEST"
  cp Input.ini "$DEST/Input.ini"
  ```

- **Windows (PowerShell):**

  ```powershell
  $DEST = Join-Path $env:LOCALAPPDATA 'SwordTale\Saved\Config\WindowsNoEditor'
  New-Item -ItemType Directory -Force -Path $DEST | Out-Null
  Copy-Item .\Input.ini (Join-Path $DEST 'Input.ini')
  ```

- **Steam Deck:** run the Linux command in Desktop Mode's terminal (Konsole).
  The `~/.steam` home directory is writable even when the SD card/read-only
  root is not — this path is gated-mode safe.

### 3. Launch

Start the game through Steam. Unreal reads `Input.ini` at startup and merges it
over the pak's `DefaultInput.ini` — no other action needed.

> **Back up first.** If you ever want the stock layout, delete or rename the
> `Input.ini` you placed (the game ships its defaults inside the pak, so it
> restores itself). Keep a copy of your own edits if you tweaked further.

---

## Method B: Steam Input (client-side, optional)

The `Input.ini` above is authoritative for the engine. You can additionally
tune deadzones/haptics in **Steam → Settings → Controller**, but do not remap
primary actions there — let `Input.ini` own them to avoid double-binding.

For controller **detection / calibration** in Steam:

1. Steam → **Settings → Controller → General Controller Settings**
2. Tick your controller types (Xbox / PlayStation / Switch Pro / Generic)
3. **Steam → Settings → Controller → Test** (or the calibration UI on Deck)
4. Deadzone: UE already applies `GamepadDeadZone=0.300000`; most pads need no
   extra adjustment.

**Steam Deck:** the built-in layout editor will show the game's *actions*
(Attack, Block, Charge, Dodge, …) because they come from the engine bindings —
you can pin extra shortcuts to them, but the trigger/slot layout above is already
what the engine reads.

---

## Method C: device-level remap (last resort)

If you cannot place a file (e.g. cloud-only play from a locked machine) and
Steam Input fails to pick up the actions, remap at the device layer:

- **Windows:** built-in Xbox Accessories app, or reWASD — swap triggers online:
  RT→LT, LT→RT, Shoulders, flip D-pad and Select as in the layout table.
- **Linux:** `steamos-input` / `xpadneo` or Steam Input's own per-game layout
  (Controller → Edit Layout → map physical triggers to the actions).
- **Steam Deck:** Edit Layout in the game's controller config.

Note Method C only rearranges *buttons* — the engine still decides what each
action does. For a layout identical to this repo, prefer Method A.

---

## Troubleshooting

| Symptom | Fix |
|---------|-----|
| Controller does nothing | Enable the controller type in Steam **General Controller Settings**; check the pad registers in Steam's Test screen |
| Old bindings still fire (e.g. RB also blocks) | Both lines (removal `-` and addition `+`) must be present in `Input.ini`; confirm the file is in `WindowsNoEditor` (not `LinuxNoEditor`/top-level Saved) and restart the game |
| Layout works but triggers feel twitchy | Fine-tune `GamepadDeadZone` in `Input.ini` (already 0.30) |
| Using Heroic/Lutris and Steam Input absent | Method A still works — it is engine-level, Steam-independent |
| Custom tweaks vanish after an update | The game does not touch `Saved/Config`; re-copy only if you reset the prefix |
| Can't reach the path (macOS/Whisky) | In Whisky, right-click the bottle → Open C: Drive, then follow `users/<user>/AppData/Local/SwordTale/Saved/Config/WindowsNoEditor` |

---

## Files

- `Input.ini` — the engine-level remap (works on every OS/kernel).
- `README.md` — this guide.

## License

MIT. This repo contains **no game files** — only configuration directives and
documentation for Unreal Engine's public config system.