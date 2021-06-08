## Setup toolchain and SDK
---

1. Firstly, we need to download the official C/C++ SDK form Rapsberry Pi foundation. So, nvaigate to the directory where you want your SDK to be stored and run the following command -

`git clone -b master https://github.com/raspberrypi/pico-sdk.git`

*This will create a directory named pico-sdk in the current directory*

2. For the SDK to be available while building your projects, it is necessary to create an environment variable to store the SDK directory's path. This environment variable must be name `PICO_SDK_PATH`. To do this use the following command -

`export PICO_SDK_PATH='PATH TO pico-sdk DIRECTORY ON YOUR SYSTEM'`

*You may put the above command in `.zshrc` or `.bashrc` file so you don't have to manually export it everytime. If these files do not exist in your user directory then, you may create them and add the above command.*

3. Now you are ready to install the toolchain required for building applications for your pico board. You require `cmake` and `arm-none-eabi-gcc`. To install them use the following commands -

`brew install cmake`

`brew tap ArmMbed/homebrew-formulae`

`brew install arm-none-eabi-gcc`

4. Now you are ready to build application for raspberry pi pico. You can build your applications using command line or using `Visual Studio Code`.

---

## Creating and building projects

1. Create a directory where all your project files will live. Make sure that the `PICO_SDK_PATH` environment variable has been created (either manually or if specific in `.zshrc` or `.bashrc`.) For the purpose of explanation lets say that we create a project directory named `test`.

2. Now you need to copy a file from the sdk. This file is named `pico_sdk_import.cmake` and lives inside `pico-sdk/external` directory. To do this you may use the following command -

`cp $PICO_SDK_PATH/external/pico_sdk_import.cmake .`

3. Within the project directory put in your source files and a `CMakeLists.txt` file. Lets assume that our project contains only one source file named `test.c`. At this stage the directory `test` will contain three files - `test.c`,  `CMakeLists.txt` and `pico_sdk_import.cmake`. For our particular case the CMakeLists.txt file will have the following lines -

`cmake_minimum_required(VERSION 3.13)`

`include(pico_sdk_import.cmake)`

`project(test_project C CXX ASM)`

`set(CMAKE_C_STANDARD 11)`

`set(CMAKE_CXX_STANDARD 17)`

`pico_sdk_init()`

`add_executable(test test.c)`

`target_link_libraries(test pico_stdlib)`

`pico_add_extra_outputs(test)`

4. Finally create a directory named `build` inside your project directory and navigate to it using you shell. Now run the following commands -

`cmake ..`
`make`

5. If there are no errors in the source code, you will find the compiled executables in the build directory. 

For more complex applicationo you only need to put modify the `CMakeLists.txt` file.

---

## For more information refer to the Official Raspberry Pi Foundation guide - [SDK guide](https://www.uctronics.com/download/Datasheet/C_and_C++_development_with_Raspberry_Pi_Pico_and_RP2040_based_boards.pdf)