# 🎮 OpenGL Setup in Visual Studio (C++)

This guide shows how to set up an OpenGL project using:
- [GLFW](https://www.glfw.org/) – for window/input
- [GLAD](https://glad.dav1d.de/) – for OpenGL function loading
- [CMake](https://cmake.org/download/) – to build your project easily

---

## ✅ Prerequisites

- Visual Studio (with C++ tools installed)
- CMake: [Download CMake](https://cmake.org/download/)

---

## 📁 1. Project Structure

Create a folder like this:
```
MyOpenGLProject/
│
├── CMakeLists.txt
├── main.cpp
├── external/
│   ├── glfw/
│   └── glad/
```

---

## 📥 2. Download Dependencies

### GLFW:
1. Go to [glfw.org](https://www.glfw.org/download.html).
2. Download the **source** ZIP.
3. Extract it into `external/glfw`.

### GLAD:
1. Visit [glad.dav1d.de](https://glad.dav1d.de/).
2. Settings:
   - Language: **C/C++**
   - Specification: **OpenGL**
   - API: **OpenGL 3.3** (or newer if you want)
   - Profile: **Core**
3. Click **Generate**.
4. Extract the ZIP into `external/glad`.

---

## 🧱 3. CMakeLists.txt Example

```cmake
cmake_minimum_required(VERSION 3.10)
project(MyOpenGLApp)

set(CMAKE_CXX_STANDARD 17)

# Add GLFW
add_subdirectory(external/glfw)

# Add GLAD
add_library(glad 
    external/glad/src/glad.c
)
target_include_directories(glad PUBLIC external/glad/include)

# Add include directories
include_directories(
    external/glad/include
    external/glfw/include
)

# Executable
add_executable(MyOpenGLApp main.cpp)

# Link everything
target_link_libraries(MyOpenGLApp
    glfw
    glad
    ${CMAKE_DL_LIBS}
)
