# scrcpy-simple-helper

Interactive device selector for scrcpy with auto-reconnect and scaling.

## Quick install

```sh
curl -sSL https://raw.githubusercontent.com/YOUR_USER/android-screen-mirror/main/scrcpy-helper -o scrcpy-helper && chmod +x scrcpy-helper
```

## Usage

```sh
./scrcpy-simple-helper
```

- Picks a connected Android device from a numbered list
- Lets you choose screen scaling (0.25x–2x, or custom pixel value)
- Optionally turns the device screen off (-S)
- Auto-reconnects if the connection drops
- Press Q to quit at any time

## Requirements

- [adb](https://developer.android.com/studio/command-line/adb)
- [scrcpy](https://github.com/Genymobile/scrcpy)

## License

MIT
