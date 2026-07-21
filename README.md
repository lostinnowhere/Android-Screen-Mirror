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

## Usage

The script shows all connected devices, a scale menu, and a screen-off toggle. You enter everything in one compact string:

| Input | Meaning |
|-------|---------|
| `12` | Device 1, screen on, no scaling (1x) |
| `124` | Device 1, screen on, scale 4 (1x) |
| `123` | Device 1, screen on, scale 3 (0.75x) |
| `122` | Device 1, screen off, scale 2 (0.5x) |
| `121280` | Device 1, screen off, max-size 1280 (720p on a 1080p tablet) |
| `111920` | Device 1, screen on, max-size 1920 (1080p) |
| `21600` | Device 2, screen on, max-size 600 |
| `221` | Device 2, screen off, scale 1 (0.25x) |
| `1` | Device 1, screen on, no scaling |

**Format:** first char = device number, second char = screen on(1) / off(2), rest = scale (1-8) or pixel max-size.

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

For a specific output resolution, enter the pixel value directly (e.g. `1280` for 720p).

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
