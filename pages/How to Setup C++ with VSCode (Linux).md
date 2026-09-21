- First, install the required tools: `cmake`, `clang`, `gdb`, `ninja`.
-
- `cmake` to make the build system for the project.
- `ninja` to build the project using the generated build system from `cmake`.
- `clang` to compile our C++ source code. Actually we use `clang++` because `clang` is for C.
- `gdb` to debug later.
- You're also going to need `ld` but that's usually installed by default.
-
- Here's how to install them in Fedora.
-
- ```bash
  sudo dnf install -y cmake ninja clang gdb
  ```
-
- Close all the VSCode instances, because we are going to reopen them later. Now, create a new directory for your C++ project. And open that directory in VSCode.
-
- ```bash
  # create new directory named myproject
  mkdir myproject
  
  # open myproject directory in VSCode
  code myproject
  ```
-
- Then, open up VSCode and install the `ms-vscode.cpptools` and `ms-vscode.cmake-tools` extensions if you haven't.
- After finished installing everything. Press `CTRL` + `SHIFT` + `P` to open command menu and search for `CMake: Quick Start`, this will help you quickly bootstrap your `cmake` configuration. Choose executable, and then choose a name for your project. Tweak the generated `CMakeLists.txt` as needed.
- Create a new C++ file named main.cpp and make a simple program.
-
- ```cpp
  #include <iostream>
  #include <string>
  
  int main() { 
    std::string name = "Yasa";
    std::cout << "Hello, " << name << std::endl;
    
    return 0;
  }
  ```
-
- Now we're going to build the project and place the output in a new `build` directory. Run this command in your project directory.
-
- ```bash
  cmake -G Ninja -D CMAKE_CXX_COMPILER=clang++ -B build -S .
  ```
-
- A new directory named `build` will appear, you then need to build the build directory.
-
- ```bash
  cmake --build build
  
  # or explicitly
  ninja -C build
  ```
-
- Now you're going to see the binary in the `build` directory named after your cmake `add_executable`.
- If you make any change to your C++ files, you don't need to call the `cmake -G Ninja -D ...` everytime, you just need to build it with `cmake --build build` or `ninja -C build`.
-
- ## Configuring Preset (Optional)
-
- Preset is useful if you want to change between `debug` and `release` mode easily, or you want to use other generator than `ninja`, etc.
- Configuring it is very easy in VSCode, open the command menu, and search `CMake: Add Configure Preset`. And adjust as needed. Here's an example.
-
- ```json
  {
    "version": 8,
    "configurePresets": [
      {
        "name": "clang",
        "displayName": "Clang++",
        "description": "Sets Ninja generator, build and install directory",
        "generator": "Ninja",
        "binaryDir": "${sourceDir}/build",
        "cacheVariables": {
          "CMAKE_CXX_COMPILER": "clang++",
          "CMAKE_BUILD_TYPE": "Release"
        }
      },
      {
        "name": "clang-debug",
        "displayName": "Clang++ Debug",
        "description": "Sets Ninja generator, build and install directory",
        "generator": "Ninja",
        "binaryDir": "${sourceDir}/build",
        "cacheVariables": {
          "CMAKE_CXX_COMPILER": "clang++",
          "CMAKE_BUILD_TYPE": "Debug"
        }
      }
    ]
  }
  ```
- Now, I can do this instead.
- ```bash
  # for release mode
  cmake --preset clang
  
  # for debug mode
  cmake --preset clang-debug
  ```
- Remember that cmake is for generating build system, you still need to build it after with `cmake --build build`.
-
-
- #cpp #vscode #fedora #linux #setup
-