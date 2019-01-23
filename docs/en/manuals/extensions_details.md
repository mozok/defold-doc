
# The Defold build setup

Here we list some relevant build information, in order to make the integrations with your extensions as easy as possible.

Here are some things to consider when you create an extension for the Defold engine.
For more general guidelines on how to develop cross platform native code, and also extension/Lua apis, please refer to [Native Extensions - Best Practices](/manuals/extensions_best_practices)

# C++ version

In the engine itself we use no C++ version higher than C++98. While you may use a higher version to build your extension, bear in mind that a higher version might come with ABI changes. This might make it impossible to use your extension in conjunction with other extensions in the engine or on the asset store.

When creating libraries (such as extensions), it's good to keep the lowest common denominator as a target.

# Toolchain

Clang - macOS, iOS, Win32
GCC - Android, Linux

*We're plan make both Android and Linux to use Clang as well*

## SDK Versions

* Android: NDK 10e, Build Tools 23.0.2, Api Level 14
* iOS: iPhoneOS11.2.sdk
* MacOS: MacOSX10.13.sdk
* Windows: WindowsKits 8.1 + 10.0, Microsoft Visual Studio 14.0
* Linux: Ubuntu 16.04, gcc 5.4.0, libssl-dev, uuid-dev, libxi-dev, libopenal-dev, libgl1-mesa-dev, libglw1-mesa-dev, freeglut3-dev
* Html5: Emscripten 1.38.0,

## C++ version + ABI compatibility

* Linux: `GCC 5.4.0`
* Android:`GCC 4.8`
* Html5: `Emscripten 1.35.0`
* Win32: `Microsoft Visual Studio 14.0` alt `clang-6.0`
* iOS/MacOS: `apple-clang` alt `clang-6.0`

For iOS/MacOS, we use `-miphoneos-version-min=6.0` and `-mmacosx-version-min=10.7` respectively.

We don't specify a specific C++ version, so we use the default of each compiler.

# Win32 + Clang

A recent addition is to be able to build the Windows builds using clang.
This allows for faster builds on our servers, and also allows us to streamline our builds.

# Static linkage

The custom engine is built using static linkage.
The main reason is that on iOS version < 8, multiple executable binaries in an .ipa aren't allowed in the app store.

# No C++ Exceptions

We don't make use of any exceptions in the engine.
It isn't generally used in game engines, since the data is (mostly) known beforehand, during development.
Removing the support for C++ exceptions decreases executable size and improves the runtime performance.

# Defold SDK

With each (biweekly) release of Defold, we release a new Defold SDK.
With it, we ship the libraries of the engine, and also a build manifest file,
which is identical in structure and syntax as the [extension](/manuals/extensions_build_variants) and [app](/manuals/extensions_build_variants) manifests.

(This sdk is not yet public)
