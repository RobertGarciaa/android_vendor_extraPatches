# nabu patches for PixelOS seventeen

vendorsetup.sh is identical to the seventeen branch. Sourcing build/envsetup.sh
runs git am once per project with that project's patches in filename order.
A failed batch is aborted using the existing seventeen behavior. There is no
additional history scanner, Python application helper or application cache.

frameworks_base order:
1. CameraDeviceImpl input configuration fix
2. Default animation scale
3. Zero auto-brightness adjustment
4. ImageReader native detach handling
5. Stock nabu keyboard/stylus policy
6. Native stylus long presses
7. Pen charging notifications

Settings order:
1. Default animation scale
2. Stock nabu Stylus & keyboard entry and availability controller
3. The same entry in Expressive and Expressive desktop layouts

The patch payloads are unchanged. Input details and hardware validation limits
are documented in vendor/xiaomi/dolby-nabu/input/PEN-STATUS.md.


## Review — 2026-11-01

All 14 patches were replayed using the existing per-project `git am` command
in isolated temporary repositories. The resulting touched files matched the
current PixelOS source byte for byte:

| Project | Reference base | Patches |
| --- | --- | ---: |
| build/soong | 321ecf4fc740 | 3 |
| frameworks/base | 044b965aa2d3 | 7 |
| packages/apps/Aperture | e4fc8292dd10 | 1 |
| packages/apps/Settings | 9c2cdaad6450 | 3 |

The three Settings layouts each have exactly one nabu entry with the correct
controller and stock activity target. NabuInputPolicy and NabuPenStatusMonitor
match the canonical copies in vendor/xiaomi/dolby-nabu/input/framework/src.
The availability controller gates the menu on ro.nabu.input_port and an
installed target activity. Framework input handling is also product gated.

vendorsetup.sh remains byte-identical to seventeen; its syntax check passed.
No history scanning, extra patch application helper, or new framework/Settings
commit was added. This source/application review does not replace testing the
recent input APK crash fix on a newly built image.
