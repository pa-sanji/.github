# Pengu / AOSPA — alioth

Build repository index and release notes for the Xiaomi Poco F3 (`alioth`).

- Device tree: [device_xiaomi_aliothCLO](https://github.com/pa-sanji/device_xiaomi_aliothCLO)
- Kernel: [xiaomi_sm8250_kernel_e404](https://github.com/pa-sanji/xiaomi_sm8250_kernel_e404)
- Vendor blobs: [proprietary_vendor_xiaomi](https://github.com/pa-sanji/proprietary_vendor_xiaomi)
- AOSPA vendor: [android_vendor_aospapengu](https://github.com/pa-sanji/android_vendor_aospapengu)
- Build index / full repo list: [.github](https://github.com/pa-sanji/.github)
- Agent findings and safety notes: [Agents.md](https://github.com/pa-sanji/Agents.md)

Canonical snapshot branch for the adapted forks: **`calcite`**.

## Sync alioth

```bash
mkdir -p ~/pengu-alioth && cd ~/pengu-alioth
repo init -u https://github.com/Project-PenguinOS/manifest -b celerity --git-lfs
mkdir -p .repo/local_manifests
curl -fsSL \
  https://raw.githubusercontent.com/pa-sanji/.github/calcite/manifests/alioth-local.xml \
  -o .repo/local_manifests/alioth-local.xml
repo sync -c --no-tags -j"$(nproc --all)"
```

Then:

```bash
source build/envsetup.sh
lunch aospa_alioth-user
./rom-build.sh alioth -i -t user
```

See [.github](https://github.com/pa-sanji/.github) for the full repo index and
[Agents.md](https://github.com/pa-sanji/Agents.md) for findings and open issues.
