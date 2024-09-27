# Scade Build Tool

This repository contains binary packages for `scd`, the SCADE Build Tool, a tool for building cross-platform packages from Swift code for both Apple and Android platforms.

## Installation

### Installation via Brew

The easiest way to install `scd` is via the Homebrew package manager. To install `scd` via Brew, run the following command:
```
brew install scade-platform/toolchain/scd
```

### Standalone package

The `scd` tool can also be installed as a standalone package. 

You can download latest standalone package here:\
https://github.com/scade-platform/scade-build-tool/releases/latest

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
