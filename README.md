# libwdi-ext — Extended libwdi fork

**libwdi-ext** is an enhanced, production-focused fork of  
[pbatard/libwdi](https://github.com/pbatard/libwdi) with additional features
designed for embedded applications, automated driver deployment, and large-scale
device provisioning.

This fork remains fully compatible with the original libwdi API, while adding
optional advanced behavior useful for OEMs, integrators, and system tools.

---

## Key Extensions

### ✔ External INF driver installation (WDI_USER external mode)
Allows installing any vendor-supplied driver (FTDI, ST, custom USB class, etc.)
without bundling proprietary drivers into your application.

### ✔ OEM INF cleanup (no more driver-store pollution)
Eliminates Windows creating many duplicate `oemXX.inf` entries over time.
Triggered via:

```c
SetEnvironmentVariableA("WDI_CLEANUP_OEM_INF", "1");
````

### ✔ Fast driver installation on Windows 10/11

Added install options:

```c
id_options.no_syslog_wait = 1;             // disables slow eventlog tailing
id_options.post_install_verify_timeout = N; // short predictable re-enumeration timeout
```

Prevents the typical 30–60s delays after switching drivers.

### ✔ Device filtering (VID/PID, VID/PID pairs, interface number, driver name)

The Zadig example is extended with highly precise device visibility filtering:

* `[device] vid = …`
* `[device] pid = …`
* `[device] vid_pid = …`
* `[device] mi = …`
* `[device] driver = …`

### ✔ Driver visibility controls

Zadig can hide/show drivers like:

* WinUSB
* libusb-win32
* libusbK
* CDC
* USER
* External USER driver

### ✔ External driver selection UI (Zadig)

Includes:

* Recursive INF search under configured path
* File-open dialog to pick INF
* Status-bar indication of selected INF
* Recommendation to store external INF path in ini

### ✔ Full documentation for embedding

See:

➡ **[docs/EMBEDDING_LIBWDI_EXTERNAL_INF.md](docs/EMBEDDING_LIBWDI_EXTERNAL_INF.md)**
Complete examples for WinUSB, libusb, CDC, USER(builtin), USER(external).

---

## Compatibility

* Fully API compatible with original **libwdi ≥ 1.4**
* Works on:

  * Windows 7
  * Windows 8
  * Windows 10
  * Windows 11 (including IoT Enterprise S)
* Tested with FTDI FT2232H, custom WCID devices, CDC, libusb stacks.

---

## Building

Same as upstream:

```
./configure --with-wdf <...> [--with-userdir PATH]
make
```

`--with-userdir` is optional; external INF mode does not require it.

---

## Licensing

The fork retains the **GPLv3** license from the upstream repository.
Redistribution of third-party drivers (e.g. FTDI, ST, Prolific, etc.)
must follow their licensing terms — therefore `libwdi-ext` provides
a legal-compliant **external INF mode** instead of bundling them.

---

## Upstream Project

This fork is based on the excellent work by:

➡ [https://github.com/pbatard/libwdi](https://github.com/pbatard/libwdi)

All foundational documentation, WCID notes, and driver stack guidance remain valid.

---

## Changelog

See:

* **CHANGELOG.md** — libwdi core changes
* **CHANGELOG_ZADIG.md** — Zadig example changes

---

## Status

`libwdi-ext` is actively maintained and continuously tested on multi-interface
USB devices under Windows 7, 10, 11.

PRs are welcome.
