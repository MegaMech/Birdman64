## What's new in 1.4.1

**Android:** no more copying the ROM by hand — on first start, the game's opening
screen offers **"Choose a game file"**, which opens your phone's normal file browser.
Pick your Pilotwings 64 (US) file from wherever it is (Downloads, Drive, USB) and
it is copied into the app's storage and remembered: every later launch starts
straight away. A wrong file says why, and you can pick again.

### Added

- Android: choose the ROM with the system file picker on first start (or whenever
  the ROM is missing); the choice is remembered across launches. No storage
  permission is needed.

**Windows:** download `Birdman64-windows-x64.zip`. **Linux:** download the `.AppImage`.

**Android (experimental):** sideload `Birdman64-android-arm64.apk` (64-bit phones,
Android 8+) and start it. The first launch builds the game on the phone (internet
needed once, about 240 MB installed), then tap **Choose a game file** and pick your
ROM. Prefer copying the file yourself? `Android/data/app.birdman64/files/rom/`
still works too. Later APKs install over it and keep your saves.

You need your own Pilotwings 64 (US) ROM.

## Quick start

1. Extract the zip and run `Birdman64.exe` from the extracted folder (Linux:
   make the AppImage executable and run it). Never run it from inside the zip.
2. If Windows shows "Windows protected your PC": click **More info**, then
   **Run anyway**.
3. Put your Pilotwings 64 (US) ROM next to the exe, or pick it when the game
   asks. Only the US version works.
4. The one-time setup downloads the game's open-source code and builds it on
   your PC (usually under a minute, internet needed once), then you are
   flying. Press Esc or F10 for settings.

The other files (debug symbols, checksums) are for bug reports and
verification.
