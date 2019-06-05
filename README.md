# DoorWatcher
DoorWatcher is an IoT project that opens doors with the help of "face recognition". In addition it also allows monitoring via the browser. 


## Contents
* [Equipment](#Equipment)
* [Installation](#Installation)
* [Usage](#Usage)
* [Troubleshooting and FAQ](#Troubleshooting-and-FAQ)

***

## Equipment
### Hardware
- Raspberry Pi Zero W
- Camera V2.1 NoIR
### Software
- OpenCV & dlib
- Virtual environment

## Installation
First we are going to install all needed packages with the **doorwatcher_software.sh** script. This will take around 2-3h mainly because of the dlib and the opencv compiling...  
  1. move the script to home directory `mv doorwatcher_software.sh ~/doorwatcher_software.sh`
  2. give the script wirting rights `chmod +x doorwatcher_software.sh` and run the script `/.doorwatcher_software.sh`

## Usage


## Troubleshooting and FAQ
#### [1] ERROR
  ```
  modprobe: ERROR: ../libkmod/libkmod.c:586 kmod_search_moddep() could not open moddep file '/lib/modules/4.14.98-v7+/modules.dep.bin'
  modprobe: FATAL: Module bcm2835-v4l2 not found in directory /lib/modules/4.14.98-v7+
  modprobe: ERROR: ../libkmod/libkmod.c:586 kmod_search_moddep() could not open moddep file '/lib/modules/4.14.98-v7+/modules.dep.bin'
  modprobe: FATAL: Module bcm2835-v4l2 not found in directory /lib/modules/4.14.98-v7+
  ```
  To fix this error just simple run following command `sudo rpi-update 963a31330613a38e160dc98b708c662dd32631d5` and then reboot the     raspberry pi

#### [2] ERROR
  ```
  opencv_test_core_pch_dephelp.dir/opencv_test_core_pch_dephelp.cxx.o
  In file included from /home/joey/opencv/opencv/opencv/modules/core/test/test_precomp.hpp:12:0,
                   from /home/joey/opencv/opencv/build/modules/core/opencv_test_core_pch_dephelp.cxx:1:
  /home/joey/opencv/opencv/opencv/modules/core/include/opencv2/core/private.hpp:66:12: fatal error: Eigen/Core: No such file or directory
  #  include <Eigen/Core>
              ^~~~~~~~~~~~
  compilation terminated.
  modules/core/CMakeFiles/opencv_test_core_pch_dephelp.dir/build.make:62: recipe for target       'modules/core/CMakeFiles/opencv_test_core_pch_dephelp.dir/opencv_test_core_pch_dephelp.cxx.o' failed
  make[2]: *** [modules/core/CMakeFiles/opencv_test_core_pch_dephelp.dir/opencv_test_core_pch_dephelp.cxx.o] Error 1
  CMakeFiles/Makefile2:1229: recipe for target 'modules/core/CMakeFiles/opencv_test_core_pch_dephelp.dir/all' failed
  make[1]: *** [modules/core/CMakeFiles/opencv_test_core_pch_dephelp.dir/all] Error 2
  make[1]: *** Waiting for unfinished jobs....
  ```
  To fix this error you will need to change the file **cmake/OpenCVFindLibsPerf.cmake**. If you can't find the file just go to the root directory `cd /` and run the this command `sudo find -name "OpenCVFindLibsPerf.cmake"`
  
  LINE | OLD | NEW 
  --- | --- | ---
  44 | `find_package(Eigen3 QUIET)` | `find_package(Eigen3 3.0.0)`
  49 |`list(APPEND OPENCV_LINKER_LIBS Eigen3::Eigen)`|`#list(APPEND OPENCV_LINKER_LIBS Eigen3::Eigen)`           
  50 |`set(HAVE_EIGEN 1)`| `#set(HAVE_EIGEN 1)`
  