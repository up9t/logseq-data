- Debugging is a process to remove bugs from a program. Simple print to the console to check a value of a variable can also be called debugging because it has the same intention that is to remove a bug from the code.
- For debugging a more complex program, there is a better way to do it by using a debugger.
- A debugger is a program that allows you to pause the program, check a variable, dive into a function, resume the execution, etc.
- Two popular debuggers for C++ are `gdb` and `lldb`.
- `gdb` is usually installed by default on most linux system including Fedora and Ubuntu. While `lldb` is part of the `llvm` project and isn't installed by default, you have to install it first, either by using package manager or download it somewhere on the internet.
- You don't need to install `lldb` to debug `clang++` program, `gdb` supports too. That's because compilers (e.g `clang++`/`g++`) produce the same debug symbols that has been standardized by the OS.
- In this example, I will use `cmake`, `ninja`, `clang`,  and `gdb`. Let's install them.
-
- ```bash
  sudo dnf install -y cmake ninja clang gdb
  ```
-
- After that, you need to know [[How to Setup C++ with VSCode (Linux)]].
-
- ## Create a VSCode debug configuration
-
- Press `CTRL` + `SHIFT` + `D` to enter the debug menu from the sidebar file explorer. Then click the link to create `launch.json`
  logseq.order-list-type:: number
- Click `Add Configuration` button on the bottom right. And choose `gdb launch`. This will automatically create an entry for you in the `launch.json`.
  logseq.order-list-type:: number
- Change the `program` path to your binary path. Which under the `build` directory.
  logseq.order-list-type:: number
- In your C++ code, add some breakpoints by clicking on the left side of the line code, or by pressing `F9` key on your keyboard.
  logseq.order-list-type:: number
- In the sidebar menu again, press the green-outlined play button.
  logseq.order-list-type:: number
- Upon running, your program will pause to the first breakpoint, you can inspect the variable or continue to the next breakpoint by clicking the continue button.
  logseq.order-list-type:: number
-
- ## Launch vs Attach
-
- There are two terms to start a debugger: `launch` and `attach`.
-
- `launch` means the debugger will launch our binary code by itself from start.
- `attach` means the program is already running, and we just make the debugger to attach to the running program.
-
-
- #debug #linux #fedora #vscode #cpp #clang #cmake
-
-