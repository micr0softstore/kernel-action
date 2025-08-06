<div align="start">
  <h1>Kernel build action</h1>
  <h3><i>Powered by GitHub Actions</i></h3>
</div>

A workflow to automatically build an Android (non-GKI) kernel

## Usage Guide

> [!NOTE]
> You will need a GitHub account.

## Options Guide

> [!NOTE]
> All options are located in [config.env](config.env)

| Base section options | Optional | Description | Example value |
|---------------------|----------|-------------|----------------|
| KERNEL_SOURCE | <div align="center">❌</div> | Link to kernel repository | `https://github.com/Jbub5/android_kernel_xiaomi_mt6768` |
| KERNEL_SOURCE_BRANCH | <div align="center">❌</div> | Branch name of kernel repository | <div align="center">`kernel-tree`</div> |
| KERNEL_CONFIG | <div align="center">❌</div> | Kernel config file name | <div align="center">`lancelot_defconfig`</div> |
| KERNEL_ARCH | <div align="center">❌</div> | The Linux kernel architecture | <div align="center">`arm64`</div> |
| KERNEL_IMAGE_NAME | <div align="center">❌</div> | Format of the kernel image for flashable AnyKernel3 zip | <div align="center">`Image.gz-dtb`</div> |

<br>

| KernelSU section options | Optional | Description | Example value |
|--------------------------|----------|-------------|---------------|
| ENABLE_KERNELSU | <div align="center">✅</div> | Enables accounting for the KernelSU options written below | <div align="center">`true`</div> |
| KERNELSU_SETUP_SOURCE | <div align="center">❌</div> | Link to KernelSU setup script | `https://raw.githubusercontent.com/tiann/KernelSU/main/kernel/setup.sh` |
| KERNELSU_TAG | <div align="center">✅</div> | Repository branch or tag of KernelSU | <div align="center">`v1.0.1`</div> |
| KSU_REVERT | <div align="center">✅</div> | Revert the [commit](https://github.com/tiann/KernelSU/commit/898e9d4f8ca9b2f46b0c6b36b80a872b5b88d899) that removed non-GKI kernel support | <div align="center">`true`</div> |
<!-- | KSU_EXPECTED_SIZE | idk | idk | idk | -->
<!-- | KSU_EXPECTED_HASH | idk | idk | idk | -->
> [!IMPORTANT]
> [KernelSU](https://kernelsu.org/guide/what-is-kernelsu.html) [no longer supports non-GKI kernels](https://github.com/tiann/KernelSU/issues/1705) after version [v1.0.0](https://github.com/tiann/KernelSU/releases/tag/v1.0.0). The last supported version is [v0.9.5](https://github.com/tiann/KernelSU/releases/tag/v0.9.5), please make sure to use the correct tag.

<br>

| Compiler section options | Optional | Description | Example value |
|--------------------------|----------|-------------|---------------|
| USE_CLANG | <div align="center">✅</div> | Enable Clang toolchain usage and accounting for options written below | <div align="center">`true`</div> |
| CLANG_SOURCE | <div align="center">❌</div> | Link to clang archive or repository | `https://github.com/ZyCromerZ/Clang/releases/download/21.0.0git-20250415-release/Clang-21.0.0git-20250415.tar.gz` |
| CLANG_BRANCH | <div align="center">✅</div> | Branch name of clang repository | <div align="center">`main`</div> |
| USE_GCC | <div align="center">✅</div> | Enable GCC toolchain usage and accounting for options written below | <div align="center">`false`</div> |
| USE_GCC_64 | <div align="center">✅</div> | Enable GCC 64-bit | <div align="center">`true`</div> |
| GCC_64_SOURCE | <div align="center">❌</div> | Link to GCC 64-bit archive or repository | `https://snapshots.linaro.org/gnu-toolchain/14.0-2023.06-1/aarch64-linux-gnu/gcc-linaro-14.0.0-2023.06-x86_64_aarch64-linux-gnu.tar.xz` |
| GCC_64_BRANCH | <div align="center">✅</div> | Branch name of GCC 64-bit repository | <div align="center">`main`</div> |
| USE_GCC_32 | <div align="center">✅</div> | Enable GCC 32-bit | <div align="center">`true`</div> |
| GCC_32_SOURCE | <div align="center">❌</div> | Link to GCC 32-bit archive or repository | `https://snapshots.linaro.org/gnu-toolchain/14.0-2023.06-1/arm-linux-gnueabihf/gcc-linaro-14.0.0-2023.06-x86_64_arm-linux-gnueabihf.tar.xz` |
| GCC_32_BRANCH | <div align="center">✅</div> | Branch name of GCC 32-bit repository | <div align="center">`main`</div> |
> [!IMPORTANT]
> You can use only Clang or GCC, but not both at the same time.

<br>

| Anykernel3 section options | Optional | Description | Example value |
|----------------------------|----------|-------------|---------------|
| USE_ANYKERNEL3 | <div align="center">✅</div> | Enable creating flashable AnyKernel3 zip and accounting for options written below | <div align="center">`true`</div> |
| ANYKERNEL3_SOURCE | <div align="center">❌</div> | Link to AnyKernel3 source | `https://github.com/Jbub5/AnyKernel3.git` |
| ANYKERNEL3_BRANCH | <div align="center">✅</div> | Branch name of AnyKernel3 repository | <div align="center">`proton`</div> |

<br>

| Build section options | Optional | Description | Example value |
|-----------------------|----------|-------------|---------------|
| EXTRA_CMDS | <div align="center">✅</div> | Additional compiler options | `LLVM=1 LLVM_IAS=1 LD=ld.lld AS=llvm-as AR=llvm-ar NM=llvm-nm OBJCOPY=llvm-objcopy OBJDUMP=llvm-objdump READELF=llvm-readelf STRIP=llvm-strip CROSS_COMPILE=aarch64-linux-gnu- CROSS_COMPILE_ARM32=arm-linux-gnueabi- CROSS_COMPILE_COMPAT=arm-linux-gnueabi- CONFIG_NO_ERROR_ON_MISMATCH=y TARGET_BUILD_VARIANT=user` |
| ENABLE_PYTHON2 | <div align="center">✅</div> | Many old kernels require python2 to build them | <div align="center">`false`</div> |
| ENABLE_CCACHE | <div align="center">✅</div> | Enable [ccache](https://ccache.dev) | <div align="center">`false`</div> |
| REMOVE_UNUSED_PACKAGES| <div align="center">✅</div> | Remove unnecessary packages and free up more disk space for builder | <div align="center">`false`</div> |
| NEED_DTBO | <div align="center">✅</div> | Upload DTBO | <div align="center">`false`</div> |
| BUILD_BOOT_IMG | <div align="center">✅</div> | Repack boot.img by replacing the kernel in it with the compiled kernel | <div align="center">`false`</div> |
| SOURCE_BOOT_IMAGE | <div align="center">✅</div> | Link to the original boot.img for repackage it | `https://raw.githubusercontent.com/xiaoleGun/KernelSU_action/main/boot/boot.img` |

## Credits

- [xiaoleGun](https://github.com/xiaoleGun) for base
- [dabao1955](https://github.com/dabao1955) for format of README.md
