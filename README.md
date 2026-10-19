# KernelSU Next v3.4.2 GKI AnyKernel3 builds

This is an independent build and release repository based on the
[WildKernels GKI build system](https://github.com/WildKernels/GKI_KernelSU_SUSFS).
Its dedicated workflow uses the official KernelSU Next **v3.4.2** tag at
`4c706b5938665866ebe16944a481a7b91e3396af` for the kernel integration.
It does not build or publish a root manager APK.

## Supported build targets

The eight Android/GKI families are `android12-5.10`, `android13-5.10`,
`android13-5.15`, `android14-5.15`, `android14-6.1`, `android15-6.6`,
`android16-6.12`, and `android17-6.18`. The eight configuration files currently
contain **211 Normal targets** across their monthly and LTS releases. These
are separate KMI-specific packages, not one ZIP that works on all devices.
Optional device variants and 16K page-size variants are not in this matrix.

## Build and release

1. In Actions, select **KernelSU Next v3.4.2 GKI AnyKernel3**, leave `scope=smoke`,
   and dispatch. The default sample is `android16-6.12`, `2026-09`.
2. Verify the published `ksun-next-v3.4.2-smoke-<run_id>` release and its ZIP,
   `SOURCE.json`, kernel `Image`, and `SHA256SUMS.txt`.
3. Dispatch the **same workflow at the same commit** with `scope=full` and set
   `smoke_run_id` to that successful smoke run. Full builds fail closed unless
   the smoke run and its published ZIP can be verified.

No scheduled builds run. The dedicated workflow requires every expected
AnyKernel3 artifact and BuildInfo, verifies ARM64 Image magic and provenance,
checks SHA-256 sums, then uploads a draft Release and publishes it only when
all assets have arrived. Build artifacts are retained for seven days to
allow the full matrix to complete. The older `Build Kernels` workflow is
inherited from WildKernels and is **not** the pinned v3.4.2 release path.

## Safety and provenance

SUSFS, NoMount, and other optional feature patches are disabled in the
dedicated workflow. A successful compile does not prove that a particular
device can boot a GKI image. Match the Android/GKI/KMI family and patch
level, back up your original boot image, and know your device recovery path
before considering a flash. A sample build does not validate the other 210
targets. Check each ZIP's `SOURCE.json` and the release's `SHA256SUMS.txt`.

The build machinery and configuration were adapted from
[WildKernels/GKI_KernelSU_SUSFS](https://github.com/WildKernels/GKI_KernelSU_SUSFS);
see [LICENSE](LICENSE) and [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).
The inherited `docs/` may describe options not enabled here.
