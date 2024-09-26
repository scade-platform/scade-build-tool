# SCADE Toolchain

The SCADE Toolchain is a comprehensive set of tools for building Swift code for both Apple and Android mobile platforms. The toolchain includes the following components:

- `scd`, the SCADE Build Tool, which supports building cross-platform packages from Swift code for both Apple and Android mobile platforms.

- A port of the Swift toolchain for the Android platform. This toolchain supports all Android architectures, including 32-bit ones, and includes a complete port of the Swift Standard Library and Foundation library to the Android platform. Learn more about the Swift Toolchain for Android here: https://www.swift-android.com/

- An improved version of Swift Package Manager with support for cross-platform XCFrameworks for both Apple and Android platforms. These frameworks can be used in SPM projects via the .binaryTarget command in the project manifest.


## Installation

The SCADE Toolchain can be installed via the Homebrew package manager using the following command:
```
brew install scade-platform/toolchain/scd
```

## Supported platforms
The `scd` build tool supports the following platforms:
- macos
- iphoneos
- iphonesimulator
- android-arm64-v8a
- android-x86_64
- android-armeabi-v7a
- android-x86

## Usage

### Building an SPM project for Android platform
To build an SPM project for the Android platform, run the `scd build` command from the root of the SPM project and pass one of the Android platforms to build for:

```
scd build --platform android-arm64-v8a
```

This command will automatically install the Swift toolchain for Android and build the SPM project for the desired Android platform.


### Archiving an SPM project for Android
The `scd` build tool can build an SPM project for multiple Android platforms and archive it into a single directory suitable for embedding into Android projects. To create an archive, run the `scd archive` command with the set of Android platforms you want to build:
```
scd archive --platform android-arm64-v8a \
            --platform android-x86_64 \
            --platform android-armeabi-v7a \
            --platform android-x86
```

The resulting archive directory will be placed into the `lib` subdirectory of the current working directory. You can change the output directory using the -o argument.

### Archiving an SPM project into .aar library
The `scd` build tool can also archive an SPM project into an Android .aar library.

Archiving into an .aar library requires a valid `AndroidManifest.xml` located inside the SPM project root. The manifest should contain at least the package ID and version information:
```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    package="com.example.scadeexample"
    android:versionCode="1"
    android:versionName="1.0">
</manifest>
```

To create an .aar archive, pass the additional `--type android-aar` argument to the `scd archive` command:
```
scd archive --type android-aar
            --platform android-arm64-v8a \
            --platform android-x86_64
```
