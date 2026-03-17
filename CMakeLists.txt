# Always run the below commmand after changing this file!
# cmake -B build -S .

cmake_minimum_required(VERSION 3.16)

project(genesis)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Export compile_commands.json for clangd
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

file(GLOB_RECURSE SRC_FILES
   src/*.cpp
)

add_executable(genesis ${SRC_FILES})