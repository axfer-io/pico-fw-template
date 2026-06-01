# Pico C/C++ Firmware Template

Embedded systems · Control · Debugging ⚙️  
I/O 🔌, firmware 🔧, and systems that actually run 🚀

---

## Overview

This repository provides a **clean, reproducible template** for embedded firmware projects using the Raspberry Pi Pico SDK.

It is designed for:
- low-level C/C++ development
- deterministic builds
- on-target debugging
- minimal magic

---

## Requirements

- Raspberry Pi Pico SDK (`PICO_SDK_PATH` exported)
- CMake ≥ 3.13
- Ninja
- ARM GCC toolchain
- `pico-tools` installed at `~/pico/tools` (for flashing & OpenOCD)


## Supported Targets

- RP2040 (Pico / Pico W)
- RP2350 (Pico 2 / Pico 2 W)

---

## Features

- Out-of-tree builds per preset
- CMake presets (Debug / Release × all boards)
- OpenOCD flash target
- SWD debugging ready
- Firmware name derived from project directory automatically
- Modular structure: `src/` as OBJECT library, `lib/` for drivers and utilities

---

## Project Structure

```text
.
├── src/            # Application code (compiled as app_src OBJECT library)
├── lib/
│   ├── drivers/    # Hardware drivers
│   └── utils/      # Utility functions
├── build/          # Generated build directories (git-ignored)
├── CMakeLists.txt
├── CMakePresets.json
└── README.md
```

### Adding source files

Add `.c` files to `src/CMakeLists.txt` only — the root never needs to change:

```cmake
add_library(app_src OBJECT
    main.c
    uart.c
)
```

---

## Using this template

Copy or clone the repo and rename the folder to your project name — the binary will be named after the folder automatically.

```bash
cp -r pico-fw-template my-project
cd my-project
```

---

## Build Flow

Presets define the board and build type.  
You configure once, then live in `cmake --build`.

### First-time configure
```bash
cmake --preset pico2w-debug
```

### Incremental build
```bash
cmake --build --preset build-pico2w-debug
```

### Build + flash
```bash
cmake --build --preset flash-pico2w-debug
```

---

## Debugging

1. Start OpenOCD
2. Attach GDB / DAP
3. Set breakpoints and inspect registers / memory

OpenOCD is expected to run on port `:3333` (SWD).

Designed to work cleanly with:
- gdb-multiarch
- Neovim + nvim-dap

---

## Design Principles

- Explicit control over convenience
- Debug-first mindset
- Hardware-driven design
- Minimal abstractions

---

## Author

**axfer-io**  
Embedded systems · Control · Debugging  
Firmware and systems that actually run.

---

## License

MIT