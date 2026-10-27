# firmware-samsung-p3s

Proprietary firmware for the **Samsung Galaxy S21 Ultra 5G (Exynos, SM-G998B, codename `p3s`)**,
used by the postmarketOS port (`device-samsung-p3s` / `firmware-samsung-p3s` in pmaports).

These files are copied unmodified from the stock **vendor** logical partition (inside `super`)
of an SM-G998B running One UI with the December 2024 security patch. They are Samsung/Broadcom
property and are provided here only so the postmarketOS port can be installed without each user
extracting them by hand.

## Contents

| Path | What | Used by |
|---|---|---|
| `vendor/firmware/wifi/bcmdhd_sta.bin_c0`, `_c1` | BCM4389 Wi-Fi firmware (station mode), per chip revision. `_c1` is 20.80.87.3 | `dhd_bcm4389` |
| `vendor/firmware/wifi/bcmdhd_clm.blob` | Regulatory (CLM) data | `dhd_bcm4389` |
| `vendor/firmware/wifi/nvram.txt*` | Board calibration, per module vendor/revision (semco / 1wk) | `dhd_bcm4389` |
| `vendor/firmware/wifi/bcmdhd_mfg.bin*`, `bcmdhd_mon.bin*` | Factory-test and monitor-mode firmware | not used |
| `vendor/firmware/bcm4389*.hcd` | Bluetooth patch RAM, per revision and module vendor | Bluetooth (not working yet) |

The driver (`bcmdhd_101_18`, built with `DHD_LINUX_STD_FW_API`) requests these by name from
`/lib/firmware` and picks the `_c0`/`_c1` and nvram variant from the chip's OTP data, so the
postmarketOS package installs them flat into `/lib/firmware`.

## Extracting them yourself

On a phone running the postmarketOS port, `p3s-wifi-probe.sh` / `p3s-lp-find.sh` from the port
work folder map `vendor` out of `super` read-only with device-mapper and copy `firmware/wifi/`.
