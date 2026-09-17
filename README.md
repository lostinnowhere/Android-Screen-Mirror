# Android Screen Mirror

Interactive Android device selector for scrcpy with auto-reconnect and scaling. Intended for Linux.

## Quick install

```sh
mkdir -p ~/Projects && curl -sSL https://raw.githubusercontent.com/lostinnowhere/Android-Screen-Mirror/master/scrcpy-helper -o ~/Projects/scrcpy-helper && chmod +x ~/Projects/scrcpy-helper
```

Then run:

```sh
~/Projects/scrcpy-helper
```

## Fast-connect CLI

Skip all prompts with one argument:

```
~/Projects/scrcpy-helper --<dev><screen>-<scale|res>[-<fps>]
```

| Part | Meaning |
|------|---------|
| `dev` | Device number (1..N) |
| `screen` | `1` = keep screen on, `2` = turn screen off |
| `scale\|res` | Scale preset 1-8 (0.25x..2x), or pixel value for the longest side |
| `fps` (optional) | scrcpy `--max-fps` cap, e.g. 30, 60 |

Examples:

```sh
~/Projects/scrcpy-helper --12-960-30   # device 1, screen off, 960px longest side, 30fps cap
~/Projects/scrcpy-helper --11-6        # device 1, screen on, scale 6 (1.5x)
~/Projects/scrcpy-helper --12-1280     # device 1, screen off, 1280px, no fps cap
~/Projects/scrcpy-helper --help        # show usage
```

## Usage

The script shows all connected devices, a scale menu, and a screen-off toggle. You enter everything in one compact string:

| Input | Meaning |
|-------|---------|
| `12` | Device 1, screen on, no scaling (1x) |
| `124` | Device 1, screen on, scale 4 (1x) |
| `123` | Device 1, screen on, scale 3 (0.75x) |
| `122` | Device 1, screen off, scale 2 (0.5x) |
| `12960` | Device 1, screen off, longest side 960px (renders 600x960 on a 1200x1920 tablet) |
| `111920` | Device 1, screen on, longest side 1920px |
| `21600` | Device 2, screen on, longest side 600px |
| `221` | Device 2, screen off, scale 1 (0.25x) |
| `1` | Device 1, screen on, no scaling |

**Format:** first char = device number, second char = screen on(1) / off(2), rest = scale (1-8) or pixel value for the longest side.

A pixel value or non-1x scale sets the Android rendering resolution:
`adb shell wm size WxH` (aspect ratio preserved). Choosing 1x resets any
leftover override, so the device renders at its native resolution.

### Scale presets

| # | Scale |
|---|-------|
| 1 | 0.25x |
| 2 | 0.5x |
| 3 | 0.75x |
| 4 | 1x (default) |
| 5 | 1.25x |
| 6 | 1.5x |
| 7 | 1.75x |
| 8 | 2x |

For a specific output resolution, enter the target longest-side pixel value directly (e.g. `960` to render at 960p, `1280` for 720p-class output).

### Live monitoring

While scrcpy is running, the terminal logs battery level and temperature whenever they change:

```
  [14:35:22]  Battery: 85%  Temp: 28.0C
  [14:42:10]  Battery: 84%  Temp: 28.5C
```

Press **Q** in the terminal to kill scrcpy and quit.

### Auto-reconnect

- If the device disconnects (USB unplugged, WiFi drops), the script waits for it to come back and reconnects automatically
- On retry, the device screen is turned off regardless of the original choice
- Press **Q** at any time to quit

### Requirements

- bash 3.2+, coreutils
- [adb](https://developer.android.com/studio/command-line/adb)
- [scrcpy](https://github.com/Genymobile/scrcpy)

Alpine Linux users: install `bash` from the main repo first.

### Android device setup

1. **Settings → About phone** → tap **Build number** 7 times
2. **Settings → System → Developer options** → enable **USB debugging**
3. Connect via USB and accept the **Allow USB debugging?** prompt

For wireless connections, enable **Wireless debugging** in Developer options and pair via `adb pair`.

No root required.

## License

MIT
