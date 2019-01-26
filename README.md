# Kotlin Native Xcode Support

Plugin to facilitate debugging iOS applications using Kotlin Native in Xcode.
Defines Kotlin files as source code, with basic highlighting. Allows you to
set breakpoints and includes llvm support to view data in the debug window.

## Installation

### Setup script

Run the following command in your terminal:

```
./setup.sh
```

### Manual installation

Please note that if you are running Xcode 8 the `Plug-ins` and `Specifications` directories might not exist.

- Copy the `Kotlin.ideplugin` directory to `~/Library/Developer/Xcode/Plug-ins/`:

	```
	cp -r Kotlin.ideplugin ~/Library/Developer/Xcode/Plug-ins/
	```
- Copy the `Kotlin.xclangspec` file to `~/Library/Developer/Xcode/Specifications`:

	```
	cp Kotlin.xclangspec ~/Library/Developer/Xcode/Specifications/
	```

lldb formatting support is provided by kotlin_lldb.py. The setup script will add
the path to `~/.lldbinit`. You can manually load this script at the lldb prompt
with

```
command script import ~/Library/Developer/Xcode/Plug-ins/Kotlin.ideplugin/Contents/Resources/kotlin_lldb.py
```

### Usage

If properly set up, you should be able to add Kotlin source to Xcode, set up breakpoints, and step through code.
Be careful not to have Kotlin source added to the iOS Bundle output.

### Sources

Setting up the Plugin has been an amalgam of various source projects, as Xcode "Plugins"
are undocumented. We aren't adding any "code", so there aren't any signing issues.

[xcode-graphql](https://github.com/apollographql/xcode-graphql)
[xcbuild](https://github.com/facebook/xcbuild)
[rust-xcode-plugin](https://github.com/mtak-/rust-xcode-plugin)

LLDB formatting originally comes from the Kotlin/Native project, source [konan_lldb.py](https://github.com/JetBrains/kotlin-native/blob/dbb162a4b523071f31913e888e212df344a1b61e/llvmDebugInfoC/src/scripts/konan_lldb.py), although the way data is grabbed has been heavily modified to better
support an interactive debugger.