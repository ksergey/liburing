cmake_minimum_required(VERSION 3.14)

project(liburing)

add_subdirectory(src)
add_subdirectory(examples)

enable_testing()
add_subdirectory(test)
