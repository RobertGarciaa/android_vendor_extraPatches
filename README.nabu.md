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

Settings keeps 0001 animation scale and 0002 nabu Stylus & keyboard entry.
The patch payloads are unchanged. Input details and hardware validation limits
are documented in vendor/xiaomi/dolby-nabu/input/PEN-STATUS.md.
