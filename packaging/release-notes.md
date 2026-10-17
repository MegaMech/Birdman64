## What's new in 1.4.0

**Android (experimental):** Birdman64 now runs on 64-bit Android phones (Android 8+) as a
sideloaded APK, with on-screen touch controls. It is early: tested on one phone so far,
please report problems.

### Added

- Android (arm64, experimental): a sideloadable APK with on-screen touch controls, which
  you can move or hide from the pause menu. Bring your own ROM; the first launch builds
  the game on the phone (needs internet once).
- Linux on 64-bit ARM (aarch64): the game now builds and runs from source.

### Fixed

- Very short button taps (shorter than one game frame) are no longer lost.
- Stray red dots under the altitude readout and slight edge smudges on the medal icons
  on the results screens are gone.

**Windows:** download `Birdman64-windows-x64.zip`. **Linux:** download the `.AppImage`.

**Android (experimental):** sideload `Birdman64-android-arm64.apk` (64-bit phones,
Android 8+), start it once, then copy your ROM into `Android/data/app.birdman64/files/rom/`
on the phone and start it again. The first launch builds the game on the phone (internet
needed once, about 240 MB installed). Later APKs install over it and keep your saves.

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
