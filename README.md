# Pengu / AOSPA alioth build repository index

Device: Xiaomi Poco F3 (`alioth`, SM8250)
ROM: Pengu / AOSPA Android 17
Canonical snapshot branch for the alioth-adapted forks: **`calcite`**

The existing per-repository work branches are intentionally preserved.
Only the pa-sanji forks adapted for alioth are snapshotted on `calcite`.
The upstream AOSPA, aospa-pipa, Roynas, NXP and Pixel dependencies are not
forked here; they keep their current revisions.

- Base manifest: `Project-PenguinOS/manifest` (branch `celerity`)
- Product manifest: `vendor/aospa/products/alioth/beans.xml` (`calcite`)
- Local overlay: `.repo/local_manifests/gamebar.xml` (GameBar + Dolby, `calcite`)
- Agent findings: [pa-sanji/Agents.md](https://github.com/pa-sanji/Agents.md)

## Adapted pa-sanji forks (`calcite`)

| Path | Repository |
|---|---|
| `build/make` | `pa-sanji/build_make` |
| `build/release` | `pa-sanji/android_build_release` |
| `build/soong` | `pa-sanji/build_soong` |
| `device/qcom/common` | `pa-sanji/android_device_qcom_common` |
| `device/qcom/sepolicy` | `pa-sanji/device_qcom_sepolicy` |
| `device/qcom/sepolicy_vndr` | `pa-sanji/android_device_qcom_sepolicy_vndr` |
| `device/xiaomi/alioth` | `pa-sanji/device_xiaomi_aliothCLO` |
| `device/xiaomi/camera` | `pa-sanji/device_xiaomi_camera` |
| `frameworks/av` | `pa-sanji/frameworks_av` |
| `frameworks/base` | `pa-sanji/frameworks_basepengu` |
| `frameworks/native` | `pa-sanji/android_frameworks_nativepengu` |
| `hardware/interfaces` | `pa-sanji/hardware_interfaces` |
| `hardware/qcom/media` | `pa-sanji/android_hardware_qcom_media` |
| `hardware/qcom/display` | `pa-sanji/android_hardware_qcom_display` |
| `hardware/qcom/gps` | `pa-sanji/android_hardware_qcom_gps` |
| `hardware/samsung-ext/interfaces` | `pa-sanji/hardware_samsung-extra_interfaces` |
| `vendor/nxp/opensource/halimpl` | `pa-sanji/android_vendor_nxp_opensource_halimpl` |
| `vendor/nxp/opensource/hidlimpl` | `pa-sanji/android_vendor_nxp_opensource_hidlimpl` |
| `vendor/qcom/opensource/thermal-hal` | `pa-sanji/android_hardware_qcom_thermal` |
| `vendor/google/pixel` | `pa-sanji/android_vendor_google_pixel` |
| `hardware/xiaomi` | `pa-sanji/android_hardware_xiaomi` |
| `kernel/configs` | `pa-sanji/android_kernel_configs` |
| `kernel/msm-4.19` | `pa-sanji/xiaomi_sm8250_kernel_e404` |
| `packages/modules/Connectivity` | `pa-sanji/packages_modules_Connectivity` |
| `system/libhwbinder` | `pa-sanji/android_system_libhwbinder` |
| `vendor/aospa` | `pa-sanji/android_vendor_aospapengu` |
| `vendor/qcom/opensource/audio-hal/primary-hal` | `pa-sanji/android_hardware_qcom_audio` |
| `vendor/qcom/opensource/power` | `pa-sanji/vendor_qcom_opensource_power` |
| `vendor/qcom/opensource/usb` | `pa-sanji/android_vendor_qcom-opensource_usb` |
| `vendor/xiaomi` | `pa-sanji/proprietary_vendor_xiaomi` |
| `vendor/xiaomi/camera` | `pa-sanji/vendor_xiaomi_camera` |
| `packages/apps/GameBar` | `pa-sanji/packages_apps_GameBar` |
| `hardware/dolby` | `pa-sanji/android_hardware_dolby` |

## Base manifest

The remaining AOSP/AOSPA projects are provided by
`Project-PenguinOS/manifest` (`celerity`). Every alioth product dependency
listed above is now forked under `pa-sanji` and tracked on `calcite`.


## Build

```bash
# Base tree
repo init -u https://github.com/Project-PenguinOS/manifest -b celerity
repo sync -c -j"$(nproc --all)"

# Apply the alioth product manifest (from vendor/aospa/products/alioth/beans.xml)
# and the GameBar/Dolby overlay in .repo/local_manifests/gamebar.xml.
repo sync -c -j"$(nproc --all)"

source build/envsetup.sh
lunch aospa_alioth-user
./rom-build.sh alioth -i -t user
```

The RBE environment used for the release builds is the BuildBuddy setup from
the local build shell. The build command is:

```bash
./rom-build.sh alioth -i -t user
```

## Current status

Build 130 artifact:

```text
out/target/product/alioth/PenguinOS-celerity-20261109-gms-alioth.zip
sha256: 1343edf4e553a6ae154ab3f9f2332faa05d05ef9207cda8ff7f954e8da5c1216
```

See `Agents.md` for the full build 127–130 notes, the BT A2DP fix, the stock
HIDL 2.2 perf/104A work, cpusets, schedutil, and the open game-audio and
`init` SIGABRT items.
