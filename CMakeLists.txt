cmake_minimum_required(VERSION 3.22)

project(LearnSYCL LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)

find_package(IntelSYCL REQUIRED)

# Get a list of all .cpp files in the root directory
file(GLOB_RECURSE sources RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} "*.cpp")

# Create an executable target for each .cpp file
foreach (file_path ${sources})
    get_filename_component(filename "${file_path}" NAME_WE)
    add_executable("${filename}" "${file_path}")
    target_include_directories("${filename}" PRIVATE src)
    add_sycl_to_target(TARGET "${filename}" SOURCES "${file_path}")
endforeach ()
