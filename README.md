# ORB-SLAM3 for Windows
ORB-SLAM3 Project for Windows Platform (espacially Visual Studio)  
We have tested the library in Windows 10, Visual Studio 2015.

# Reference
- ORB-SLAM3 project: https://github.com/UZ-SLAMLab/ORB_SLAM3  
- ORB-SLAM2 for windows: https://github.com/Phylliida/orbslam-windows  
- ORB-SLAM2 for windows_2: https://github.com/phdsky/ORBSLAM24Windows  


# Prerequisites

1. Visual Studio: Tested with VS2015

2. Cmake: Required at least 2.8. (Tested with 3.14.7)

3. OpenCV: Required at least 3.0. (Tested with 3.4.1)

4. glew (for pangolin): Tested with 2.1.0

5. boost: Tested with 1.67.0: https://www.boost.org/users/history/version_1_67_0.html  

# Build
## eigen  

## DBoW2  
- Open cmake-gui and make a 'build' directory in ORB-SLAM3forWindows/Thirdparty/DBoW2  
- Click Configure and select Visual Studio 14 2015 x64.  
- Click Generate and open the resulting project in the build directory.  
- Change build type to Release.  
- Right click on DBoW2 project -> Properties -> General -> Target Extension: .lib, and Configure Type: Static Library (.lib)  
- DBoW2 project -> Properties -> C/C++ Tab -> Code Generation -> Runtime Library: Multi-threaded(/MT)  
- Build ALL_BUILD. Finish(DBoW2.lib).

## g2o  
- Open cmake-gui and Make a 'build' directory in ORB-SLAM3forWindows/Thirdparty/g2o  
- Click Configure and select Visual Studio 14 2015 x64.  
- Click Generate and open the resulting project in the build directory.  
- Change build type to Release.  
- Right click on g2o project -> Properties -> General -> Target Extension: .lib, and Configure Type: Static Library (.lib)  
- g2o project -> Properties -> C/C++ Tab -> Code Generation -> Runtime Library: Multi-threaded(/MT)  
- g2o project -> Properties -> C/C++ Tab -> Preprocessor -> Preprocessor Definitions: add a 'WINDOWS'.  
- Build ALL_BUILD. Finish(g2o.lib).

## Pangolin  
- Open cmake-gui and Make a 'build' directory in ORB-SLAM3forWindows/Thirdparty/Pangolin
- Click Configure and select Visual Studio 14 2015 x64.
- cmake error: could not find git for clone of ... : Disable BUILD_EXTERN_GLEW, LIBJPEG, LIBPNG and input value directly (used GLEW only)  
- If window says Configuring Done, it's OK  
- Click Generate and open the resulting project in the build directory.  
- Change build type to Release.  
- pangolin project -> Properties -> C/C++ Tab -> Code Generation -> Runtime Library: Multi-threaded(/MT)  
- Build ALL_BUILD. (ignore error "cannot open input file 'pthread.lib') Finish(pangolin.lib).

## ORB-SLAM3 for Windows  
- Open cmake-gui and make a 'build' directory in ORB-SLAM3forWindows  
- Click Configure and select Visual Studio 14 2015 x64.  
- Click Generate and open the resulting project in the build directory.  
- Change build type to Release.  
- Setting Boost Library (include, dir, ...)
- Right click on ORB-SLAM3 project -> Properties -> General -> Target Extension: .lib, and Configure Type: Static Library (.lib)  
- ORB-SLAM3 project -> Properties -> C/C++ Tab -> Code Generation -> Runtime Library: Multi-threaded(/MT)  
- ORB-SLAM3 project -> Properties -> C/C++ Tab -> Preprocessor -> Preprocessor Definitions: check 'COMPILEDWITHC11'.  
- Build ORB-SLAM3 (not ALL_BUILD). Finish(ORB_SLAM3.lib)  

# Test Program
We have tested the following projects: **mono_euroc, mono_inertial_euroc, stereo_euroc, stereo_inertial_euroc**

## example: The EuRoC MAV Dataset: monocular-inertial
- Open **mono_inertial_euroc** directory in ORB-SLAM3forWindows.  
- Change build type to Release.  
- Setting Boost Library (include, dir, ...)  
- Right click on mono_inertial_euroc project -> Properties -> C/C++ Tab -> Code Generation -> Runtime Library: Multi-threaded(/MT)  
- mono_inertial_euroc project -> Properties -> Linker -> Advanced -> Delete import library.  
- Define 'usleep' function in mono_inertial_euroc.cc
- Build mono_inertial_euroc.  Finish(mono_inertial_euroc.exe).
- **Visual Studio 0xC00000FD: Stack overflow error**: Right click on the project -> Properties -> Linker -> System -> Stack Reserve Size: 8388608 (the default stack size is 1MB = 1048576)
- You will find the test program in ORB-SLAM3forWindows\Examples\Monocular-Inertial\Release.  
- Download the EuRoC MAV Dataset: https://projects.asl.ethz.ch/datasets/doku.php?id=kmavvisualinertialdatasets
- Convert ORBvoc.txt.tar.gz -> ORBvoc.txt
- Execute the following script:  
`mono_inertial_euroc.exe (path_to_vocabulary) (path_to_settings) (path_to_image_folder_1) (path_to_times_file_1) (path_to_image_folder_2) (path_to_times_file_2) ... (path_to_image_folder_N) (path_to_times_file_N)`
- The result of Machine Hall 01 Dataset (monocular-inertial):  
<img width="980" alt="example_mono_inertial_euroc" src="https://user-images.githubusercontent.com/68829425/88619172-de098a00-d0d5-11ea-8167-2329bd44611a.png">
