# Zadig (libwdi-ext edition) Changelog

## [1.0.0-ext]

### Added
- Full external USER driver support:
  - Display name from INI.
  - External driver path selection.
  - Recursive INF auto-locator.
  - Windows file dialog selection with status bar indication.

- Extended device filtering:
  - VID list
  - PID list
  - VID/PID pairs
  - Interface number (MI)
  - Current driver name

- Extended driver list visibility:
  - Toggle WinUSB, libusb-win32, libusbK, CDC, USER, and external USER.

- Installer environment configuration via INI:
  - `[behavior] cleanup_oem_inf = true/false`
  - `[behavior] no_syslog_wait = ...`
  - `[behavior] post_install_verify_timeout = ...`

### Fixed
- Removed dependency on `--with-userdir` to show USER driver
  when external INF is configured.

### Improved
- Status bar now shows active external INF.
- Better error messaging for missing external INF.
- Stable behavior on Windows 7, 10, 11.
