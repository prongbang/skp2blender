# skp2blender

Python bindings for the official Sketchup API and an importer for blender based on them

## Install dev tools

- Install Python3 

```shell
brew install python@3.11
```

- Install Cython from shell: 

```shell
pip3 install Cython --install-option="--no-cython-compile"
```

- Download Sketchup SDK https://extensions.sketchup.com/sketchup-sdk

## Build for macOS

1. Copy `LayOutAPI.framework` and `SketchUpAPI.framework` from SDK directory to `skp2blender`

2. Build macOS version

```shell 
python3 setup.py build_ext --inplace
```

3. Run the two last lines of setup script manually: 

```shell
install_name_tool -change @rpath/SketchUpAPI.framework/Versions/Current/SketchUpAPI @loader_path/SketchUpAPI.framework/Versions/Current/SketchUpAPI sketchup.cpython-311-darwin.so 
```

```shell
install_name_tool -change @rpath/SketchUpAPI.framework/Versions/A/SketchUpAPI @loader_path/SketchUpAPI.framework/Versions/A/SketchUpAPI sketchup.cpython-311-darwin.so
```

## Pack add-ons for macOS

Copy the following files from `skp2blender` to `sketchup-importer-macos`

1. `LayOutAPI.framework` 

```shell
cp -R LayOutAPI.framework sketchup-importer-macos
```

2. `SketchUpAPI.framework` 

```shell
cp -R SketchUpAPI.framework sketchup-importer-macos
```

3. `sketchup.cpython-311-darwin.so`

```shell
cp -R sketchup.cpython-311-darwin.so sketchup-importer-macos/sketchup.so
```

Zip add-ons

```shell
zip -r sketchup-importer-0.23.2-macos.zip sketchup-importer-macos
```

## Install add-ons to Blender

1. Open blender
2. Edit -> Preferences -> Add-Ons -> Install -> sketchup-importer-0.23.2-macos.zip

