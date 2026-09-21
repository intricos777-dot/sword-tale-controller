# Sword Tale: Lost Excalibur — Controller Support

Controller/gamepad support configuration for **Sword Tale: Lost Excalibur** (Steam App ID: 3305630).

## What this does

This repo provides controller input bindings so you can play Sword Tale: Lost Excalibur with a gamepad instead of keyboard and mouse.

## Installation

### Steam Input (recommended)

1. Right-click Sword Tale: Lost Excalibur in your Steam library
2. Select **Properties** → **Controller** → **General Controller Settings**
3. Enable your controller type (Xbox, PlayStation, etc.)
4. Steam Input will automatically provide gamepad support

### Manual configuration

Copy the files from this repo into your Proton prefix:

```bash
# Find your Proton prefix for this game
GAMEDIR="$HOME/.local/share/Steam/steamapps/compatdata/3305630"

# Copy the Input.ini
cp Input.ini "$GAMEDIR/pfx/drive_c/users/steamuser/AppData/Local/SwordTale/Saved/Config/WindowsNoEditor/Input.ini"
```

### For non-Steam play (lutris, heroic, etc.)

Use the `Input.ini` from this repo and place it in your game's Saved/Config directory.

## Controls

| Action | Keyboard | Gamepad |
|--------|----------|---------|
| Move Forward | W / Up | Left Stick Up |
| Move Backward | S / Down | Left Stick Down |
| Move Left | A / Left | Left Stick Left |
| Move Right | D / Right | Left Stick Right |
| Look/Turn | Mouse / A/D | Right Stick / Left Stick X |
| Jump | Space | A (Bottom Face) |
| Attack | Left Click | X (Right Face) |
| Attack 2 | Right Click | Y (Left Face) |
| Aim | Right Click Hold | Right Trigger |
| Dodge | Left Shift | LB |
| Use Item | E | RB |
| Cycle Inventory | Q | D-Pad Left |
| Open Map | M | D-Pad Up |
| Pause/Menu | Escape | Start/Select |
| Toggle Menu | F1 | D-Pad Right |
| Quick Save | F5 | B |
| Quick Load | F8 | A |

## UE4 Input.ini

The `Input.ini` file contains Unreal Engine 4 input bindings that map both keyboard and gamepad inputs. UE4's built-in gamepad support handles the translation automatically when Steam Input is enabled.

## Compatibility

Tested with:
- Steam Input (SteamOS / Linux / Windows)
- Xbox controllers (native XInput)
- PlayStation controllers (via DS4Windows or Steam Input)
- Generic SDL2 gamepads

## Troubleshooting

If controller doesn't work:
1. Verify Steam Input is enabled for this game in Steam properties
2. Check that your controller is detected by Steam
3. Ensure the Input.ini is in the correct Saved/Config path
4. Try restarting the game after applying the config

## License

MIT
