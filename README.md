# 🚀🦀 Turbo Tauri

This project belongs to [Project Graph](https://github.com/LiRenTech/project-graph), a next-generation node diagram drawing tool. If you need some examples of Turbo Tauri, please check the `.github/workflows` directory of Project Graph.

GIVE ME A STAR

> [!IMPORTANT]
> This workflow is still in beta. Please report any issues you encounter to the [issue tracker](https://github.com/LiRenTech/turbo-tauri/issues).

> [!IMPORTANT]
> We'll never support iOS!

## Introduction

Turbo Tauri is a GitHub Actions workflow designed to automate the building and releasing of Tauri applications. This workflow supports multiple platforms including Linux, Windows, macOS, and Android, offering lots of customization options.

## Features

- ⚡ Remote Cache support for faster builds (Powered by [Turbo](https://turbo.build))
- 📔 Automatically creates GitHub releases
- 🔨 Builds the frontend interface
- 🦀 Builds and releases Tauri applications
- ⬆️ Generates updater JSON files **(Only supports Linux (for now))**
- 📦 Updates AUR package versions

## Usage

To use the Turbo Tauri workflow, add the following configuration to your GitHub repository:

```yaml
# .github/workflows/build.yml
name: Build
on:
  push:
    branches:
      - master
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: LiRenTech/turbo-tauri/.github/workflows/turbo-tauri.yml@master
        with:
          # Workflow parameters go here
        secrets:
          # Secrets go here
```

## Workflow Parameters

| Parameter             | Description                                            | Required | Default                 |
| --------------------- | ------------------------------------------------------ | -------- | ----------------------- |
| `app_root`            | The root directory of the application.                 | Yes      | `.`                     |
| `app_version`         | The version of the application.                        | Yes      | `"0.0.0"`               |
| `app_version_android` | The application version for Android, CANNOT be `0.0.0` | No       | `"0.0.1"`               |
| `release_name`        | The name of the release.                               | Yes      | `"Release"`             |
| `release_notes`       | The release notes.                                     | No       | `""`                    |
| `release_tag`         | The tag used for the release.                          | Yes      | `"v0.0.0"`              |
| `prerelease`          | Whether to mark the release as a prerelease.           | No       | `false`                 |
| `delete_release`      | Whether to delete the release.                         | No       | `true`                  |
| `turbo_team`          | The team used for Turbo.                               | Yes      | N/A                     |
| `android_key_path`    | The path to the Android key file, relative to app_root | No       | `"upload.jks"`          |
| `aur_package_name`    | The name of the AUR package.                           | No       | `""`                    |
| `aur_key_algorithm`   | The algorithm used for the AUR key.                    | No       | `"ed25519"`             |
| `task_build`          | The task to run for building the app.                  | No       | `"tauri:build"`         |
| `task_build_android`  | The task to run for building the app for Android.      | No       | `"tauri:build:android"` |

## Secrets

| Secret                               | Description                                                                                | Required | Default |
| ------------------------------------ | ------------------------------------------------------------------------------------------ | -------- | ------- |
| `GITHUB_TOKEN`                       | GitHub token used to create releases.                                                      | Yes      | N/A     |
| `TURBO_TOKEN`                        | Token used to enable Turbo remote caching.                                                 | No       | N/A     |
| `TAURI_SIGNING_PRIVATE_KEY`          | Private key used to sign application binaries for updater support.                         | No       | N/A     |
| `TAURI_SIGNING_PRIVATE_KEY_PASSWORD` | Password for the signing key.                                                              | No       | N/A     |
| `ANDROID_KEYSTORE`                   | Base64 of `jks` file for APK signing.                                                      | No       | N/A     |
| `ANDROID_KEYSTORE_PASSWORD`          | Password for the keystore.                                                                 | No       | N/A     |
| `ANDROID_KEY_ALIAS`                  | Alias for the key.                                                                         | No       | N/A     |
| `BUILD_ENV`                          | Environment variables to pass to `tauri build`. Format: `key1=value1\\nkey2=value2\\n...`. | No       | N/A     |
| `AUR_SSH_PRIVATE_KEY`                | SSH private key for AUR publishing.                                                        | No       | N/A     |

## Workflow Steps

1. **Create Release**: Automatically creates a GitHub release.
2. **Build Frontend**: Builds the frontend interface using pnpm and Node.js.
3. **Publish Tauri**: Builds and releases Tauri applications for various platforms.
4. **Generate Updater JSON**: Generates a JSON file containing version information and release notes.
5. **Bump AUR Version**: Updates the version information of the AUR package.

## Notes

- Ensure your GitHub repository contains the source code and configuration files for your Tauri application.
- Adjust the parameters and steps in the workflow according to your application's requirements.

## Contribution

If you have any suggestions or feature requests, please submit an Issue or Pull Request.
