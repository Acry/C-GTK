# Silence warning
cmake_minimum_required(VERSION 3.14)

# Set the project name and the language
PROJECT(tutorial C)

# Use PkgConfig to detect GTK headers/library files
FIND_PACKAGE(PkgConfig REQUIRED)
PKG_CHECK_MODULES(GTK3 REQUIRED gtk+-3.0)

# Setup CMake to use GTK, tell the compiler where to look for headers
# and to the linker where to look for libraries
INCLUDE_DIRECTORIES(${GTK3_INCLUDE_DIRS})
LINK_DIRECTORIES(${GTK3_LIBRARY_DIRS})

# Add an executable compiled from c source
ADD_EXECUTABLE(demo main.c)

# Link the target to the GTK libraries
TARGET_LINK_LIBRARIES(demo ${GTK3_LIBRARIES})

