---
aliases:
  - C++ Build Process
---
# C++ Build Process
> From [studyplan.dev](https://www.studyplan.dev/cmake/cpp-build-process)

This course is about how to use CMake to build C++ projects.

We learned C++ in my degree, but never how to use CMake (maybe because my already credited courses from my previous DEC talked about it). I actually used it a bit in an internship to build a program running on multiple ESP32s with the ESP-IDF.

I want to use it more in my next projects, be it in C or C++.

## Sections

### Chapter 1
This chapter was mostly revision of what I already knew about compilers, with added information about compiler flags and the `ar` program for static libraries.

It presents mostly each step of the compilation process (preprocessing, compiling, assembling, linking) and shows the different tools needed to do it by hand in the CLI before using CMake.

#### 📌 Learned 
- Compiler flags for different steps of the compilation process
- `ar` for archiving static libraries
- Position-Independent Code for dynamic libraries
- A simple Hello World program with `<iostream>` is 25k lines after preprocessing since it includes the whole iostream headers

---
### Chapter 2
This chapter presents the organization of a C++ project as well as build systems and their limitations for complex projects. It talked about versioning, project layout, API vs ABI, etc.

#### 📌 Learned 
- Typical C++ projet layout consisting of `src` folder for the source code and private headers, `include` folder for the public headers and`libs` folder for external libraries
- Two ways of separating multiple parts of a project like `core` and `graphics` by either having folder for each part under `src` and `include` or having `src` and `include` in each folder of each part
- Compiler flags for linking libraries (`-I`, `-L`, `-l`)
- Semantic versioning
- Platform differences such has two file system for a `dll` on Windows (`.lib` and `.dll`) vs `.so` on Linux and macOS
- Limitations of Makefiles and IDE Project files such as vendor lock-in, dependency on GUI or the monolithic unreadable single Makefile and duplication when splitting it