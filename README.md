# Android Screen Mirror

Interactive Android device selector for scrcpy with auto-reconnect and scaling. Intended for Linux.

## Quick install

```sh
mkdir -p ~/Projects && curl -sSL https://raw.githubusercontent.com/lostinnowhere/Android-Screen-Mirror/main/scrcpy-helper -o ~/Projects/scrcpy-helper && chmod +x ~/Projects/scrcpy-helper && echo "Saved to ~/Projects/scrcpy-helper"
```

## Usage

```sh
./scrcpy-helper
```

- Picks a connected Android device from a numbered list
- Lets you choose screen scaling (0.25x–2x, or custom pixel value)
- Optionally turns the device screen off
- Auto-reconnects if the connection drops
- Press Q to quit at any time

## Requirements

### Linux host
- bash 3.2+, coreutils
- [adb](https://developer.android.com/studio/command-line/adb)
- [scrcpy](https://github.com/Genymobile/scrcpy)

Alpine Linux users: install `bash` from the main repo first.

### Android device
The device must have **USB debugging** enabled. To enable it:

1. Open **Settings → About phone** and tap **Build number** 7 times to unlock developer options
2. Go to **Settings → System → Developer options**
3. Enable **USB debugging**
4. Connect the device to your computer via USB and accept the **Allow USB debugging?** prompt on the device

For wireless connections (optional), enable **Wireless debugging** in Developer options and pair via `adb pair`.

No root access is required. scrcpy handles the screen mirroring and audio forwarding automatically once debugging is granted.

## License

MIT
