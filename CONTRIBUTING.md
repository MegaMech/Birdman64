# Contributing to Birdman64

Thanks for your interest! Contributions and forks are welcome.

## Build and test

Prerequisites are the same as in the
[README "Building from source"](README.md#building-from-source) section:
Rust stable, the project's C compiler (zig 0.16.0, fetched by the command
below; no LLVM install needed), on Linux also `libasound2-dev`,
`libudev-dev`, `libdbus-1-dev` and `pkg-config`, and a recursive clone (the
decompilation is a submodule).

```sh
git clone --recursive https://github.com/USER/Birdman64
cd Birdman64
cargo run -p pw64-cbuild --example get_zig --features fetch   # once
cargo run --release -p birdman64        # run the game
cargo test --workspace             # run the tests
cargo clippy --workspace --all-targets -- -D warnings   # must be clean
```

The decompiled C compiles on first build (with zig, the same compiler the
release uses on players' machines); you need your own US ROM to actually
play, never committed.

## Changing the game's C code (patches)

The decompiled game lives in the read-only `decomp/` submodule; never edit it.
Our changes to it are **patches**, applied at build time (and, in the release,
on the player's machine after the decomp is downloaded):

- `crates/pw64-game/patches/<path under decomp>.patch`, one per decomp file,
  for `src/**.c` and `include/**.h` (e.g. `patches/src/app/hud.c.patch`).
- New code that doesn't have to live inside a decomp file goes in
  `crates/pw64-game/native/` instead (e.g. `native/src/pw64_plane.c`, declared
  in `native/pw64_native.h`). Keep patch hunks small: a hook call into native
  code, not a whole feature. Keep new state in native code as well: adding a
  field to a decomp struct means patching its header and shifting every
  user of the struct.
- Mark changes with a `PW64:` comment saying why.

**To change a decomp file:**

1. Copy the original (e.g. `decomp/src/app/hud.c`) to two scratch
   directories as `a/src/app/hud.c` and `b/src/app/hud.c`, with LF line
   endings (the checkout may be CRLF).
2. Edit the `b/` copy.
3. From the directory holding `a/` and `b/`, run
   `git -c core.autocrlf=false diff --no-index --no-prefix a/src/app/hud.c b/src/app/hud.c`
   and drop the `diff` and `index` lines, so the header reads
   `--- a/src/app/hud.c` / `+++ b/src/app/hud.c`.
4. Merge the new hunks into the existing patch file, or save it as a new
   `.patch` under the path above. Hunks must apply in order against the
   **pristine** file, not against another patch's output.
5. `cargo build -p pw64-game` applies every patch; a hunk that doesn't apply
   is reported with its file name.

Notes:

- Don't use GNU `patch` or `git apply` to test: our applier is strict (no
  fuzz, line endings ignored) and is the only one that counts. GNU `patch`
  rejects some of our patches.
- `cargo test --workspace` also checks every patch against the first-run
  builder's patch format (`pw64-cbuild`, `ops_vs_patches`), so a patch that
  builds locally but breaks the release build is caught in CI.
- The release builds the game from the downloaded decomp, so CI has a
  "First-run game build" job: if only that job and the build jobs fail, a
  patch or native file doesn't compile.
- Patches only exist for the native build, so no `#ifdef` guard is needed.
- Native code must also build on Windows, Linux, macOS, iOS and Android; CI
  covers all of them.

## Legal rules (non-negotiable)

- Never commit, upload, or attach **ROM data or extracted game assets** to a
  pull request or an issue: that includes ROM images, textures, audio,
  models, and in-game text. For rendering bugs, a small cropped screenshot of
  the glitch is fine; no full-screen captures, videos or asset dumps.
- Code may be derived from the MIT-licensed
  [Pilotwings64Decomp](https://github.com/gcsmith/Pilotwings64Decomp).
- Never copy code from [Pilotwings64Recomp](https://github.com/gcsmith/Pilotwings64Recomp):
  it is GPL-3.0 and incompatible with this project's MIT code. Reading it for
  reference is fine; copying is not.

## Pull requests

- One topic per PR.
- `cargo test --workspace` passes and `cargo clippy --workspace --all-targets`
  is clean.
- Keep changes consistent with the surrounding code style, and comment the
  *why* (name the decomp function a port mirrors).

## Bug reports

Open an issue with:

- `crash.log` if the game crashed (it lives next to your saves),
- your GPU model and driver version, your OS,
- the SHA-1 of your ROM (on Windows: `certutil -hashfile rom.z64 SHA1`).

**Never attach the ROM itself.** We do not need it, and we cannot distribute
it.

## Conduct and security

Contributions follow the
[Contributor Covenant code of conduct](CODE_OF_CONDUCT.md); security issues
are reported privately per [SECURITY.md](SECURITY.md), never in a public
issue.
