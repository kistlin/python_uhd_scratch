# UHD
## Compile
### Preparations
#### Windows
##### libusb
Download libusb from [github](https://github.com/libusb/libusb/releases)

##### CMake command line to generate solution
```
"C:\Program Files\CMake\bin\cmake.exe" -G "Visual Studio 16 2019" -A x64
-DCMAKE_CONFIGURATION_TYPES:STRING=Release
-DCMAKE_INSTALL_PREFIX:PATH=C:/libs/uhd-4.0.0.0/_install
-DENABLE_PYTHON_API:BOOL=ON
-DENABLE_USB:BOOL=ON
-DENABLE_B200:BOOL=ON
-DBoost_DIR="C:/libs/boost/boost_1_75_0/_install/lib/cmake"
-DBOOST_INCLUDEDIR="C:/libs/boost/boost_1_75_0/_install/include/boost-1_75"
-DPYTHON_EXECUTABLE="C:/tools/WinPython/WPy64-3920/python-3.9.2.amd64/python.exe"
-DPYTHON_INCLUDE_DIR="C:/tools/WinPython/WPy64-3920/python-3.9.2.amd64/include"
-DPYTHON_LIBRARY="C:/tools/WinPython/WPy64-3920/python-3.9.2.amd64/libs/python39.lib"
-DRUNTIME_PYTHON_EXECUTABLE="C:/tools/WinPython/WPy64-3920/python-3.9.2.amd64/python.exe"
-DLIBUSB_INCLUDE_DIRS="C:/libs/libusb-1.0.24/include/libusb-1.0"
-DLIBUSB_LIBRARIES="C:/libs/libusb-1.0.24/VS2019/MS64/dll/libusb-1.0.lib"
../host
```

## Post-build
### Windows
#### Auto-completion for IDEs
```
mklink "C:\tools\WinPython\WPy64-3920\python-3.9.2.amd64\Lib\site-packages\libpyuhd.pyd" "C:\tools\WinPython\WPy64-3920\python-3.9.2.amd64\Lib\site-packages\uhd\libpyuhd.pyd"
```

#### Make dependant dll's available
Changes in `C:\tools\WinPython\WPy64-3920\python-3.9.2.amd64\Lib\site-packages\uhd\__init__.py` at the top
```
import os
os.add_dll_directory(r'C:\libs\libusb-1.0.24\VS2019\MS64\dll')
os.add_dll_directory(r'C:\libs\uhd-4.0.0.0\_install\bin')
```

## USRP images
Download firmware images from `https://github.com/EttusResearch/uhd/releases`
### Windows
#### Environment variables
Set the following environment variable for uhd where to search for images.
```
UHD_IMAGES_DIR=C:\libs\uhd-images_4.0.0.0
```

## Run test script
Don't increase duration too much, this already produces an 80 MB file.
```
python pyuhd_rx_to_file.py --output-file test.bin --freq 107400000 --rate 1e6 --duration 10.0 --channels 0 --gain 10
```
