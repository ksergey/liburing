file(GLOB sources "*.c" "*.cc")

# exclude helpers.c from list
list(FILTER sources EXCLUDE REGEX ".*/helpers.c$")

find_package(Threads)

# compile helpers.c as library
add_library(uring_test_helpers STATIC ${CMAKE_CURRENT_SOURCE_DIR}/helpers.c)
target_link_libraries(uring_test_helpers PUBLIC ${CMAKE_THREAD_LIBS_INIT})

foreach (source ${sources})
  get_filename_component(testName ${source} NAME_WE)

  add_executable(${testName} ${source} helpers.c)
  target_compile_options(${testName}
    PRIVATE -Wall -Wextra -Wno-unused-parameter -Wno-sign-compare -g)
  target_compile_definitions(${testName}
    PRIVATE -D_GNU_SOURCE -D__SANE_USERSPACE_TYPES__)
  target_link_libraries(${testName}
    PRIVATE uring uring_test_helpers)

  add_test(${testName} ${testName})
endforeach()
