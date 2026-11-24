# PhoneRemote IR investigation / cloud build

This repository scaffold uses GitHub Actions so the APK can be inspected and Android projects can be built in the cloud without a PC.

## Important status

The supplied `PhoneRemote.apk` is a compiled APK, not an Android Studio source project. This workflow first decodes it and produces a report/source artifact for inspection. It does **not** claim to convert Wi-Fi commands into IR or produce a modified IR-only APK automatically. The original Power IR code and the TV's other IR command codes must be identified before a safe functional modification can be made.

## Setup from an Android phone

1. Create a new **private** GitHub repository.
2. Upload this scaffold's files, keeping the `.github/workflows` folder structure.
3. Upload your original APK to `input/PhoneRemote.apk` (do not replace or delete your original copy).
4. Open the repository's **Actions** tab.
5. Select **Inspect PhoneRemote APK**, then **Run workflow**.
6. When it finishes, download the `phonremote-inspection` artifact. It contains APKTool's decoded resources/manifest and JADX Java output.

## What the workflow does

- Uses a pinned APKTool release and JADX release in the GitHub runner.
- Decodes the APK and decompiles DEX for review.
- Searches decoded output for ConsumerIrManager, transmit calls, IR patterns, and network-related code.
- Uploads the inspection output as a GitHub Actions artifact.

## Safety / signing

Do not install a rebuilt APK unless it is signed and you trust the source. Rebuilding a third-party APK may break its signature, licensing, or security assumptions. Keep the original APK backed up. This workflow does not sign or publish an installable APK.
