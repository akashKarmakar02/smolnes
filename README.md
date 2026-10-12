# Smolnes for Twilight OS

Twilight framebuffer and keyboard port of [binji/smolnes](https://github.com/binji/smolnes).
Upstream history and the MIT license are preserved. The imported Twilight
sources come from `twilight_os` commit `3c5fdad`; emulator and pacing logic
are unchanged by extraction into this repository.

The SDL backend is replaced by `/dev/fb0` and `/dev/input/event0`. Frames use
accumulated absolute monotonic deadlines; `pacing.h` contains the pure timing
helpers. The Twilight branch does not use upstream's SDL submodule or desktop
CMake/CI configuration.

Build the static musl executable:

```sh
make CC=musl-gcc
```

Run the host pacing regression tests:

```sh
make test
```

Twilight OS checks out this repository at `userspace/apps/smolnes`; its normal
`make userspace` build stages `smolnes` into `rootfs/bin`. In the guest, run
`smolnes /path/to/game.nes` with a legally obtained ROM. Game data is not
included and must not be committed.

Commit and push port changes here before bumping Twilight OS's gitlink.
`smolnes-twilight.patch` is the original port patch retained for provenance;
the current C source and pacing tests are authoritative.
