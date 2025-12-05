# Android Emulators CI

This repository demonstrates how to boot a Cuttlefish Android emulator in GitHub Actions using the preinstalled Android SDK on ubuntu-latest runners.

## What is Cuttlefish?

Cuttlefish is Google's configurable virtual Android device that can run both remotely (using third-party cloud offerings) and locally (on Linux x86_64 and ARM64 machines). It's designed for testing and development of Android system images.

Learn more: [Cuttlefish Documentation](https://source.android.com/docs/devices/cuttlefish)

## Features

- **Automated Cuttlefish Build**: Builds the official Cuttlefish packages from source using a git submodule
- **Caching**: Caches both Cuttlefish packages and Android system images for faster subsequent runs
- **System Images**: Downloads the latest AOSP Cuttlefish system images from Android CI
- **Screenshot Artifact**: Captures and uploads a screenshot of the running emulator
- **Simplified Setup**: All code is inlined into the GitHub Action workflow

## GitHub Actions Runner Environment

This workflow takes advantage of the preinstalled Android SDK and tools on GitHub's ubuntu-latest runners. For details on what's available, see:

[Ubuntu 24.04 Runner Image Documentation](https://github.com/actions/runner-images/blob/main/images/ubuntu/Ubuntu2404-Readme.md)

## Running Locally

The workflow uses the `external/android-cuttlefish` submodule to build packages. To update or build locally:

```bash
# Update submodule to latest version
git submodule update --remote external/android-cuttlefish

# Checkout a specific version
cd external/android-cuttlefish
git checkout v1.31.0
cd ../..
git add external/android-cuttlefish
git commit -m "Update Cuttlefish to v1.31.0"
```

## Workflow Overview

The CI workflow (`.github/workflows/ci.yml`) performs these steps:

1. **Build Cuttlefish packages** from source (cached by version)
2. **Install Cuttlefish** and configure KVM/networking permissions
3. **Download Android system images** from ci.android.com (cached by build ID)
4. **Launch the emulator** using Cuttlefish with optimized CI settings
5. **Verify and screenshot** the running device
6. **Upload artifacts** for inspection

## Resources

- [Cuttlefish Documentation](https://source.android.com/docs/devices/cuttlefish)
- [GitHub Actions Runner Images](https://github.com/actions/runner-images/blob/main/images/ubuntu/Ubuntu2404-Readme.md)
- [Android Cuttlefish Repository](https://github.com/google/android-cuttlefish)
