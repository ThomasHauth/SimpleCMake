cmake_minimum_required (VERSION 2.6)
project (Simple) 

# assume a gcc-style compiler is used
set(CMAKE_CXX_FLAGS "-O2 -g -ggdb")

add_executable (Simple Simple.cpp) 

