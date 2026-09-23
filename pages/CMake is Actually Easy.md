- CMake is known for the industry standard of C++ meta-build system. The main reason why C++ requires meta build system is because every operating system has its own preferred build tools. For example, Windows expects solution files (.sln), while Linux traditionally relies on GNU Make (Makefiles). If C++ has a standardized build system, there won't be need for meta build system. You can think of standardized build system like `npm` for Node.js or `cargo` for Rust.
-
- ## How to add dependencies to our project?
-
- Adding external dependencies is a common practice when building a project, in fact, most of the libraries we need have already been built by someone else. Instead of building the same thing from scratch (reinventing the wheel), we just need to add those libraries to our project, by this, we make the development process a lot faster and easier as we focused on the part that is most important to our project.
- Adding dependencies in other languages is a piece of cake, For example:
- In Nodejs, you can use: `npm add <library>`
- In Go, you can use: `go get <url>`
- In Rust, you can use: `cargo add <library>`
-
- But in C++, things don't go as easy. There are multiple ways to add a library to our project.
-
- **1. The modern and recommended approach**
- This method relies on a CMake feature called `FetchContent`. Note that this only work on a library that has `CMakeLists.txt` on it. Here's an example to add a library from a github repository.
-
- ```txt
  include(FetchContent)
  
  FetchContent_Declare(
    glfw
    GIT_REPOSITORY https://github.com/glfw/glfw
    GIT_TAG 3.5.1
  )
  
  FetchContent_MakeAvailable(glfw)
  
  target_link_libraries(your_project_name PRIVATE glfw)
  ```
-
- **2. Copy and paste**
- If you copy and paste a piece of source code to your `third_party` directory, you can make it as a static library first, then link it against your project.
- ```txt
  add_library(glad STATIC third_party/glad/src/glad.c)
  
  # header files
  target_include_directories(glad PUBLIC third_party/glad/include)
  
  target_link_libraries(your_project_name PRIVATE glad)
  ```
- The first line is telling CMake to build it as a `static` library.
- Second line is providing header files, and the `PUBLIC` keyword here tells it to be exposed to our project so we can access them. For example in our C++ file: `#include <glad/glad.h>`, if we set it to `PRIVATE`, we won't be able to add that include header.
-
- **3. Git submodule**
- As the name say, you use `git submodule`, the downsides are you need to use `git` and the `--recursive` flag which I always forgot how to use it.
-
- **4. ExternalProject_Add**
- This one is kind of old, I don't know really know how.
-
- #cmake #cpp #unfinished
-