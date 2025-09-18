---
aliases:
  - C++ Build Process
---
# C++ Build Process
> From https://www.studyplan.dev/cmake/cpp-build-process

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