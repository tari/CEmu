Two different types of web build are supported: a pure library to be integrated
into a separately-provided web page, and a simple standalone page using the SDL
GUI.

In both cases, use `core/emscripten.mk` to compile the core.

## As a library

    make -C core -f emscripten.mk WebCEmu.js

This will build an Emscripten javascript module providing the [Module
API](https://emscripten.org/docs/api_reference/module.html). To interact with
the emulator in an instance of the module, call the functions exported by
`core/os/main-emscripten.c` via the `ccall` method of the module.

## Standalone

    make -C core -f emscripten.mk libcemucore.a
    emmake make -C gui/sdl appname=cemu.html \
        CC=emcc CCFLAGS="-std=c99 -O2 -Wall -Wextra --use-port=sdl2"

This generates `gui/sdl/cemu.html` and some extra library files (javascript +
wasm). Opening the HTML file in a browser should run the emulator.
