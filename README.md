# myos-libc

C standard library and userspace runtime for MyOS.

## Purpose

`myos-libc` provides the native C userspace foundation for the MyOS operating system.

Its target is the public **`x86_64-myos`** platform. It will contain the C standard library, userspace runtime, public headers, syscall wrappers, and the Unix/POSIX-facing interfaces required by MyOS programs and third-party source ports.

## Architectural boundary

```text
applications / ports
        |
        v
    myos-libc
        |
        v
public x86_64-myos ABI
        |
        v
    MyOS kernel
```

The library must consume only documented public MyOS interfaces.

In particular:

- applications must not include kernel-private headers;
- libc must not depend on accidental kernel implementation details;
- MyOS owns its syscall ABI;
- Linux binary/syscall compatibility is not a design target;
- portable Unix/POSIX APIs are implemented as concrete consumers require them;
- missing functionality discovered by a port belongs in the appropriate reusable libc or operating-system layer rather than in application-specific workarounds.

## Scope

The project is expected to grow incrementally to provide:

- C runtime startup and process entry support;
- syscall invocation wrappers;
- `errno` and userspace error conventions;
- ISO C library headers and functions;
- memory, string, conversion and formatted-I/O facilities;
- file and directory interfaces;
- process and environment interfaces;
- time, signal and terminal interfaces;
- locale and multibyte support as required;
- mathematical functions and floating-point support;
- the public headers and libraries installed into the MyOS sysroot.

The exact API surface is intentionally demand-driven by MyOS userland and real third-party ports.

## Related projects

- [crecabar/myos](https://github.com/crecabar/myos) — kernel and platform.
- [crecabar/myos-userland](https://github.com/crecabar/myos-userland) — first-party userspace commands and tools.
- [crecabar/myos-vim](https://github.com/crecabar/myos-vim) — Vim port and a major libc/Unix API integration consumer.

## Status

Early bootstrap/planning stage. The public MyOS userspace ABI and libc surface are being developed incrementally alongside the operating system.

## License

`myos-libc` is licensed under the **GNU General Public License version 2 only (GPL-2.0-only)**.

See [LICENSE](LICENSE).
