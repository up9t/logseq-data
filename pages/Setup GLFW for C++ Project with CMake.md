-
- First of all you need to download the necessary dependencies https://www.glfw.org/docs/latest/compile.html#compile_deps_wayland
-
- In the documentation, it says Fedora user need to have these installed.
- ```bash
  sudo dnf install -y wayland-devel libxkbcommon-devel libXcursor-devel libXi-devel libXinerama-devel libXrandr-devel
  ```
-
- After installed, we need to configure our CMakeLists.txt. We're going to use FetchContent feature from  CMake, it is modern alternative than the old `ExternalProject_Add`, and better than `git submodule`.
-
- ```txt
  include(FetchContent)
  
  FetchContent_Declare(
    glfw
    GIT_REPOSITORY https://github.com/glfw/glfw
    GIT_TAG 3.5.1
  )
  
  FetchContent_MakeAvailable(glfw)
  
  target_link_libraries(cpp PRIVATE glfw)
  ```
- Then after you modify the CMakeLists.txt file, you don't need to execute the `cmake` command again to generate the build system, you can just use the build system like `ninja` or `cmake --build`.
-
- > GLFW is a library for window management and input only, for actually drawing something inside the created window, you need another library like GLAD for OpenGL, and Google Dawn for WebGPU.
-
-
- #cpp #glfw #setup #cmake #unfinished
-
-