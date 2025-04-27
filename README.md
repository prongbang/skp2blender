# skp2blender 🔄

[![Blender](https://img.shields.io/badge/Blender-3.0+-orange.svg)](https://www.blender.org/)
[![SketchUp](https://img.shields.io/badge/SketchUp%20SDK-Latest-green.svg)](https://extensions.sketchup.com/sketchup-sdk)
[![Python](https://img.shields.io/badge/Python-3.11-blue.svg)](https://www.python.org/)
[![Platform](https://img.shields.io/badge/platform-macOS-lightgrey.svg)](https://www.apple.com/macos/)

> Python bindings for the official SketchUp API and an importer for Blender. Seamlessly transfer your SketchUp models to Blender.

## ✨ Features

- 🔗 **Native API Bindings** - Direct access to SketchUp's official API
- 🎯 **One-Click Import** - Import SketchUp files directly into Blender
- 🚀 **Optimized Performance** - Fast and efficient conversion process
- 🔄 **Material Support** - Preserves materials and textures
- 🎨 **Component Hierarchy** - Maintains model structure and organization
- 🍎 **macOS Support** - Both Intel and Apple Silicon architectures

## 📥 Download Prebuilt Add-ons

Download the appropriate version for your Mac:

- [**macOS (Intel)**](https://github.com/prongbang/skp2blender/raw/master/add-ons/sketchup-importer-0.23.2-macos-intel.zip)
- [**macOS (Apple Silicon)**](https://github.com/prongbang/skp2blender/raw/master/add-ons/sketchup-importer-0.23.2-macos-arch64.zip)

## 🚀 Quick Installation

1. Download the appropriate version above
2. Open Blender
3. Go to `Edit → Preferences → Add-Ons → Install`
4. Select the downloaded zip file
5. Enable the "Import-Export: SketchUp Importer" add-on
6. Done! You can now import SketchUp files via `File → Import → SketchUp (.skp)`

## 🛠️ Build from Source

### Prerequisites

1. **Python 3.11**
   ```shell
   brew install python@3.11
   ```

2. **Cython**
   ```shell
   pip3 install Cython --install-option="--no-cython-compile"
   ```

3. **SketchUp SDK**
   - Download from [SketchUp SDK](https://extensions.sketchup.com/sketchup-sdk)

### Build Process

1. **Prepare SDK Files**
   ```shell
   # Copy SDK frameworks to skp2blender directory
   cp -R /path/to/SDK/LayOutAPI.framework ./skp2blender/
   cp -R /path/to/SDK/SketchUpAPI.framework ./skp2blender/
   ```

2. **Build Python Extension**
   ```shell
   cd skp2blender
   python3 setup.py build_ext --inplace
   ```

3. **Fix Dynamic Library Paths**
   ```shell
   install_name_tool -change @rpath/SketchUpAPI.framework/Versions/Current/SketchUpAPI \
     @loader_path/SketchUpAPI.framework/Versions/Current/SketchUpAPI \
     sketchup.cpython-311-darwin.so
   
   install_name_tool -change @rpath/SketchUpAPI.framework/Versions/A/SketchUpAPI \
     @loader_path/SketchUpAPI.framework/Versions/A/SketchUpAPI \
     sketchup.cpython-311-darwin.so
   ```

### Package the Add-on

1. **Prepare Add-on Directory**
   ```shell
   mkdir -p sketchup-importer-macos
   ```

2. **Copy Required Files**
   ```shell
   # Copy frameworks
   cp -R LayOutAPI.framework sketchup-importer-macos/
   cp -R SketchUpAPI.framework sketchup-importer-macos/
   
   # Copy compiled extension
   cp sketchup.cpython-311-darwin.so sketchup-importer-macos/sketchup.so
   ```

3. **Create ZIP Archive**
   ```shell
   cd sketchup-importer-macos
   zip -r ../sketchup-importer-0.23.2-macos.zip .
   ```

## 📚 Usage

After installation, you can import SketchUp files in Blender:

1. Go to `File → Import → SketchUp (.skp)`
2. Select your SketchUp file
3. Configure import options if needed
4. Click "Import SKP"

### Import Options

- **Scale**: Adjust the scale factor for imported models
- **Import Cameras**: Include cameras from SketchUp file
- **Import Lights**: Include lights from SketchUp file
- **Reuse Materials**: Optimize material import for multiple objects

## 🔧 Troubleshooting

### Common Issues

1. **Import Error**
   - Ensure you've downloaded the correct version for your Mac
   - Check that the add-on is properly enabled in Blender preferences

2. **Build Failures**
   - Verify Python version matches (3.11)
   - Ensure SketchUp SDK is properly downloaded and extracted
   - Check that all prerequisites are installed

3. **Runtime Errors**
   - Make sure all framework files are in the correct location
   - Verify dynamic library paths are correctly set

## 🙏 Acknowledgments

- [SketchUp SDK](https://extensions.sketchup.com/sketchup-sdk) for providing the API
- [Blender](https://www.blender.org/) community for the amazing 3D software
- All contributors who have helped improve this project

---
