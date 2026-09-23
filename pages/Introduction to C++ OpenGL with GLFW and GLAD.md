- OpenGL is just a specification.
- GLFW is a window management library.
- GLAD is a loader for OpenGL.
-
- First, we're going to setup GLFW.
- Here's how to do it (placeholder)
-
- Before being able accessing OpenGL API, you first need to load it, that's what GLAD used for. Without it, the program will exit with **core dumped**.
-
- This is the syntax to load OpenGL with GLAD:
- ```cpp
    int ok = gladLoadGLLoader((GLADloadproc)glfwGetProcAddress);
  ```
- Before that, make sure to call `glfwMakeContextCurrent(window)` first, otherwise it'll fail.
-
- **Why is there no triangle when specified with the GLFW window hint?**
-
- There's a scenario where you use OpenGL version 4.5+, and you already set up everything, there's still no triangle showed up. But it worked without the hint.
- ```cpp
    glfwWindowHint(GLFW_CONTEXT_VERSION_MAJOR, 4);
    glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, 5);
    glfwWindowHint(GLFW_OPENGL_PROFILE, GLFW_OPENGL_CORE_PROFILE);
  ```
- That's because OpenGL 4.5 or something, strictly requires VAO or Vertex Array Object.
-
-
- #cpp #glfw #glad #opengl #cmake #unfinished
-
-